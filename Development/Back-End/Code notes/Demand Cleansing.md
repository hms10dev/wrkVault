# Demand Cleansing Explanations
## Related links (Confluence)
- https://manhattanassociates.atlassian.net/wiki/spaces/ASCP/pages/4320493604/Demand+Cleansing+Policy
- [[demandCleansing Process Flow.canvas|demandCleansing Process Flow]]

# Demand Cleansing:
## Demand Cleansing: A Culinary Analogy

Imagine you're a chef preparing a gourmet meal. The raw ingredients are your historical demand data. Before you can create a masterpiece, you need to ensure these ingredients are clean, fresh, and free from any impurities. This is where **demand cleansing** comes in.

**Demand cleansing** is the process of cleaning and preparing demand data to make it suitable for analysis and forecasting. It's like ensuring your ingredients are free from contaminants before cooking.

### Why is Demand Cleansing Important?

- **Data Quality:** Ensures that the data is accurate, consistent, and free from errors.
- **Forecast Accuracy:** Improves the accuracy of demand forecasts by providing a solid foundation.
- **Decision Making:** Supports better decision-making by providing reliable and trustworthy data.

### Common Cleansing Techniques

1. **Outlier Detection:** Identifies and removes data points that are significantly different from the rest of the data. This could be due to errors, anomalies, or special events.
2. **Missing Data Input:** Fills in missing data points with estimated values based on historical trends or statistical methods.
3. **Error Correction:** Corrects errors or inconsistencies in the data, such as incorrect dates or quantities.
4. **Data Normalization:** Standardizes the data to a common scale, making it easier to compare and analyze.
5. **Seasonal Adjustment:** Accounts for seasonal patterns in demand to get a clearer view of underlying trends.

### Key Challenges in Demand Cleansing

- **Data Quality Issues:** Dealing with inconsistent data formats, missing values, and errors.
- **Outlier Detection:** Identifying outliers without removing valuable information.
- **Imputation Methods:** Choosing the appropriate method for filling in missing data.
- **Computational Complexity:** Cleansing large datasets can be computationally intensive.

### Benefits of Effective Demand Cleansing

- **Improved Forecast Accuracy:** More accurate demand forecasts lead to better inventory management and reduced stockouts.
- **Enhanced Decision Making:** Data-driven decisions based on clean and reliable data.
- **Increased Efficiency:** Streamlined processes and reduced manual effort.

**In essence, demand cleansing is a crucial step in the process of transforming raw demand data into valuable insights that drive business decisions.**

## Demand Cleansing Steps

### 1. **Data Collection and Ingestion:**

- Gather demand data from various sources (e.g., sales data, point-of-sale systems, inventory records).
- Ingest the data into a suitable data warehouse or data lake.

### 2. **Data Validation and Cleaning:**

- **Check for completeness:** Ensure that all required fields are populated.
- **Verify accuracy:** Validate the data against known constraints (e.g., positive quantities, valid dates).
- **Identify and correct errors:** Address inconsistencies, typos, or other errors.
- **Handle missing values:** Impute missing values using appropriate methods (e.g., mean, median, interpolation).

### 3. **Data Standardization and Formatting:**

- **Convert data formats:** Ensure consistency in data formats (e.g., dates, currencies).
- **Standardize units of measure:** Convert units to a common standard (e.g., kilograms to pounds).
- **Cleanse text data:** Remove unnecessary characters, normalize case, and handle special characters.

### 4. **Outlier Detection and Removal:**

- **Identify outliers:** Use statistical methods (e.g., Z-score, IQR) to detect data points that deviate significantly from the norm.
- **Remove or adjust outliers:** Decide whether to remove outliers or adjust their values based on the context.

### 5. **Seasonal Adjustment:**

- **Identify seasonal patterns:** Analyze historical data to identify recurring seasonal fluctuations.
- **Adjust data:** Remove seasonal effects to reveal underlying trends.

### 6. **Data Aggregation and Transformation:**

