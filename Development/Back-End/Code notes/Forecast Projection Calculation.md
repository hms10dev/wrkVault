# 🌱 Note: Forecast Projection Calculation Notes 
##  ⌚️ Date: Apr 5, 2024
##  🎫 Story Ticket: 

> [!info] Summary:
> > 
> > - [x] This method essentially calculates a forecast projection array based on the provided parameters and historical data. It considers factors such as seasonal effects, trends, and future forecast changes to generate the projection.
> > - [ ] simple
> > - [ ] task
> > - [ ] simple
> > 
> >
> > 


# Code 👩🏾‍💻
---
```java
@Component  
public class ForecastProjectionCalculator  
{  
    private static final Logger logger = CPLoggerFactory.getLogger(ForecastProjectionCalculator.class);  
  
    @Value("${forecastProjection.window:52}")  
    int forecastProjectionWindow = 52;  
      
    @Autowired  
    protected ManualForecastCalculator myManualForecastCalculator;  
  
    public double[] calculateForecastProjection(EngineForecastEntity fe, EngineTimePeriod currentWeekTimePeriod, EngineTimePeriod currentYearTimePeriod,  
                                  Map<LocalDate, List<EngineManualForecastEvent>> futureForecastChangesByPeriodStartDate,  
                                  Integer length){  
       if (length==null) length = forecastProjectionWindow;  
       double[] forecastProjection = new double[length];  
       LocalDate forecastProjectionStartDate = currentWeekTimePeriod.getStartDate();  
       boolean isUFM = fe.getForecastMethodType().getCode().equals(EnumeratedEntities.FORECAST_METHOD_TYPE_UNIFIED_FORECASTING_ID);  
  
       double level = (fe.getCurrentForecast().getEffectiveManualForecast()!=null ? fe.getCurrentForecast().getEffectiveManualForecast() : 0.0);  
       double qValue = Math.max(1.0, (isUFM && fe.getEffectiveQValue()!=null ? fe.getEffectiveQValue() : 1.0));        
       int p = fe.getNumHistoryPeriodsPerForecastPeriod();  
       double periodForecast = getPeriodForecast(level, qValue, p);  
         
       double annualGrowthRate = 0.0;  
       if (MathUtils.greaterThanZero(level) && fe.getManualTrend()!=null){  
          annualGrowthRate = fe.getManualTrend()/p * 52.0 / level;  
       }  
       double trendDampeningFactor = (!MathUtils.isZero(annualGrowthRate) ? ForecastConfigUtils.getTrendDampeningFactor() : 1.0);  
       int firstSPIndex = (fe.getSeasonalProfile() != null ? fe.getSeasonalProfile().getSeasonalityIndex(forecastProjectionStartDate, currentYearTimePeriod) : -1);  
         
       for(int i=0; i<forecastProjection.length; i++){  
          double si = 1.0;  
          if (fe.getSeasonalProfile() != null){  
             int currSPIndex = (firstSPIndex + i) % 52;  
             si = fe.getSeasonalProfile().getIndex(currSPIndex);  
          }       
          double seasonalPeriodForecast = periodForecast * si;  
            
          if (i==0){  
             forecastProjection[i] = (seasonalPeriodForecast/(double)p);  
          }  
          else{  
             // modify seasonal period forecast based on future events in future forecast periods  
             if (futureForecastChangesByPeriodStartDate!=null && !futureForecastChangesByPeriodStartDate.isEmpty()){      
                LocalDate weekStartDate = BusinessCalendarUtil.getDateOffset(forecastProjectionStartDate, 7*i);  
                List<EngineManualForecastEvent> mfeList = futureForecastChangesByPeriodStartDate.get(weekStartDate);  
                if (mfeList!=null && !mfeList.isEmpty()){          
                   seasonalPeriodForecast = myManualForecastCalculator.modifySeasonalPeriodForecast(fe,  
                         seasonalPeriodForecast, si, p, mfeList, currentWeekTimePeriod);  
                   if(!MathUtils.isZero(si)) {  
                      periodForecast = seasonalPeriodForecast / si;  
                   }  
                   else {  
                      periodForecast = seasonalPeriodForecast;  
                   }  
                }                      
             }  
               
             // trend is calculated weekly on the first day of the week, therefore the week-1 woudln't have any trend,   
             // week-2 would have 7 days of trend, week-3 would have 14 days of trend, and so on  
             forecastProjection[i] = Math.max(0, (seasonalPeriodForecast/(double)p) * ( 1.0 + annualGrowthRate * Math.pow(i/52.0, trendDampeningFactor)));  
          }  
       }    
       return forecastProjection;  
    }
```



