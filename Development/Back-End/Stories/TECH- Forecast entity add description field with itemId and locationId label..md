# 🌱 Note: TECH- Forecast entity add description field with itemId and locationId label. 
##  ⌚️ Date: Aug 16, 2023
##  🎫 Story Ticket: https://manhattanassociates.atlassian.net/browse/AI-4921

> [!info] Acceptance Criteria:
> > 
> > 
> > - [ ] During ForecastInit, when a Forecast entity is created, then populate the description field with the itemId and locationId labels if present; 
> > - [ ] otherwise this field is null.
> > - [ ] task
> > - [ ] simple
> > 
> >
> > 


# To-do list 📝
---

- [ ] Add a “Description field” in the Forecast entity. When records are created in Forecast, populate it with **itemId +_+locationId. This field will be added only to show in UI**
- [ ] *Add a description field**
- [ ] Then use the helper class to adjust**
- [ ] Add field to entity xml**
- [ ] Populate field with data find where its getting fetched**
- [ ] Description** **itemid : locationid value**


# Jot down 📝 
---

## What do I need to mock in the createForecast Class?

#### Class :

```java
public Forecast createForecast(Context context, ForecastPolicy forecastPolicy, Map<String, Object> annotations)  
{  
    String forecastId = hashIdGenerator.generateId();  
    securityKeyHelper.validateAndSetSecurityKey(context, Forecast.ENTITY_NAME, null, null);  
    Forecast forecast = EntityFactory.getFactory().newEntity(ForecastEntity.class, new Forecast.Key(forecastId));  
  
    forecast.setForecastPolicy(new ForecastPolicy.Key(forecastPolicy.getForecastPolicyId()));  
  
    SmoothingPolicy.Key smoothingPolicy = forecastPolicy.getSmoothingPolicy();  
  
    forecast.setSmoothingPolicy(smoothingPolicy);  
  
    ForecastControlPolicy.Key forecastControlPolicy = forecastPolicy.getForecastControlPolicy();  
    forecast.setForecastControlPolicy(forecastControlPolicy);  
    ForecastHistoryUsedTypeBase.Key forecastHistoryUsedType = forecastPolicy.getForecastHistoryUsedType();  
    forecast.setForecastHistoryUsedType(forecastHistoryUsedType);  
    ForecastExceptionPolicy.Key forecastExceptionPolicy = forecastPolicy.getForecastExceptionPolicy();  
  
    forecast.setForecastExceptionPolicy(forecastExceptionPolicy);  
  
    Map<String, Object> entityLabels = new HashMap<>();  
    entityLabels.put(EntityLabelType.Annotations.name(), annotations);  
    forecast.setEntityLabels(entityLabels);  
  
    //creating the description  
    String itemId = (String) forecast.getAnnotations().get(ForecastConstants.ITEM_ID.getValue());  
    String locationId = (String) forecast.getAnnotations().get(ForecastConstants.LOCATION_ID.getValue());  
  
    String description = itemId.concat(" ").concat(locationId) ;  
    forecast.setDescription(description);  
  
    logger.debug("--createForecast() -> Description: {}", description);  
  
    forecast = forecastService.add(context, forecast);  
  
    logger.debug("--createForecast() -> Forecast: {}", forecast);  
    return forecast;  
}
```


#### Idears:

When writing unit tests for the given method `createForecast`, we want to mock the external dependencies and isolate the method under test
In this case, the method depends on the following external components:

1. `hashIdGenerator`: This is used to generate a forecastId. You should mock its behavior to return a predefined forecastId during testing.

2. `securityKeyHelper`: This is used to validate and set a security key. You might need to mock its behavior based on the test scenario, either to perform a successful validation or to simulate a failure.

3. `EntityFactory`: This is used to create a new `Forecast` entity. Mock its behavior to return a mock `Forecast` object.

4. `forecastService`: This is used to add the `Forecast` object to the service. You need to mock its behavior to handle the `forecastService.add` call.

5. Logging (`logger.debug`): You may want to mock the logging behavior or verify that the correct log messages are being generated.

6. `forecastPolicy`: This is an input parameter. You'll need to create a mock or stub object for this.

Here's a rough outline of how you might structure your unit test using a mocking framework like Mockito:

```java
import static org.mockito.Mockito.*;

@RunWith(MockitoJUnitRunner.class)
public class ForecastTest {

    @Mock
    private HashIdGenerator hashIdGenerator;
    
    @Mock
    private SecurityKeyHelper securityKeyHelper;
    
    @Mock
    private EntityFactory entityFactory;
    
    @Mock
    private ForecastService forecastService;
    
    @InjectMocks
    private ForecastProcessor forecastProcessor; // The class containing createForecast
    
    @Test
    public void testCreateForecast() {
        // Arrange
        Context context = new Context(); // Create a context object
        
        ForecastPolicy forecastPolicy = mock(ForecastPolicy.class); // Create a mock forecastPolicy
        
        Map<String, Object> annotations = new HashMap<>(); // Create annotations
        
        // Mock the behaviors
        when(hashIdGenerator.generateId()).thenReturn("mockedForecastId");
        // Mock other behaviors for securityKeyHelper, entityFactory, and forecastService
        
        // Act
        Forecast result = forecastProcessor.createForecast(context, forecastPolicy, annotations);
        
        // Assert
        // Verify the interactions, check values of result, etc.
    }
}
```

This is just a basic outline, and you'll need to adapt it to your specific testing framework and project setup. The idea is to use mocking to control the behavior of external dependencies and ensure that the method under test is being tested in isolation.
  


# Sub-pages 📑

---
- [[Sub Page]]
- [[Sub Page]]
- [[Sub Page]]
- [[Sub Page]]

# Reference links 🔗
---

[Beyond Frank Lloyd Wright: A Broader View of Art in Chicago](https://www.nytimes.com/2018/03/08/arts/chicago-museums-art.html?rref=collection%2Fsectioncollection%2Ftravel)

  
[Havana's Symphony of Sound](https://www.nytimes.com/2018/03/12/travel/havana-cuba.html?rref=collection%2Fsectioncollection%2Ftravel)