- **Aggregate data:** Combine data at different levels (e.g., daily, weekly, monthly).
- **Transform data:** Apply transformations (e.g., log transformations, normalization) to improve data distribution.

### 7. **Data Quality Assessment:**

- **Evaluate data quality:** Use metrics (e.g., completeness, accuracy, consistency) to assess the quality of the cleansed data.
- **Iterate if necessary:** If data quality is not satisfactory, revisit previous steps and refine the cleansing process.

---

# _Demand Cleansing Methods Explanations:_

## `classifyAndCleanseDemand()`

### Purpose:

This method is a core component of the demand cleansing process. It classifies demand based on historical patterns and cleanses the data to ensure accuracy.

### Key Parameters

- **demandCleansingBatchContext**: Provides context information for the cleansing process.
- **demandCleansingPolicy**: Defines the rules and thresholds for cleansing.
- **tempDistributionByDemandClassification**: Stores temporary distribution data based on demand classification.
- **originalHistory**: The original demand history data.
- **tempDistributionByDateMap**: Maps dates to their corresponding temperature distributions.
- **productLocation**: Represents the product's location information.
- **demandCleansingResult**: Stores the results of the cleansing process.
- **demandClassification**: The classification assigned to the demand.
- **calledInFEContext**: Indicates whether the method is called from the frontend context.
- **demandClassificationOnly**: Indicates whether only demand classification is performed.

### Workflow

1. **Calculate Weighted Percentage of Zero Demand:**
    - Calculate the percentage of zero demand for each year.
    - Weight the percentages based on the policy's year weights.
    - Calculate the weighted average percentage of zero demand.
2. **Classify Demand as Intermittent or Regular:**
    - Compare the weighted average percentage to the zero demand threshold.
    - If it's greater than or equal to the threshold, classify as intermittent; otherwise, classify as regular.
3. **Cleanse Demand (if necessary):**
    - If `demandClassificationOnly` is false, call the `cleanseDemand` method to cleanse the data.
    - If `demandClassificationOnly` is true, create a new `IndexedHistory` instance with the original history values.
4. **Calculate Weighted Average of Cleansed Demand:**
    - Calculate the average demand for each year.
    - Weight the averages based on the policy's year weights.
    - Calculate the weighted average of cleansed demand.
5. **Classify Demand as Slow Mover or Fast Mover:**
    - Based on the demand classification (regular or intermittent) and the weighted average of cleansed demand, classify as slow mover or fast mover.
6. **Update Temp Distribution (if not in FE context):**
    - Update the `tempDistributionByDemandClassification` with the appropriate distribution detail based on the demand classification.
7. **Calculate Mean, Standard Deviation, and Other Metrics:**
    - Calculate the mean, standard deviation, and other metrics for the cleansed history.
    - Update the `demandCleansingResult` with these metrics.
    - Update the `demandClassification` with the calculated values.

### Key Logic

- **Weighted Averages:** The method uses weighted averages to account for the varying importance of different years in the demand history.
- **Thresholds:** The `demandCleansingPolicy` defines thresholds for determining if demand is intermittent or regular, and slow mover or fast mover.
- **Classification:** The method classifies demand based on both zero demand percentage and average demand.
- **Data Cleansing:** The `cleanseDemand` method (not shown in this snippet) likely performs additional cleansing steps, such as outlier detection or smoothing.
- **Temp Distribution Update:** The method updates a temporary distribution map to track the distribution of demand across different classifications.

### Potential Questions for `classifyAndCleanseDemand`
#### General Questions

- **Purpose:** What is the overall goal of this method? How does it contribute to the larger demand forecasting or analytics system?
- **Assumptions:** Are there any underlying assumptions about the data or the cleansing process? How do these assumptions impact the accuracy and reliability of the results?
- **Limitations:** What are the limitations of this method? Are there any scenarios where it might not provide accurate or meaningful results?
#### Specific Questions

