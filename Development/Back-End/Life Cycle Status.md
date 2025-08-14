# Lifecycle Status - Complete Reference

## Overview & Business Purpose

**What it is**: A way for customers to categorize items based on where they are in their sales lifecycle, helping manage millions of SKUs efficiently.

**Why it matters**: Determines what forecasting and ordering actions should be taken for each item.

## Lifecycle Status vs. Lifecycle Configuration

### **Key Distinction (SCP vs DFIO):**

- **SCP**: Lifecycle Status and Lifecycle Configuration are **separate entities**
    - Status must be set up first to be available in Configuration dropdown
- **DFIO**: Configuration is defined in the same entity as the status

### **Lifecycle Status** (Code and Description)

- The label/identifier (e.g., "ACTIVE", "INACTIVE", "DISCONTINUED")
- Can be set at multiple levels: Item Location, Item, Item Inheritance Policy

### **Lifecycle Configuration** (The Boolean Flags)

- The behavior settings for each status
- Can be set at same levels: Item Location, Item, Item Inheritance Policy
- **Key flexibility**: Same status can have different configurations for different items

**Example**:

- ACTIVE at global level: Calculate Order Factors = Yes, Calculate Order Quantities = Yes
- ACTIVE for specific item: Calculate Order Factors = Yes, Calculate Order Quantities = No

## Common Lifecycle Stages & Values

### **Standard Statuses:**

1. **Active** - Normal forecasting and ordering
2. **Inactive** - Temporarily not selling
3. **Discontinued** - End of life, clear remaining inventory

### **Lifecycle Progression:**

1. **New Item** - Just introduced, may need promotional forecasting
2. **Active** - Standard selling item, full forecasting and ordering
3. **Discontinued** - End of life, selling remaining inventory, no new orders

## Technical Implementation

### **Inheritance Framework:**

- **Performance optimization**: Status isn't stored on all 16 million item locations
- **Inheritance hierarchy**: Global → Region → Class → Item → Item Location
- **On-the-fly resolution**: Item Location gets status from its parent when requested
- **Source**: "inherited attribute on itemLocation gets inherited from the item"

### **Boolean Configuration Flags:**

Each lifecycle status has multiple boolean settings (~10-15 total):

- Should I forecast?
- Should I order?
- Should I estimate lost sales?
- Bypass all processing?
- Calculate demand forecast
- Calculate order factors
- Calculate order quantities

## Integration with Forecasting

### **How Forecasting Uses Lifecycle Status:**

1. **Forecast Initialization**: System fetches lifecycle status from item location
2. **Boolean check**: "Should I forecast this item?"
3. **Action taken**:
    - If "Calculate Forecast" = Yes → Run forecasting
    - If "Calculate Forecast" = No → Skip forecasting
    - If "Bypass All Processing" = Yes → Do nothing

### **Storage on Forecast Entity:**

- Lifecycle status gets **saved on the forecast entity** during processing
- **Represents**: "This was the lifecycle status the last time forecasting ran"
- **Not real-time** - only updated when forecast processes run again
- **Could be stale** if status changes between forecast runs

### **Update Cycle:**

- **Forecast Initialization**: Fetches and saves lifecycle status
- **Forecast Update**: Re-fetches and updates lifecycle status
- **Key point**: Status on forecast = "lifecycle status as of last forecast run"

## Real-World Business Examples

### **Gap Retail Scenario:**

- **Spring polo shirts in summer**: Still active, normal forecasting continues
- **Spring polo shirts in fall**: Discontinued, clear inventory, no new supplier orders
- **Why no forecasting for discontinued?** No point forecasting if you're not ordering more from suppliers

### **Business Logic by Status:**

- **Active items**: Need forecasting to determine how much to order from suppliers
- **Discontinued items**: Just selling remaining stock, no supplier orders needed
- **Inactive items**: Temporarily not selling (maybe seasonal), may resume later

## Current Development Work (AI-20833)

### **PSO Request:**

- **Problem**: PSO can't see lifecycle status on Forecast Entity list page
- **Solution**: Abolash adding lifecycle status field to forecast entity backend
- **My UI Work**: Display the field properly with correct labeling

### **My Role & Learning Opportunities:**

1. **UI Implementation**: Add field to forecast entity display (straightforward)
2. **Code Review**: Review Abolash's backend implementation to learn patterns
3. **Domain Knowledge**: Build understanding of how forecasting uses lifecycle data
4. **Business Context**: Understand the "why" behind the technical work

## Key Questions for Learning

### **Technical Understanding:**

- How does inheritance framework determine which status to use?
- What happens if status changes mid-cycle?
- How do the boolean flags affect different forecasting processes?
- What other components use lifecycle status?

### **For Current Story:**

- Does every forecast entity need to display lifecycle status?
- How should we handle inherited vs. direct status values?
- What's the user experience expectation for PSO?

## Documentation References

- [Life Cycle Policy Documentation](https://manhattanassociates.atlassian.net/wiki/spaces/ASCP/pages/4316954746/Life+Cycle+Policy)
- [Life Cycle Policies (Edit)](https://manhattanassociates.atlassian.net/wiki/spaces/ASCP/pages/edit-v2/5210964268#Life-Cycle-Policies)

## Residency Training Notes

### **Log This Learning As:**

- "Research on lifecycle status and relationship to forecasting"
- "Understanding inheritance framework in item location context"
- "Business logic: how lifecycle status drives forecasting decisions"
- "SCP vs DFIO lifecycle configuration differences"

### **Future Value:**

- When in meetings about lifecycle status, I'll understand the business context
- Can contribute to discussions about forecasting behavior
- Understand why certain items don't get forecasted
- Know the difference between status and configuration

---

**Key Takeaway**: While my UI implementation is straightforward (add a field), understanding this business context helps me work more effectively with the team and contribute meaningfully to discussions about forecasting behavior.