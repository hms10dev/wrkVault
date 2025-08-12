## ForecastHistoryFactors Data Structure

**Glossary:**

- **DTO (Data Transfer Object):** A class that encapsulates data for transfer between different layers of an application.
- **JSON (JavaScript Object Notation):** A lightweight data interchange format used for exchanging data between applications.
- **Reflection:** The ability of a program to examine or modify its own structure and behavior at runtime.
- **ObjectMapper:** A library used to convert between Java objects and JSON data.
- **CLOB:** Character Large Object, a data type for storing large textual data in a database.

**Current Format:**

The `ForecastHistoryFactors` data is currently stored in a nested array structure:

```
ForecasthistoryFactors
{ 
  [
    [
      "Seasonal Index" = 0.0,
      "Period start date" = 0.0,
      "Trend" = 0.0
    ],
    [
      "Seasonal Index" = 0.0,
      "Period start date" = 0.0,
      "Trend" = 0.0
    ],
    [
      "Seasonal Index" = 0.0,
      "Period start date" = 0.0,
      "Trend" = 0.0
    ]
  ]
}
```

**Issues:**

- Field names are strings instead of constants.
- Data types are not explicitly defined.
- The structure can become very large due to the nested arrays and potential future growth.

**Proposed Solution:**

1. **CompactForecastHistoryFactors DTO:**
    - Create a new DTO class named `CompactForecastHistoryFactors`.
    - Define fields with clear names (e.g., `forecast`, `qValue`, `iat`, etc.) and appropriate data types (e.g., `double`, `String`).
```Java
public class CompactForecastHistoryFactors {

  private ArrayList<String> columns;
  private ArrayList<ArrayList<Object>> data;

  // Getters and setters (can be generated using reflection)
  public ArrayList<String> getColumns() {
    return columns;
  }

  public void setColumns(ArrayList<String> columns) {
    this.columns = columns;
  }

  public ArrayList<ArrayList<Object>> getData() {
    return data;
  }

  public void setData(ArrayList<ArrayList<Object>> data) {
    this.data = data;
  }
}

```
1. **JSON Conversion:**
    - Use ObjectMapper to convert between the current `ForecastHistoryFactors` format and the new `CompactForecastHistoryFactors` DTO format.
    - Leverage reflection to automatically generate getters and setters for both DTOs.
2. **Static Columns List:**
    - Define a static list of column names in the `ForecastHistory` entity class.
    - Use this list for consistency when accessing and setting data in both formats.

**Benefits:**

- Improved readability and maintainability.
- Reduced data size and storage requirements.
- Easier data manipulation and transformation.

**New Structure:**
```JSON
{
  "Columns": [
    "Forecast",
    "QValue",
    "IAT",
    "HitTracker",
    "...."  // Add more column names as needed
  ],
  "Data": [
    [
      43.6459,  // This would be passed into setForecast()
      9.3987,
      10,
      "11100011",
      ....      // Add more data values corresponding to columns
    ],
    [
      43.6459,  // This would be passed into setForecast()
      9.3987,
      10,
      "11100011",
      ....      // Add more data values corresponding to columns
    ]
  ]
}

```
- This JSON object has two main properties:
	- `"Columns"`: An array of strings representing the names of all data points. The order of elements in this array is crucial.
	- `"Data"`: An array of arrays containing the actual data values. Each inner array represents a single data point, with the order of elements corresponding to the column names in the `"Columns"` array.

**Next Steps:**

- Implement the `CompactForecastHistoryFactors` DTO class.
- Write code to parse the current format to the new format and vice versa using ObjectMapper and reflection.
- Define the static column list in the `ForecastHistory` entity class.

** Hawa's Additional Notes:**

- Organize these notes in a knowledge management tool like Obsidian for future reference.

**Remember:**

- Refine these notes iteratively by reviewing code and notes to ensure clarity and stuff.


**CompactForecastHistoryFactorsDTO.java**