- **Weighted Averages:** Why are weighted averages used to calculate the percentage of zero demand and the average cleansed demand? How are the weights determined?
- **Thresholds:** How are the thresholds for classifying demand as intermittent or regular, and slow mover or fast mover, defined? Are they based on historical data, domain knowledge, or other factors?
- **Data Cleansing:** What specific cleansing techniques are used in the `cleanseDemand` method (if applicable)? How do these techniques help improve data quality?
- **Temp Distribution Update:** What is the purpose of updating the `tempDistributionByDateMap`? How is this data used in subsequent analyses?
- **Classification Criteria:** How do the criteria for classifying demand as regular, intermittent, slow mover, or fast mover align with business requirements and industry best practices?
- **Performance:** Is the method computationally efficient? Are there any optimizations that could be made to improve performance?
- **Robustness:** How robust is the method to changes in data patterns or policy parameters? Is it able to adapt to evolving conditions?

By asking these questions, you can gain a deeper understanding of the method's functionality, assumptions, and potential areas for improvement.

## `processClassifyAndCleanseDemand()`

The code is a Java method responsible for processing demand data, classifying it based on historical patterns, and cleansing it to ensure data integrity. It's part of a larger demand forecasting system.

### Key Parameters:

- `calledInFEContext`: Indicates whether the method is called from the frontend context.
- `demandCleansingBatchContext`: Provides context information for the cleansing process.
- `demandCleansingPolicy`: Defines the rules and thresholds for cleansing.
- `tempDistributionByDemandClassification`: Stores temporary distribution data based on demand classification.
- `tempDistributionByDateMap`: Maps dates to their corresponding temperature distributions.
- `productLocation`: Represents the product's location information.
- `originalHistory`: The original demand history data.
- `demandCleansingResult`: Stores the results of the cleansing process.
- `demandClassification`: The classification assigned to the demand.
- `productLocationUpdateMap`: A map for updating product location information.
- `zeroFilledList`: A list of dates with zero demand.
- `plidPLMap`: A map relating product location IDs to product location objects.
- `isDemandClassificationOnly`: Indicates whether only demand classification is performed.

### Workflow:

1. **Check Product Location Status:** If the product location is inactive, classify it as inactive and record the result in `demandCleansingResult`.
2. **Handle New Demand:** If there's no original history and the demand classification is not inactive, classify the demand as new.
3. **Process Existing Demand:** If there's original history:
   - Zero-fill the history to ensure consistent time series.
   - Calculate the first and last non-zero demand periods.
   - Determine if the demand is new or inactive based on the non-zero demand periods and thresholds.
   - If the demand is not new or inactive, recursively call `classifyAndCleanseDemand` to further process the data.
4. **Return Cleansed History:** If a cleansed history was created, return it. If no cleansed history was created and there's original history, return the original history with zero-filling.
5. **Apply Demand Classification:** Update the product location update map with the demand classification.

### **Key Logic:**

- **Demand Classification:** The code classifies demand as new, inactive, or other based on historical patterns and thresholds defined in `demandCleansingPolicy`.
- **Zero-Filling:** Ensures that the demand history has consistent time series by filling missing data points with zeros.
- **Thresholds:** The `demandCleansingPolicy` defines thresholds for determining if a demand is new or inactive based on the number of non-zero demand periods.
- **Recursive Calls:** The `classifyAndCleanseDemand` method can recursively call itself to process demand data at different levels or granularity.

## `testDemandCleansing()`

### **Purpose:**

This code is a JUnit test case that simulates the demand cleansing process and verifies its correctness against expected results. It's likely part of a larger testing suite for a demand forecasting or analytics system.

### **Key Components:**

- `DemandCleansingBatchContext`: Creates a context object to store configuration parameters and results.
- `DemandCleansingPolicyEntity`: Represents the policy governing the cleansing process.
- `testData`: Contains test data, including expected results.
- `helper`: A helper class that provides utility methods for test setup and verification.

### **Workflow:**

