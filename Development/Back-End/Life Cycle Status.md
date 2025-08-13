inherited attribute on itemLocation gets inherited from the item

https://manhattanassociates.atlassian.net/wiki/spaces/ASCP/pages/4316954746/Life+Cycle+Policy
https://manhattanassociates.atlassian.net/wiki/spaces/ASCP/pages/edit-v2/5210964268#Life-Cycle-Policies

**Life Cycle Status**: Code and Description

- In SCP, Life Cycle Status is a separate entity from Life Cycle Configuration (e.g. calculate demand forecast, calculate order factors, etc.). Life Cycle Statuses must be set up first for them to be available in the Life Cycle Configuration drop down.
    
    - In DFIO, life cycle configuration is defined in the same entity as the status
        
- Life Cycle Status can be set at the following levels: Item Location, Item, Item Inheritance Policy
    

**Life Cycle Configuration**:

- Life Cycle Configuration can be set at the following levels: Item Location, Item, Item Inheritance Policy
    
- A Life Cycle Status can have different meanings for different Items / Item Locations
    
- Example:
    
    - ACTIVE can be defined at the highest level with Calculate Order Factors and Calculate Order Quantities = true
        
    - For a particular Item or Item Location, ACTIVE configuration can be overridden to Calculate Order Factors = true and Calculate Order Quantities = false. The Item / Item Locations can behave differently without host sending a separate Life Cycle Status