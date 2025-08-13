guide me through creating a component test for the following: 

1. **Current State:** - The `processDemandCleansing` method triggers the demand cleansing job. - The job currently processes only `context` and `demandCleansingPolicyID`. - There's no parameter or flag indicating whether it's "classification only." 2. **Goal:** - Introduce a Boolean flag (e.g., `isClassificationOnly`) that propagates through the system without disrupting existing logic. - Ensure this flag makes it to the `DemandCleansingRequestDTO` for downstream processing. - 
   

 **1. Add a Boolean to the API Layer** - Update the controller: - Create a new API endpoint or extend the existing one to include `isClassificationOnly`. - Validate and process the flag from the UI input. - Potential Code Change on this level

```
java
@RequestMapping("/demandCleansing/classifcationOnly")
public ResponseEntity<Void> triggerDemandCleansing(
    @RequestParam String policyId, {
    demandCleansingService.processDemandCleansing(policyId, true);
    return ResponseEntity.ok().build();
}
```

### **2. Modify the `processDemandCleansing` Signature** - Add `Boolean isClassificationOnly` as a parameter. - Update logic to handle this flag, ensuring it is persisted in subsequent calls. - Potential Code Changes: Map Service

```
java
    public void processDemandCleansing(Context context, String demandCleansingPolicyId, boolean isClassificationOnly)
     {
            logger.trace(() -> ">> processDemandCleansing() for demandCleansingPolicyId: " + demandCleansingPolicyId);
            DemandCleansingPolicy cleansingPolicy =
                    demandCleansingPolicyService.findByDemandCleansingPolicyId(context, demandCleansingPolicyId);
            if(cleansingPolicy == null)
            {
                String messageString = MessageFormat.format("Demand Cleansing Policy with Id : {0} not found", demandCleansingPolicyId);
                Message message = new Message(MessageType.ERROR, "ERROR", messageString);
                List<Message> messageList = new ArrayList<>();
                messageList.add(message);
                throw ManhRuntimeExceptionUtil.getRuntimeException(ExceptionReason.NOT_FOUND, null, messageList,
                        message.getDescription(), null, true);
            }
            triggerDemandCleansingJob(context, demandCleansingPolicyId,isClassificationOnly);
            logger.trace(() -> "<< processDemandCleansing() ");
        }
```

```
java
    public void processDemandCleansing(Context context, DemandCleansingRequestDTO demandCleansingRequestDTO, boolean isClassificationOnly) {
        
       //add getter and setter to demandCleansingRequestDTO per #4
    
        demandCleansingRequestDTO.setIsClassificationOnly(isClassificationOnly);
         demandCleansingService.cleanseDemand(context, demandCleansingRequestDTO);
    
    }
```

- service:

```
java
    //line 204
    //so within the engine context builder, there needs to be a way to persist the boolean, 
    //so we need to add that within the demand engine context builder
    //eg:
    DemandCleansingEngineContext demandCleansingEngineContext =
                                    new DemandCleansingEngineContext.Builder().withContext(context)
                                            .withDemandCleansingPolicy(cleansingPolicy)
                                            .withBusinessCalendarDTO(businessCalendarDTO)
                                            .withItemLocationFactorsByItemAndLocation(
                                                    itemLocationFactorsDTOMapByItemAndLocation)
                                            .withDemandSmoothingPeriodTypes(getDemandSmoothingPeriodTypes(context))
                                            .withMetricsByItemAndLocation(metricByItemLocation)
                                            .withPromoEventsByItemAndLocation(promoEventMap)
                                            .build();
```

- adapter - line 95

```
java
DemandCleansingBatchContext batchContext = new DemandCleansingBatchContext();

//set Is ClassiciationOnly
        batchContext.setDemandCleansingPolicy(demandCleansingPolicy);
        batchContext.setCurrentTimePeriod(BusinessCalendarUtil.getWeekTimePeriod(demandCleansingEngineContext.getBusinessCalendarDTO(), currentBusinessDate));
        batchContext.setCurrentBusinessDate(currentBusinessDate);
        batchContext.setProductLocationMap(constructEngineProductLocations(demandCleansingEngineContext));
        batchContext.setHistoryMap(getDemandCleansingHistoryMap(demandCleansingEngineContext));
        batchContext.setDemandSmoothingPeriodTypes(demandCleansingEngineContext.getDemandSmoothingPeriodTypes());

       demandCleansingBatchProcessor.processProductAggregation(batchContext);
```