# Breakdown 🤖
---

Sure, let's break down the given code into simpler steps:

1. **Method Signature and Parameters**:
   - The method `calculateForecastProjection` takes several parameters:
     - `fe`: An EngineForecastEntity object.
     - `currentWeekTimePeriod`: An EngineTimePeriod object representing the current week.
     - `currentYearTimePeriod`: An EngineTimePeriod object representing the current year.
     - `futureForecastChangesByPeriodStartDate`: A Map containing future forecast changes grouped by start date.
     - `length`: An Integer representing the length of the forecast projection.

2. **Setting Default Length**:
   - If the `length` parameter is null, it's set to a default value called `forecastProjectionWindow`.

3. **Initialization**:
   - An array `forecastProjection` of type `double` is initialized with the determined length.
   - The start date of the forecast projection is set to the start date of the current week.

4. **Calculation of Level and Q Value**:
   - The `level` is determined from the current forecast.
   - The `qValue` is determined based on whether the forecast method is a Unified Forecasting Method.

5. **Calculation of Period Forecast**:
   - The `periodForecast` is calculated based on the level, qValue, and the number of historical periods per forecast period.

6. **Calculation of Annual Growth Rate**:
   - If there's a manual trend and the level is greater than zero, the annual growth rate is calculated.

7. **Initialization of Trend Dampening Factor**:
   - The trend dampening factor is set based on whether the annual growth rate is not zero.

8. **Determination of Seasonal Profile Index**:
   - The seasonal profile index for the forecast start date is determined.

9. **Loop for Forecast Projection**:
   - A loop iterates over the forecast projection length.
   - For each iteration:
     - The seasonal index is calculated based on the seasonal profile.
     - The seasonal period forecast is calculated.
     - For the first iteration, the forecast projection is set based on the seasonal period forecast divided by the number of periods.
     - For subsequent iterations, the seasonal period forecast is modified based on future forecast events.
     - The forecast projection for the iteration is calculated considering the trend and seasonal effects.

10. **Return**:
    - The calculated forecast projection array is returned.

This method essentially calculates a forecast projection array based on the provided parameters and historical data. It considers factors such as seasonal effects, trends, and future forecast changes to generate the projection.

### Code Breakdown with snippets:
Sure, let's break down the `calculateForecastProjection` method step by step:

1. **Initialization:**
   - If the `length` parameter is `null`, it's set to a default value (`forecastProjectionWindow`).
   - Initialize an array `forecastProjection` of size `length` to store the forecasted values.
   - Determine the start date for the forecast projection.

   ```java
   if (length == null) {
       length = forecastProjectionWindow;
   }
   double[] forecastProjection = new double[length];
   LocalDate forecastProjectionStartDate = currentWeekTimePeriod.getStartDate();
   ```

2. **Calculation of Forecast Parameters:**
   - Calculate the level and Q value based on the forecast entity and its properties.
   - Determine the period forecast based on the level, Q value, and historical data.
   - Calculate the annual growth rate and trend dampening factor if applicable.

   ```java
   double level = (fe.getCurrentForecast().getEffectiveManualForecast() != null ? fe.getCurrentForecast().getEffectiveManualForecast() : 0.0);
   double qValue = Math.max(1.0, (isUFM && fe.getEffectiveQValue() != null ? fe.getEffectiveQValue() : 1.0));
   int p = fe.getNumHistoryPeriodsPerForecastPeriod();
   double periodForecast = getPeriodForecast(level, qValue, p);

   double annualGrowthRate = 0.0;
   if (MathUtils.greaterThanZero(level) && fe.getManualTrend() != null) {
       annualGrowthRate = fe.getManualTrend() / p * 52.0 / level;
   }
   double trendDampeningFactor = (!MathUtils.isZero(annualGrowthRate) ? ForecastConfigUtils.getTrendDampeningFactor() : 1.0);
   ```