1. **Initialize Context and Policy:** Creates a `DemandCleansingBatchContext` object and sets its demand smoothing period types. Creates a new `DemandCleansingPolicyEntity` and sets it as the policy for the context.
2. **Populate History:** Calls a `populateHistory` method to populate the context with test history data.
3. **Set Product Location:** Sets the product location information in the context.
4. **Configure Policy:** Sets various parameters of the `demandCleansingPolicy` based on the test data.
5. **Process Demand:** Calls the `processProductAggregation` method of the `demandCleansingBatchProcessor` to initiate the cleansing process.
6. **Verify Results:** Retrieves the cleansed history and demand classification from the context. Compares the cleansed history values against the expected results. Verifies the demand classification status, type, and mover category.

### **Key Logic:**

- **Test Data:** The test data contains expected results for comparison.
- **Policy Configuration:** The code sets various policy parameters based on the test data to simulate different scenarios.
- **Result Verification:** The code compares the cleansed history and classification against expected values to ensure correctness.

### Analyzing the Code: Potential Questions

**processClassifyAndCleanseDemand()**

- Classification Criteria: What are the specific criteria used to classify demand as "new," "inactive," or "other"? How do these criteria align with business requirements?
- Recursive Calls: Why does the method recursively call itself in certain scenarios? What is the purpose of this recursion, and how does it contribute to the overall cleansing process?
- Zero-Filling: What is the rationale behind zero-filling the demand history? How does this impact the subsequent analysis and classification?
- Thresholds: How are the thresholds for determining new or inactive demand (e.g., `newThresholdPeriods`, `inactiveThresholdPeriods`) defined and adjusted? Are they based on historical data, domain knowledge, or other factors?
- Product Location Impact: How does the product location status (active or inactive) influence the cleansing process? Are there specific considerations or adjustments made for inactive locations?

**testDemandCleansing()**

- Test Coverage: What scenarios does this test case cover? Are there any edge cases or specific scenarios that are not adequately tested?
- Expected Results: How are the expected results for the test case determined? Are they based on historical data, simulations, or other sources?
- Test Data: Is the test data representative of real-world scenarios? Are there any limitations or assumptions associated with the test data?
- Assertions: Are the assertions in the test case comprehensive and appropriate? Do they adequately verify the correctness of the cleansed data and classification?
- Test Automation: How is this test case integrated into the overall testing process? Is it automated and run regularly?

---
# [[Presentations]] outline:

## **Demand Cleansing: A Culinary Analogy**
## **Introduction:**

Imagine you're a chef preparing a gourmet meal. The raw ingredients are your historical demand data. Before you can create a masterpiece, you need to ensure these ingredients are clean, fresh, and free from impurities. This is where **demand cleansing** comes in.

Just like cleaning ingredients, demand cleansing ensures that your data is accurate, consistent, and ready for use in demand forecasting. It’s the foundation for creating reliable insights and making business decisions.

---

## **Why is Demand Cleansing Important?**
- **Data Quality**: Ensures your data is free from anomalies like promotions and events, giving you a clear baseline.
- **Forecast Accuracy**: Increases the reliability of your forecasts by providing clean data.
- **Decision Making**: Provides a strong foundation for better decision-making, backed by trustworthy data.

### Additional Importance:
- **Baseline Historical Metric**: Cleansing removes outliers such as promotions and events from your data, ensuring that your baseline historical metric reflects true demand.
- **Incorporating Lost Sales**: Cleansed demand also factors in lost sales, providing a more comprehensive view of actual demand.

---

## **Common Cleansing Techniques**

1. **Outlier Detection**: Identifies and removes data points significantly different from the norm, such as sales during promotions or special events.
2. **Missing Data Input**: Fills in missing values using historical trends or statistical methods.
3. **Error Correction**: Corrects inconsistencies, such as invalid dates or quantities.
4. **Data Normalization**: Standardizes data across different scales to enable comparison and analysis.
5. **Seasonal Adjustment**: Removes seasonal patterns to better understand underlying trends.