- ### **3. Update the Listener Logic** - make sure your `isClassificationOnly` flag is passed from `processDemandCleansing` to the listener. - change the listener class to handle and forward the flag to downstream services.

```
java
     public void processDemandCleansing(Context context, Document document)
        {
            logger.debug("--processDemandCleansing() -> Input document {}", document);
            String demandCleansingPolicyId = (String) document.get(EVENT_REFERENCE_ID.getValue());
            List<Map<String,Object>> itemDocumentList = (List<Map<String, Object>>) document.get(ITEM_DETAILS.getValue());
            List<ItemDTO> itemDTOList = itemDocumentList.stream().map(doc -> objectMapper.convertValue(doc, ItemDTO.class)).collect(Collectors.toList());
            String forkId = (String) document.get(FORK_ID.getValue());\
            
            //retrive the boolean from input document and set it to variable isClassificationOnly
            boolean isClassificationOnly = (boolean) document.getOrDefault(IS_CLASSIFICATION_ONLY.getValue(), false);
    
            DemandCleansingRequestDTO demandCleansingRequestDTO = new DemandCleansingRequestDTO();
            demandCleansingRequestDTO.setDemandCleansingPolicyId(demandCleansingPolicyId);
            demandCleansingRequestDTO.setItemDTOs(itemDTOList);
            demandCleansingRequestDTO.setAsyncProcessTrackingId(forkId);
            //add getter and setter to demandCleansingRequestDTO per #4
        demandCleansingRequestDTO.setIsClassificationOnly(isClassificationOnly);
            logger.debug("--processDemandCleansing() -> DemandCleansingRequestDTO {}", demandCleansingRequestDTO);
    
            demandCleansingPolicyMapService.processDemandCleansing(context, demandCleansingRequestDTO);
        }
```

### **4. Extend the `DemandCleansingRequestDTO`** - Add a new field (`Boolean isClassificationOnly`) to this DTO. - make sure your getter and setter methods are added and appropriately used in all relevant classes.

```
java
Private Boolean isClassificationOnly

public Boolean isClassificationOnly()
    {
        return isClassificationOnly;
    }

    public void setisClassificationOnly(Boolean isClassificationOnly)
    {
        this.isClassificationOnly = isClassificationOnly;
    }
```

### **5. Persist the Flag in the Job** - Modify the job creation logic in `triggerDemandCleansingJob`: - Pass `isClassificationOnly` through the job parameters map. - Ensure the flag persists as part of the job execution context. - Map Service Changes:

```
java
 private void triggerDemandCleansingJob(Context context, String demandCleansingPolicyId,boolean isClassificationOnly)
    {
        Map<String, Object> requestMapForDemandCleansingJobType = new HashMap<>();
        requestMapForDemandCleansingJobType.put(JobSchedule.Fields.JOB_TYPE_ID.getCode(),
                ForecastConstants.DEMAND_CLEANSING_JOB_TYPE_ID.getValue());
        Map<String, String> jobParamsField = new HashMap<>();
        jobParamsField.put(JobParameters.Fields.INPUT_KEY.getCode(),
                ForecastConstants.DEMAND_CLEANSING_POLICY_ID.getValue());
        jobParamsField.put(JobParameters.Fields.INPUT_VALUE.getCode(), demandCleansingPolicyId);
        
        //add to forecast Constants isClassifcationOnly Field
        
        jobParamsField.put(JobParameters.Fields.INPUT_KEY.getCode(),
                ForecastConstants.IS_CLASSIFICATION_ONLY.getValue());
        jobParamsField.put(JobParameters.Fields.INPUT_VALUE.getCode(), isClassificationOnly);
        
        
        List<Map<String, String>> listJobParamsField = new ArrayList<>();
        listJobParamsField.add(jobParamsField);
        requestMapForDemandCleansingJobType.put(JobScheduleBase.Fields.FW_JOB_PARAMETERS.getCode(), listJobParamsField);
        Document document = new Document(requestMapForDemandCleansingJobType);
        jobScheduleMapService.triggerAdhocJob(context, document, null);
    }
```

