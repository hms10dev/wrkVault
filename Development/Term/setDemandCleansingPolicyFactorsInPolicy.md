```java
public DemandCleansingPolicy setDemandCleansingPolicyFactorsInPolicy(Context context,  
        DemandCleansingPolicy demandCleansingPolicy){  
    DemandCleansingPolicyFactorsDTO demandCleansingPolicyFactorsDTO;  
    if (demandCleansingPolicy == null) {  
        throw new IllegalArgumentException("DemandCleansingPolicy cannot be null");  
    }  
    String demandCleansingPolicyFactors = demandCleansingPolicy.getDemandCleansingPolicyFactors();  
            logger.debug("--setDemandCleansingPolicyFactorsInPolicy() -> Existing DemandCleansingPolicyFactors : {}",  
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
            logger.warn(  
                    "--setDemandCleansingPolicyFactorsInPolicy() -> Issue parsing demandCleansingPolicyFactors : {}",  
                    demandCleansingPolicyFactors);  
            demandCleansingPolicyFactorsDTO = new DemandCleansingPolicyFactorsDTO();  
        }  
    }  
    List<String> locationIds = demandCleansingHelper.getLocationIdsForDemandCleansingPolicy(demandCleansingPolicy);  
    String locations = String.join(", ", locationIds);  
    demandCleansingPolicyFactorsDTO.setLocations(locations);  
    demandCleansingPolicyFactorsDTO.setIsClassificationOnly(demandCleansingPolicy.parseDemandCleansingPolicyFactors().getIsClassificationOnly());  
    try  
    {  
        demandCleansingPolicyFactors = objectMapper.writeValueAsString(demandCleansingPolicyFactorsDTO);  
    }  
    catch (JsonProcessingException e)  
    {  
        logger.warn(  
                "--setDemandCleansingPolicyFactorsInPolicy() -> Issue converting DemandCleansingPolicyFactorsDTO to string : {}",  
                demandCleansingPolicyFactorsDTO);  
    }  
            logger.debug("--setDemandCleansingPolicyFactorsInPolicy() -> DemandCleansingPolicyFactors(After reset) : {}",  
                    demandCleansingPolicyFactors);  
    DemandCleansingPolicy modifiedDemandCleansingPolicy = demandCleansingPolicy;  
    if (StringUtils.isEmpty(  
            demandCleansingPolicy.getDemandCleansingPolicyFactors()) || !demandCleansingPolicy.getDemandCleansingPolicyFactors()  
            .equals(demandCleansingPolicyFactors))  
    {  
        demandCleansingPolicy.setDemandCleansingPolicyFactors(demandCleansingPolicyFactors);  
        modifiedDemandCleansingPolicy = demandCleansingPolicyService.save(context, demandCleansingPolicy);  
    }  
    modifiedDemandCleansingPolicy.setDemandCleansingPolicyFactorsDTO(demandCleansingPolicyFactorsDTO);  
    logger.debug("DTO after populated: {}", demandCleansingPolicyFactorsDTO);  
    return modifiedDemandCleansingPolicy;  
}
```


## Tests
```java
@Test  
public void testSetDemandCleansingPolicyFactorsInPolicyWhenDemandCleansingPolicyIsNull() {  
    assertThrows(IllegalArgumentException.class, () -> {  
        demandCleansingPolicyMapService.setDemandCleansingPolicyFactorsInPolicy(context,null);  
    });  
}  
  
@Test  
public void testShouldInitializeFactorsDTOWhenPolicyFactorsAreEmpty() {  
    DemandCleansingPolicy policy = mock(DemandCleansingPolicy.class);  
    when(policy.getDemandCleansingPolicyFactors()).thenReturn(null);  
  
    DemandCleansingPolicy result = demandCleansingPolicyMapService.setDemandCleansingPolicyFactorsInPolicy(context,policy);  
  
  
    assertNotNull(result.getDemandCleansingPolicyFactorsDTO());  
}
```



![[Screenshot 2024-12-27 at 2.03.59 PM.png]]