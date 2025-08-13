# Enterprise Supply Chain Management Book Log

Focus Areas: Forecasting • Demand Cleansing • Inventory Optimization • Seasonal Profiling

## 1. Introduction to Demand Forecasting
- Forecasting is about projecting demand using historical data, adjusted for trends, seasonality, and external influences.
- Methods include moving averages, curve fitting, and time series analysis.
- The forecast drives decisions across production, purchasing, and distribution.
- Related: [[Development/Back-End/Code notes/Forecast Projection Calculation|Forecast Projection Calculation]]

## 2. Inputs for Forecasting
- Requires item/location master data, sales & price history, configurations like seasonality, data cleansing rules, causal events.
- Output: unconstrained demand forecast, forecast error metrics (e.g. MAPE, MAD).

## 3. Data Cleansing & Demand Spikes
- Cleansing removes anomalies like spikes (e.g., >2σ deviations); suspect data can be auto-flagged or manually reviewed.
- "Lost sales" (e.g., due to stockouts) can be algorithmically restored for true demand representation.
- See also [[Development/SCP/Demand Cleansing Notes|Demand Cleansing Notes]].

## 4. Seasonality & Seasonal Profiling
- Seasonal indices capture patterns in weekly/monthly demand.
- De-seasonalized forecasts remove fluctuations, then indices are reapplied to recreate seasonal demand.
- Helps improve long-range and promotional forecast accuracy.

## 5. Causal Factor Modeling
- Planned events: promos, holidays, clearance sales.
- Unplanned events: weather, local incidents.
- Causal models normalize history to better reflect demand.
- Future forecasts can reuse historical causal factors as templates.

## 6. Forecast Accuracy & Analytics
- Key metrics: Forecast Error (MAPE, MAD), Tracking Signal (bias detection over time).
- Waterfall/cascade analysis compares previous forecasts to actuals to evaluate forecast improvement toward delivery week.

## 7. Inventory Optimization
- Balances holding cost vs. stockout risk using safety stock levels, service level targets, reorder policies (OUTL).
- Depends heavily on forecast accuracy to avoid overstock/understock situations.
- Related training: [[Training/Active Inventory/Active Allocation Training|Active Inventory Training]].

---

## Weekly Log
### Week Ending: Mar 07, 2025 – Introduction to Forecasting
- Forecasting is the starting point for demand planning—projecting future sales based on past data.
- Common methods: moving average, time series, curve fitting.
- Forecasts drive production, purchasing, and distribution strategies.

### Week Ending: Mar 14, 2025 – Forecast Inputs & Configuration
- Inputs include item/location data, sales history, pricing, and event data.
- Forecasting systems also rely on seasonal settings and causal factors.
- Forecast outputs: unconstrained demand and forecast error reports like MAPE and MAD.

### Week Ending: Mar 21, 2025 – Demand Cleansing
- Cleansing filters out anomalies like spikes and dips.
- Lost sales (e.g., stockouts) can be restored using statistical models.
- Ensures the data reflects true demand, not noisy artifacts.

### Week Ending: Mar 28, 2025 – Seasonal Profiling
- Seasonal indices are calculated to de-seasonalize demand and then re-apply patterns.
- Helps in modeling future promotional or event-driven spikes accurately.
- Essential for long-term forecast smoothing and realism.

### Week Ending: Apr 04, 2025 – Inventory Optimization & Forecast Accuracy
- Inventory optimization balances service level goals with cost.
- Key factors: safety stock, lead time variability, forecast error.
- Forecast accuracy is tracked via MAPE, MAD, and tracking signals.
- Waterfall analysis helps track improvements and measure bias over time.