### **6. Update Service and Aggregation Logic** - make sure all of your downstream methods respect the flag: - in `processProductAggregation` class, check for the flag through the demandCleansing Batch Context # Previous work/notes 1. **Backend Integration:** Modify the existing API to accept a flag indicating whether to perform full cleansing or classification only. The API should then pass this flag to the legacy code. 1. API: `/demandCleansingPolicy/triggerDemandCleansing/{demandCleansingPolicyId}` 2. The Method it calls: `demandCleansingPolicyMapService.processDemandCleansing(context, demandCleansingPolicyId);` c. the in the listener class for the method: `public void processDemandCleansing(Context context, DemandCleansingRequestDTO demandCleansingRequestDTO)` d. method it calls : `demandCleansingService.cleanseDemand(context, demandCleansingRequestDTO);` e. `demandCleansingAdapter.cleanseDemandByBatch(demandCleansingEngineContext);` f. `demandCleansingBatchProcessor.processProductAggregation(batchContext);` then the line 262 2. **Legacy Code Modification:** Update the legacy code to recognize the classification-only flag and adjust its behavior accordingly, such as skipping cleansing steps and not persisting unnecessary data. 1. Its the Boolean `boolean isDemandClassificationOnly` in the `processClassifyAndCleanseDemand` method. 2. within that is the `boolean demandClassificationOnly`in the `classifyAndCleanseDemand` method 3. in classifyAndCleanseDemand Method:

```
java
        if (!demandClassificationOnly)
                {
                    cleansedHistory = cleanseDemand(demandCleansingBatchContext, demandCleansingPolicy, originalHistory,
                            demandCleansingResult);
                }
```

So it checks if the flag is false. line 262 (Method `public void processProductAggregation(DemandCleansingBatchContext demandCleansingBatchContext)` )

```
java
 if (demandCleansingBatchContext.isDemandClassificationOnly() && originalHistory != null) {
                                // replacing the raw history with original cleansed units because we are only running
                                // classification
                                IndexedHistory originalCleansedUnits = (IndexedHistory) demandCleansingBatchContext
                                        .getOriginalCleansedUnitsMap().get(productNodeId).get(entry.getKey());
                                if (originalCleansedUnits != null) {
                                    originalHistory.setHistoryValues(originalCleansedUnits.getHistoryValues());
                                    originalHistory.zeroFill();
                                }
                            }
```

THERE ARE SOME THINGS I MISSED  - accidentally modified wrong listener method. - Changed wrong DTO, need to add to `DemandCleansingPolicyFactorsDTO` - Need to modify the following : - so I actually didn’t need to do much here, I just need to edit the `demandCleansingPolicyMapService.triggerDemandCleansing(context, demandCleansingPolicyId);` that is called here

```
java
  public void triggerDemandCleansing(Context context, String demandCleansingPolicyId)
    {
        DemandCleansingPolicy cleansingPolicy = demandCleansingPolicyService.checkDemandCleansingPolicyExistByDemandCleansingPolicyId(
                context, demandCleansingPolicyId);
        cleansingPolicy = setLocationsInDemandCleansingPolicy(context, cleansingPolicy);
				 //change it using this
				 cleansingPolicy = setDemandCleansingPolicyFactors(context,cleansingPolicy);
	        
	        itemInteractionService.exportItemsForDemandCleansing(cleansingPolicy);
    }
```