```java
package com.manh.cp.ai.forecast.forecast.dto;  
  
import com.fasterxml.jackson.annotation.JsonProperty;  
  
import java.time.LocalDate;  
import java.util.ArrayList;  
  
public class CompactForecastHistoryFactorsDTO  
{  
    private ArrayList<String> columns;  
    private ArrayList<ArrayList<Object>> data;  
    private Double seasonalIndex;  
    private LocalDate periodStartDate;  
    private Double forecast;  
    private Double adjustedCleansedDemand;  
    private Double demandFrequency;  
    private String seasonalProfile;  
    private Double trend;  
    private Double variance;  
    private Double trackingSignal;  
    private Double qVariance;  
    private Double seasonalKappa;  
    private Double qTrackingSignal;  
    private Double qKappa;  
    private Integer weekOfYear;  
  
  
    public ArrayList<String> getColumns() {  
        return columns;  
    }  
  
    public void setColumns(ArrayList<String> columns) {  
        this.columns = columns;  
    }  
  
    public ArrayList<ArrayList<Object>> getData() {  
        return data;  
    }  
  
    public void setData(ArrayList<ArrayList<Object>> data) {  
        this.data = data;  
    }  
  
    @JsonProperty(value = "PeriodStartDate")  
    public LocalDate getPeriodStartDate()  
    {  
        return periodStartDate;  
    }  
    public void setPeriodStartDate(LocalDate periodStartDate)  
    {  
        this.periodStartDate = periodStartDate;  
    }  
    @JsonProperty(value = "SeasonalIndex")  
    public Double getSeasonalIndex()  
    {  
        return seasonalIndex;  
    }  
    public void setSeasonalIndex(Double seasonalIndex)  
    {  
        this.seasonalIndex = seasonalIndex;  
    }  
    @JsonProperty(value = "Forecast")  
    public Double getForecast()  
    {  
        return forecast;  
    }  
    public void setForecast(Double forecast)  
    {  
        this.forecast = forecast;  
    }  
    @JsonProperty(value = "AdjustedCleansedDemand")  
    public Double getAdjustedCleansedDemand()  
    {  
        return adjustedCleansedDemand;  
    }  
    public void setAdjustedCleansedDemand(Double adjustedCleansedDemand)  
    {  
        this.adjustedCleansedDemand = adjustedCleansedDemand;  
    }  
    @JsonProperty(value = "DemandFrequency")  
    public Double getDemandFrequency()  
    {  
        return demandFrequency;  
    }  
    public void setDemandFrequency(Double demandFrequency)  
    {  
        this.demandFrequency = demandFrequency;  
    }  
    @JsonProperty(value = "SeasonalProfile")  
    public String getSeasonalProfile() {  
        return seasonalProfile;  
    }  
    public void setSeasonalProfile(String seasonalProfile) {  
        this.seasonalProfile = seasonalProfile;  
    }  
    public Double getTrend() {  
        return trend;  
    }  
    public void setTrend(Double trend) {  
        this.trend = trend;  
    }  
    @JsonProperty(value = "Variance")  
    public Double getVariance() {  
        return variance;  
    }  
    public void setVariance(Double Variance) {  
        this.variance = Variance;  
    }  
    @JsonProperty(value = "TrackingSignal")  
    public Double getTrackingSignal() {  
        return trackingSignal;  
    }  
    public void setTrackingSignal(Double trackingSignal) {  
        this.trackingSignal = trackingSignal;  
    }  
    @JsonProperty(value = "QVariance")  
    public Double getQVariance() {  
        return qVariance;  
    }  
    public void setQVariance(Double qVariance) {  
        this.qVariance = qVariance;  
    }  
    @JsonProperty(value = "SeasonalKappa")  
    public Double getSeasonalKappa() {  
        return seasonalKappa;  
    }  
    public void setSeasonalKappa(Double seasonalKappa) {  
        this.seasonalKappa = seasonalKappa;  
    }  
    @JsonProperty(value = "QTrackingSignal")  
    public Double getQTrackingSignal() {  
        return qTrackingSignal;  
    }  
    public void setQTrackingSignal(Double qTrackingSignal) {  
        this.qTrackingSignal = qTrackingSignal;  
    }  
    @JsonProperty(value = "QKappa")  
    public Double getQKappa() {  
        return qKappa;  
    }  
    public void setQKappa(Double qKappa) {  
        this.qKappa = qKappa;  
    }  
    @JsonProperty(value = "WeekOfYear")  
    public Integer getWeekOfYear() {  
        return weekOfYear;  
    }  
    public void setWeekOfYear(Integer weekOfYear) {  
        this.weekOfYear = weekOfYear;  
    }  
    @Override  
    public String toString() {  
        return "ForecastHistoryFactorsDTO{" +  
                "seasonalIndex=" + seasonalIndex +  
                ", periodStartDate=" + periodStartDate +  
                ", forecast=" + forecast +  
                ", adjustedCleansedDemand=" + adjustedCleansedDemand +  
                ", demandFrequency=" + demandFrequency +  
                ", seasonalProfile=" + seasonalProfile +  
                ", trend=" + trend +  
                ", variance=" + variance +  
                ", trackingSignal=" + trackingSignal +  
                ", qVariance=" + qVariance +  
                ", qTrackingSignal=" + qTrackingSignal +  
                ", qKappa=" + qKappa +  
                ", seasonalKappa=" + seasonalKappa +  
                ", weekOfYear=" + weekOfYear +  
                '}';  
}}

```

**ForecastConstants.java

