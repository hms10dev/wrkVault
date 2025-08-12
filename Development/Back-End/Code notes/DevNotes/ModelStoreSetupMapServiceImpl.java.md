# Notes for this class:

## Initial Code Coverage: 90%

## Uncovered Code Lines: 3

## Uncovered Conditions: 3


- Need to cover a null condition for the criteria Query
	- lines 74-77
- Need to cover the Exception catching that returns the logger error 
	- lines 122-125
	 ```java
	catch (Exception ex)
        {
        logger.error("Error Occured while framing criteriaQuery {0}",ex.getMessage());
		criteriaQuery.setQuery(incomingQuery);
 }
```


## Example test to check if exception was thrown:

#### ai-forecast component:
src/test/java/com/manh/cp/ai/policy/impl/service/ForecastPolicyMapServiceImplTest.java

``` java
@Test  
public void testProcessForecastInitNull()  
{  
    ForecastPolicy policy = getForecastPolicy(TEST_POLICY_ID);  
    Mockito.when(forecastPolicyService.findByForecastPolicyId(context, TEST_POLICY_ID)).thenReturn(null);  
    boolean exceptionThrown = true;  
    try    {  
        forecastPolicyMapService.processForecastInitialization(context, policy.getForecastPolicyId());  
    }  
    catch (ManhRuntimeException e)  
    {  
        exceptionThrown = true;  
        assertEquals(1, e.getMessages().size());  
    }  
    assertTrue(exceptionThrown);  
  
}
```