```

`setDemandCleansingPolicyFactors(context,cleansingPolicy,demandCleansingPolicyId);`

```
java
 private DemandCleansingPolicy setDemandCleansingPolicyFactors(Context context, DemandCleansingPolicy dCPolicy)
    {
        DemandCleansingPolicyFactorsDTO demandCleansingPolicyFactorsDTO;
        String demandCleansingPolicyFactors = dCPolicy.getDemandCleansingPolicyFactors();

        logger.debug("--setDemandCleansingPolicyFactors() -> Existing DemandCleansingPolicyFactors : {}",
                demandCleansingPolicyFactors);

        if (StringUtils.isEmpty(demandCleansingPolicyFactors))
        {
            demandCleansingPolicyFactorsDTO = new DemandCleansingPolicyFactorsDTO();
        }
        else
        {
            try
            {
                demandCleansingPolicyFactorsDTO = objectMapper.readValue(demandCleansingPolicyFactors,
                        new TypeReference<>()
                        {
                        });
            }
            catch (JsonProcessingException e)
            {
                logger.warn("--setDemandCleansingPolicyFactors() -> Issue parsing DemandCleansingPolicyFactors : {}",
                        demandCleansingPolicyFactors);
                demandCleansingPolicyFactorsDTO = new DemandCleansingPolicyFactorsDTO();
            }

        }

        boolean classificationStatus = demandCleansingHelper.getClassificationOnlyFromDemandCleansingPolicyFactors(dCPolicy);
        demandCleansingPolicyFactorsDTO.setIsClassificationOnly(classificationStatus);

        try{
            demandCleansingPolicyFactors = objectMapper.writeValueAsString(demandCleansingPolicyFactorsDTO);
        }
        catch(JsonProcessingException e){
            logger.warn("--setDemandCleansingPolicyFactors() -> Issue converting DemandCleansingPolicyFactorsDTO to string : {}", demandCleansingPolicyFactorsDTO);
        }
        logger.debug("--setDemandCleansingPolicyFactors() -> demandCleansingPolicyFactors(After reset) : {}", demandCleansingPolicyFactors);
        Boolean isClassification ;

        DemandCleansingPolicy updatedDemandCleansingPolicy = dCPolicy;

        if (StringUtils.isEmpty(dCPolicy.getDemandCleansingPolicyFactors()) || !dCPolicy.getDemandCleansingPolicyFactors().equals(demandCleansingPolicyFactors))
        {
            dCPolicy.setDemandCleansingPolicyFactors(demandCleansingPolicyFactors);
            updatedDemandCleansingPolicy = demandCleansingPolicyService.save(context, dCPolicy);
        }
        return updatedDemandCleansingPolicy;
    }
}
```

- [`DemandCleansingServiceImpl.Java`](http://DemandCleansingServiceImpl.Java) changes - Line 141

```
java
Boolean isClassificationOnly = demandCleansingHelper.getIsClassificationOnlyFromDemandCleansingPolicyFactors(cleansingPolicy);
```

- ~~so would I add a method to retrive that boolean in the DCP serviceimpl?~~ - ~~since there is no method or could I add it in the request DTO just like there is a getItemDTOs method in the request dto~~ - ~~like I did here:~~ ### **4. Extend the `DemandCleansingRequestDTO`** - Add a new field (`Boolean isClassificationOnly`) to this DTO. - make sure your getter and setter methods are added and appropriately used in all relevant classes.

```
java
        Private Boolean isClassificationOnly
        
        public Boolean isClassificationOnly()
            {
                return isClassificationOnly;
            }
        
            public void setisClassificationOnly(Boolean isClassificationOnly)
            {
                this.isClassificationOnly = isClassificationOnly;
            }
```

No so what I actually need to do is create a method in the ***HELPER CLASS!!*** - `demandCleansingHelper.java`

```
java
 public boolean getIsClassificationOnlyFromDemandCleansingPolicyFactors(DemandCleansingPolicy demandCleansingPolicy)
    {
        String demandCleansingPolicyFactor = demandCleansingPolicy.getDemandCleansingPolicyFactors();
            logger.debug(() -> MessageFormat.format("-- getIsClassificationOnlyFromDemandCleansingPolicyFactors() -> DemandCleansingPolicyFactor : {0} for DemandCleansingPolicy {1}",
                    demandCleansingPolicyFactor, demandCleansingPolicy.getDemandCleansingPolicyId()));
            Boolean isClassificationOnly;
                try {
                    DemandCleansingPolicyFactorsDTO demandCleansingPolicyFactorDTO = objectMapper.readValue(demandCleansingPolicyFactor,
                            new TypeReference<>() {
                            });
                    isClassificationOnly = demandCleansingPolicyFactorDTO.getIsClassificationOnly();
                } catch (Exception e) {
                    logger.error("--getIsClassificationOnlyFromDemandCleansingPolicyFactors() -> Issue parsing demandCleansingPolicyFactor : {}", demandCleansingPolicyFactor);
                    String messageString = MessageFormat.format("Demand Cleansing Policy Factors not setup correctly for DemandCleansingPolicyId : {0}", demandCleansingPolicy.getDemandCleansingPolicyId());
                    Message message = new Message(MessageType.ERROR, "ERROR", messageString);
                    List<Message> messageList = new ArrayList<>();
                    messageList.add(message);
                    throw ManhRuntimeExceptionUtil.getRuntimeException(ExceptionReason.BAD_DATA, e, e.getMessage(), false);
                }

        logger.debug("--getIsClassificationOnlyFromDemandCleansingPolicyFactors() -> isClassificationOnly: {}", isClassificationOnly);
        return isClassificationOnly;
    }
```

- `DemandCleansingPolicyFactorsDTO` changes

```
java
public class DemandCleansingPolicyFactorsDTO
{
    private String locations;
    private Boolean isClassificationOnly
    
    
    public Boolean getIsClassificationOnly()
    {
        return isClassificationOnly;
    }

