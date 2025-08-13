//AI-21511  

@Test  
public void testDemandCleansingClassificationOnlyWorkflow() {  
    // make a mock event and policy  
    Document demandCleansingPolicy = createDemandCleansingPolicy("DemandCleansingPolicy-1");  
    demandCleansingPolicy.put(DemandCleansingPolicyBaseDTO.Fields.DMND_CLEANSING_POLICY_FACTORS.getCode(), "{\"Locations\":\"Location1\",\"isClassificationOnly\":true}");  
  
    demandCleansingPolicyMapServiceImpl.saveDemandCleansingPolicy(context, demandCleansingPolicy, null, null);  
    commitTransaction();  
  
    // sim listener processing triggerDemandCleansing event  
  
    demandCleansingListener.triggerDemandCleansing(context, demandCleansingPolicy);  
  
    //Validate that the policy DTO is populated  
    DemandCleansingPolicy policy = demandCleansingPolicyService.checkDemandCleansingPolicyExistByDemandCleansingPolicyId(context,"DemandCleansingPolicy-1");  
    Assert.assertNotNull(policy);  
  
    String policyFactors = policy.getDemandCleansingPolicyFactors();  
    Assert.assertNotNull(policyFactors);  
    Assert.assertEquals("{\"isClassificationOnly\":true,\"Locations\":\"Location1\"}", policyFactors);  
  
    //    Assert.assertEquals("{\"Locations\":\"Location1\",\"isClassificationOnly\":true}", policyFactors);  
  
    DemandCleansingPolicyFactorsDTO factorsDTO = policy.getDemandCleansingPolicyFactorsDTO();  
    Assert.assertNotNull(factorsDTO);  
    Assert.assertTrue(factorsDTO.getIsClassificationOnly());  
}  
  
    @Test  
    public void testDemandCleansingClassificationOnlyWorkflow(){  
        // make a mock event and policy  
        Document demandCleansingPolicy=createDemandCleansingPolicy("DemandCleansingPolicy-1");  
        demandCleansingPolicy.put(DemandCleansingPolicyBaseDTO.Fields.DMND_CLEANSING_POLICY_FACTORS.getCode(), "{\"Locations\":\"Location1\",\"isClassificationOnly\":true}");  
  
        demandCleansingPolicyMapServiceImpl.  
                saveDemandCleansingPolicy(context,demandCleansingPolicy,null,null);  
        commitTransaction();  
  
        DemandCleansingRequestDTO demandCleansingRequestDTO = new DemandCleansingRequestDTO();  
        demandCleansingRequestDTO.setDemandCleansingPolicyId("DemandCleansingPolicy-1");  
        demandCleansingRequestDTO.setItemDTOs(Collections.singletonList(getItemDTO()));  
        demandCleansingService.cleanseDemand(context,demandCleansingRequestDTO);  
        commitTransaction();  
        DemandCleansingResult dcResult=demandCleansingResultService.findByDemandCleansingPolicyAndItemAndLocation(context,demandCleansingRequestDTO.getDemandCleansingPolicyId(),TEST_ITEM,TEST_LOCATION);  
        Assert.assertTrue(dcResult.getRegular());  
        Assert.assertTrue(dcResult.getFastMover());  
        Assert.assertFalse(dcResult.getIntermittent());  
        Assert.assertFalse(dcResult.getSlowMover());  
        Assert.assertFalse(dcResult.getNewIndicator());  
        Assert.assertFalse(dcResult.getInactive());  
        Assert.assertEquals(Long.valueOf(28),dcResult.getUpperOutliers());  
        Assert.assertEquals(Long.valueOf(28),dcResult.getUpperSpikes());  
        Assert.assertEquals(Long.valueOf(0),dcResult.getLowerOutliers());  
        Assert.assertEquals(Long.valueOf(0),dcResult.getLowerSpikes());  
        Assert.assertEquals(Double.valueOf(61.9583),dcResult.getMeanDemand());  
        Assert.assertEquals(Double.valueOf(30.3198),dcResult.getStandardDeviation());  
  
        DemandCleansingPolicy demandCleansingResultEntity = dcResult.getDemandCleansingPolicyEntity();  
        //so its setting the factors in the string, but the DTO remains null. I need to figure that out .  
        String policyFactors = demandCleansingResultEntity.getDemandCleansingPolicyFactors();  
        Assert.assertNotNull(policyFactors);  
        Assert.assertEquals("{\"Locations\":\"Location1\",\"isClassificationOnly\":true}", policyFactors);  
  
        DemandCleansingPolicyFactorsDTO factorsDTO = demandCleansingResultEntity.getDemandCleansingPolicyFactorsDTO();  
        Assert.assertNotNull(factorsDTO);  
        Assert.assertEquals(true, factorsDTO.getIsClassificationOnly());  
  
  
  
    }