3. **Seasonality Index Calculation:**
   - Determine the seasonality index for the forecast start date.
   - Adjust the seasonal period forecast based on the seasonality index.

   ```java
   int firstSPIndex = (fe.getSeasonalProfile() != null ? fe.getSeasonalProfile().getSeasonalityIndex(forecastProjectionStartDate, currentYearTimePeriod) : -1);

   for (int i = 0; i < forecastProjection.length; i++) {
       double si = 1.0;
       if (fe.getSeasonalProfile() != null) {
           int currSPIndex = (firstSPIndex + i) % 52;
           si = fe.getSeasonalProfile().getIndex(currSPIndex);
       }
       double seasonalPeriodForecast = periodForecast * si;
   }
   ```

4. **Forecast Projection Calculation:**
   - Iterate over each forecast period and calculate the forecasted value.
   - Adjust the forecast based on future events and trends.
   - Store the forecasted value in the `forecastProjection` array.

   ```java
   for (int i = 0; i < forecastProjection.length; i++) {
       // Calculate seasonal period forecast
       // Adjust seasonal period forecast based on future events
       // Calculate trend and adjust forecast
       forecastProjection[i] = /* Final calculated forecast value */;
   }
   ```

5. **Return:**
   - Return the `forecastProjection` array containing the forecasted values.

   ```java
   return forecastProjection;
   ```

This method takes various parameters related to the forecast entity and its context, calculates forecast parameters, adjusts for seasonality, incorporates future events, and calculates the final forecast projection for the specified length.


### What is the purpose?
Of course, let's simplify and explain the purpose of the `calculateForecastProjection` method and what each part does.

1. **Initialization:**
   - Sets up the initial conditions for the forecast calculation, like the length of the forecast projection and the start date.

2. **Calculation of Forecast Parameters:**
   - Determines key factors affecting the forecast, like the current level of demand, a multiplier for adjusting the forecast (Q value), and the historical pattern of demand over a certain period (period forecast). It also calculates the annual growth rate and adjusts for any manual trends provided.

3. **Seasonality Index Calculation:**
   - Considers the seasonal pattern in demand. It calculates a factor (seasonality index) representing how demand varies throughout the year. This is used to adjust the forecast based on the time of year.

4. **Forecast Projection Calculation:**
   - Predicts the demand for each future period based on the initial forecast parameters and any adjustments needed. It considers both the historical pattern and any anticipated changes due to future events. Additionally, it applies a trend factor to account for changes in demand over time.

5. **Return:**
   - Provides the forecasted demand values for the specified length of time.

In essence, this method takes in various inputs related to historical demand, current conditions, and potential future events, and then uses them to predict future demand over a specified time period. It considers factors like seasonality and trends to make the forecast as accurate as possible.
  

# Potential Questions:📝

---

1. How is the length of the forecast projection window determined if the `length` parameter is not provided?
	1. 
	
   
2. What does the `getPeriodForecast` function do, and how is it used in the context of the code?
	1. 
	 
  
3. How is the `annualGrowthRate` calculated, and under what conditions is it considered?
	1. 

	   
4. What is the significance of the `trendDampeningFactor`, and how is it determined?
	1. 

	   
5. How does the code handle seasonal variations in the forecast projection?
	1. 

	   
6. Can you explain the logic behind modifying the seasonal period forecast based on future events?
	1. 

	   
7. What is the role of the `myManualForecastCalculator.modifySeasonalPeriodForecast` method?
	1. 

	   
8. How is the trend factor incorporated into the forecast projection calculation?
	1. 

	   


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