```java
/*  
 * Copyright &#169; 2022 Manhattan Associates, Inc. All Rights Reserved. * * Confidential, Proprietary and Trade Secrets Notice * * Use of this software is governed by a license agreement. This software * contains confidential, proprietary and trade secret information of * Manhattan Associates, Inc. and is protected under United States and * international copyright and other intellectual property laws. Use, disclosure, * reproduction, modification, distribution, or storage in a retrieval system in * any form or by any means is prohibited without the prior express written * permission of Manhattan Associates, Inc. * * Manhattan Associates, Inc. * 2300 Windy Ridge Parkway, 10th Floor * Atlanta, GA 30339 USA */package com.manh.cp.ai.forecast.common;  
  
public enum ForecastConstants  
{  
    FIELD_NAME("FieldName"),  
    ITEM_ID("ItemId"),  
    ITEM_IDS("ItemIds"),  
    LOCATION_ID("LocationId"),  
    LOCATION_IDS("LocationIds"),  
    ITEM_KEY("ItemKey"),  
    LOCATION_KEY("LocationKey"),  
    FORECAST_POLICY_ID("ForecastPolicyId"),  
    FORECAST_PURPOSE_ID("ForecastPurposeId"),  
    FILTER_EXPRESSIONS("FilterExpressions"),  
    MAX_LIMIT("MaxLimit"),  
    EVENT_REFERENCE_ID("EventReferenceId"),  
    JOB_TYPE_ID("ForecastInitialize"),  
    DEMAND_CLEANSING_JOB_TYPE_ID("DemandCleansing"),  
    DEMAND_CLEANSING_POLICY_ID("DemandCleansingPolicyId"),  
  
    SEASONAL_PROFILING_JOB_TYPE_ID("SeasonalProfiling"),  
    SEASONAL_PROFILE_POLICY_ID("SeasonalProfilePolicyId"),  
  
    DEMAND_SMOOTHING_PERIOD_TYPE_NO_SMOOTHING("NO_SMOOTHING"),  
    DEMAND_SMOOTHING_PERIOD_TYPE_3_PERIOD_SMOOTHING("3_PERIOD_SMOOTHING"),  
    DEMAND_SMOOTHING_PERIOD_TYPE_5_PERIOD_SMOOTHING("5_PERIOD_SMOOTHING"),  
  
    FORECAST_ID("ForecastId"),  
    // Forecast Assignment Policy Rules Constant  
    ANNUAL_DEMAND_FORECAST("annualDemandForecast"),  
    CURRENT_FORECAST("currentForecast"),  
    STANDARD_DEVIATION_UNITS("standardDeviationUnits"),  
    SEASONAL_INDEX("seasonalIndex"),  
    ITEM_LOCATION_GROUP_IDS("itemLocationGroupIds"),  
    ITEM_LOCATION_GROUP_ID("ItemLocationGroupId"),  
    ITEM_LOCATION_GROUP("itemLocationGroup"),  
    ITEM_LOCATION("itemLocation"),  
    LIFE_CYCLE_STATUS("lifeCycleStatus"),  
    VELOCITY_CODE("velocityCode"),  
    PURCHASE_PRICE("purchasePrice"),  
    DEFAULT_ITEM_LOCATION_FACTOR_TEMPLATE("DefaultItemLocationFactorTemplate"),  
    REPLENISHMENT("Replenishment"),  
    ENTITY_TYPE("EntityType"),  
    ENTITY_TYPE_ITEM("Item"),  
    ENTITY_TYPE_LOCATION("Location"),  
    FILTER_ATTRIBUTE("FilterAttribute"),  
    FILTER_VALUE("FilterValue"),  
    FILTER_CONDITION_ID("FilterConditionId"),  
    FORECAST_POLICY("forecastPolicy"),  
    SEASONAL_PROFILE_POLICY("seasonalProfilePolicy"),  
    POLICY_NAME("PolicyName"),  
    FORECAST_NOTIFICATION_TEMPLATE("ForecastNotificationTemplate"),  
    PERIOD_START_DATE("periodStartDate"),  
    FORECAST("forecast"),  
    ADJUSTED_CLEANSED_DEMAND("adjustedCleansedDemand"),  
    DEMAND_FREQUENCY("DemandFrequency"),  
    SEASONAL_PROFILE("SeasonalProfile"),  
    TREND("trend"),  
    VARIANCE("Variance"),  
    TRACKING_SIGNAL("TrackingSignal"),  
    Q_VARIANCE("qVariance"),  
    Q_TRACKING_SIGNAL("qTrackingSignal"),  
    Q_KAPPA ("qKappa"),  
    SEASONAL_KAPPA("seasonalKappa"),  
    WEEK_OF_YEAR ("weekOfYear");  
  
    private final String value;  
  
    ForecastConstants(final String value)  
    {  
        this.value = value;  
    }  
  
    public String getValue()  
    {  
        return value;  
    }  
}
```