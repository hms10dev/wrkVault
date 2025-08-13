Reference:
https://manhattanassociates.atlassian.net/wiki/spaces/ASCP/pages/4320493604/Demand+Cleansing+Policy
Related: [[Training/Enterprise Supply Chain Management/Enterprise Supply Chain Management|Enterprise Supply Chain Management Book Log]]

### Terminologies

**Uncleansed Sales:**

- Raw sales quantity from host system
    
- Everything sold during the history dsperiod (regardless of the reason)
    

**Demand:**

- Represents what was sold, shipped or expected to sell during a period
    
- Represents Cleansed Sales = Un-cleansed Sales + Lost Sales - Promotional Sales
    
- Clamping is done to the raw sales quantity to smooth the out-liners or remove spikes (for accurate forecast)
    

**Adjusted Cleansed Sales:**

- Represent the cleansed sale based on Item relationship
    
- Cleansed sales of new Item + Cleansed sales of old Item
    

**Cleansed vs. Clamped:**

- Cleansed is based on all historical data (like Forecast init)
    
- Clamped is based on the most recent/current week demand (like Forecast update).