    public void setIsClassificationOnly(Boolean isClassificationOnly)
    {
        this.isClassificationOnly = isClassificationOnly;
    }

    @JsonProperty(value = "Locations")
    public String getLocations()
    {
        return locations;
    }

    public void setLocations(String locations)
    {
        this.locations = locations;
    }

    @Override
    public String toString() {
        return "DemandCleansingPolicyFactorsDTO{" +
                "Locations=" + locations +
                '}';
    }
}
```

Last Change: - `DemandCleansingAdapter.Java` changes - Line 103

```
java
batchContext.setDemandClassificationOnly(demandCleansingHelper.getClassificationOnlyFromDemandCleansingPolicyFactors(demandCleansingPolicy));
```

- create transient field, demandCleansingPolicyFactorsDTO - that would go in the DCP Policy Entity - and then I would set it in the DCP POLICY ENTITY --- ### **Implementation Steps** 1. **Add Transient Field to the `DemandCleansingPolicy` Entity:** - Add a transient field `demandCleansingPolicyFactorsDTO` to avoid persisting it in the database.

```
java
import javax.persistence.Transient;

@Entity
public class DemandCleansingPolicy {
    // Existing fields...

    @Transient
    private DemandCleansingPolicyFactorsDTO demandCleansingPolicyFactorsDTO;

    // Getter and Setter
    public DemandCleansingPolicyFactorsDTO getDemandCleansingPolicyFactorsDTO() {
        return demandCleansingPolicyFactorsDTO;
    }

    public void setDemandCleansingPolicyFactorsDTO(DemandCleansingPolicyFactorsDTO demandCleansingPolicyFactorsDTO) {
        this.demandCleansingPolicyFactorsDTO = demandCleansingPolicyFactorsDTO;
    }
}
```

1. **Set `demandCleansingPolicyFactorsDTO` in the Entity:** - When retrieving or updating the `DemandCleansingPolicy`, populate this field with parsed data from `demandCleansingPolicyFactors`.

```
java
public DemandCleansingPolicy setDemandCleansingPolicyFactors(Context context, DemandCleansingPolicy demandCleansingPolicy) {
    String factorsJson = demandCleansingPolicy.getDemandCleansingPolicyFactors();
    DemandCleansingPolicyFactorsDTO factorsDTO;

    if (StringUtils.isNotBlank(factorsJson)) {
        try {
            factorsDTO = objectMapper.readValue(factorsJson, DemandCleansingPolicyFactorsDTO.class);
        } catch (JsonProcessingException e) {
            logger.error("Error parsing demandCleansingPolicyFactors JSON for policyId: {}", demandCleansingPolicy.getDemandCleansingPolicyId(), e);
            factorsDTO = new DemandCleansingPolicyFactorsDTO(); // Fallback to default
        }
    } else {
        factorsDTO = new DemandCleansingPolicyFactorsDTO(); // Default empty DTO
    }

    // Set the transient field
    demandCleansingPolicy.setDemandCleansingPolicyFactorsDTO(factorsDTO);

    return demandCleansingPolicy;
}
```

1. **Update Service or Repository Logic:** - Ensure that this method is called wherever `DemandCleansingPolicy` is fetched or updated, particularly in `triggerDemandCleansing` or similar methods.

```
java
public void triggerDemandCleansing(Context context, String demandCleansingPolicyId) {
    DemandCleansingPolicy policy = demandCleansingPolicyService.checkDemandCleansingPolicyExistByDemandCleansingPolicyId(context, demandCleansingPolicyId);

    // Set the factors DTO before further processing
    policy = setDemandCleansingPolicyFactors(context, policy);

    itemInteractionService.exportItemsForDemandCleansing(policy);
}
```

1. **Access `demandCleansingPolicyFactorsDTO` in Logic:** - Use the transient field directly in your downstream logic without repeatedly parsing it.

```
java
public boolean isClassificationOnly(DemandCleansingPolicy demandCleansingPolicy) {
    DemandCleansingPolicyFactorsDTO factorsDTO = demandCleansingPolicy.getDemandCleansingPolicyFactorsDTO();
    return factorsDTO != null && Boolean.TRUE.equals(factorsDTO.getIsClassificationOnly());
}
```

**Unit Tests:** - Test `setDemandCleansingPolicyFactors` to ensure it correctly populates the transient field from valid and invalid JSON. 2.
 **Integration Tests:** - Confirm that the `isClassificationOnly` flag is respected in the overall workflow after populating the transient field. ---