---

## **Key Challenges in Demand Cleansing**

- **Data Quality Issues**: Handling inconsistent formats, missing values, and errors.
- **Configuring Demand Cleansing Policies**: Defining how to handle outliers, incorporating promotions and events.
- **Outlier Detection**: Balancing the removal of outliers without discarding valuable information.
- **Imputation Methods**: Deciding the best approach to handle missing data.
- **Computational Complexity**: Cleansing large datasets efficiently can be challenging.

### Policy Configuration:
- **Demand Cleansing Policies** allow users to define cleansing classification parameters and how to react to conditions like promotions and lost sales. These policies ensure accurate cleansing at item and location hierarchies.

---

## **Benefits of Effective Demand Cleansing**

- **Improved Forecast Accuracy**: Better inventory management and fewer stockouts due to more accurate demand forecasts.
- **Enhanced Decision Making**: Data-driven decisions are possible when using clean, reliable data.
- **Increased Efficiency**: Streamlines processes, reduces manual effort, and ensures your cleansed demand reflects true demand.

### Additional Benefits:
- **Accurate Demand Metrics**: Calculating net demand (sales - promotions + lost sales) and storing it as **cleanseSales** gives a precise view of demand.
- **Streamlined Process**: Once demand cleansing is initially run, the system handles further updates automatically during forecasting periods, unless new data changes occur.

---

## **Demand Cleansing Process Steps**

### 1. **Data Collection and Ingestion:**
- Gather demand data from various sources, including sales, promotions, and lost sales.

### 2. **Data Validation and Cleaning:**
- Apply **Demand Cleansing Policy** to identify and remove outliers like promotions and events, ensuring your baseline demand is accurate.
- Ensure lost sales are incorporated into the cleansed data.

### 3. **Data Standardization and Formatting:**
- Convert formats (dates, currencies), standardize units of measure, and cleanse text data to ensure consistency.

### 4. **Outlier Detection and Removal:**
- Detect outliers, such as promotions and special events, and remove or adjust them to focus on core demand.

### 5. **Seasonal Adjustment:**
- Remove seasonal effects from the data to better understand underlying trends.

### 6. **Data Aggregation and Transformation:**
- Aggregate data at appropriate levels and apply transformations to improve data usability.
- Calculate **net demand** (sales - promotions + lost sales) and store it as **cleanseSales**.

### 7. **Data Quality Assessment:**
- Assess the quality of the cleansed data using metrics like completeness and accuracy.
- Iterate and refine cleansing as necessary to meet quality standards.

---

## **Demand Cleansing Methods - A Closer Look**

### **Demand Cleansing Policy**:
- Allows users to configure **Cleansing Classification Parameters** and **Demand Cleansing Parameters** for items at their respective location hierarchies.
- Ensures that demand cleansing is tailored to the specific needs of each item and location for more accurate forecasts.

### **Ongoing Data Updates**:
- After the initial demand cleansing, the system automatically updates data (sales, promotions, lost sales) each period (weekly or monthly) unless new sales, promotions, or lost sales data trigger manual intervention.

---

## **Key Questions to Consider**

- **When to Run Cleansing**: Should you run demand cleansing more than once? Usually, you don’t need to manually re-run it unless new sales, promotions, or lost sales data change.
- **Policy Setup**: How do your **Cleansing Parameters** handle the specific needs of different items and locations? Are they configured to handle promotions, events, and lost sales accurately?

---

## **Conclusion**

**Demand cleansing** is essential for ensuring that your demand data is free from outliers, accurately reflects true demand, and incorporates lost sales. A well-configured demand cleansing policy not only improves forecast accuracy but also automates much of the process after the initial run, saving time and effort.

In essence, **demand cleansing** is like preparing your ingredients before cooking. You can't create a reliable forecast if the data (ingredients) aren't clean and ready for analysis. With effective demand cleansing, your data becomes a powerful tool for making informed business decisions.

---
