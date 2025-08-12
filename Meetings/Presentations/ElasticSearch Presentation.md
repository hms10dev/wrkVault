# Outline:

## Title
## Overview

## Intro/What is ElasticSearch?
- distibuted, RESTful search and analytics engine. build on top of Apache Lucene
- instead of information being stored as rows of columnar data, ElasticSearch stores complex Data structures serialized as JSON Docs
## What does it have to do with SCP?

## Visual Aid

## Kibana & What is Kibana?
- Kibana is Open Source Data Visualization & Exploration tool By Elastic Folks
- Provisioned for all MA Stacks
- At Runtime, Our applications run and create logs while doing so
- Kibana Allows us to actually dissect those logs and get more insight into them

## How it helps us
- The MA Products sit on a componentized platform of individual servers which work together to execute tasks. Tasks may be as simple as:

> > **“Fetch the forecast policy for item X at location Y.”**

Example policy data returned:

```json
{
	"item": "12345",
	"location": "DC_East",
	"forecast_method": "croston",
	"time_granularity": "weekly",
	"seasonality": "low",
	"manual_override": false
}

```


These simple tasks are likely to be satisfied by a single component. However, tasks may become as complex as the business flow requires, such as:

> Determine and apply the most appropriate forecast policy for item X across multiple locations, considering historical demand variability, item lifecycle stage, promotions, planned events, and capacity constraints — and automatically trigger a re-forecast if any conditions have changed.

These more complex tasks are likely to involve logic and resources from many components. Each component involved is responsible for publishing its own logs statements to Elasticsearch, which in turn consolidates and indexes these messages. Then, Kibana permits a user to query and review logs in near-real time across all components of the MA application.

### How to Access
URL

## Visual/Examples to put in presentation
![[screenshotr_2025-4-23T11-26-29.png]]
![[Pasted image 20250423105658.png]]
![[Pasted image 20250423111027.png]]
## Any Questions?




##Additional Notes:
Its built with Java, Elasticsearch is a **NoSQL database**. That means it stores data in an unstructured way and that you cannot use SQL to query it.
### Resources:
https://manhattanassociates.atlassian.net/wiki/spaces/~565623871/pages/1005980656/Elasticsearch
https://manhattanassociates.atlassian.net/wiki/spaces/COE/pages/5022515578/Elasticsearch+Kibana+for+Logs
https://manhattanassociates.atlassian.net/wiki/spaces/COE/pages/5023334548/Browsing+Kibana
https://zapier.com/blog/screenshot-background/#:~:text=generators%20happened%20via-,Pika,-.%20I%27ve%20followed%20the

https://www.elastic.co/



---
# Presentation iteration 2:

#### **Slide 1: Title**

**Elasticsearch & Kibana in MA Applications: What Consultants Need to Know**

_Speaker notes:_  
"Today’s session will keep things simple and practical — we’ll cover what Elasticsearch and Kibana are, how they fit into MA applications, and what consultants like you need to know when working with these tools."

---

#### **Slide 2: Objectives**

✅ Why Elasticsearch is used  
✅ How Kibana helps us troubleshoot  
✅ What you need to know as consultants  
✅ Best practices

_Speaker notes:_  
"My goal is not to turn you into Elasticsearch engineers — it’s to give you confidence in using Kibana effectively and help you understand what’s going on behind the scenes."

---

#### **Slide 3: What is Elasticsearch?**

- Distributed search and analytics engine
    
- Stores logs as JSON documents
    
- Optimized for fast, near real-time search (~1 second latency)
    
- Powers all log searchability behind Kibana
    

_Speaker notes:_  
"Elasticsearch is a special kind of search engine designed to store logs efficiently. It takes all the logs from various MA components and makes them searchable almost immediately — that’s what enables the Kibana experience you’re familiar with."

---

#### **Slide 4: Why Elasticsearch matters here**

- MA platform = componentized system
    
- Complex workflows involve many components
    
- Each component logs independently
    
- Elasticsearch consolidates and indexes all these logs so Kibana can show them
    

_Speaker notes:_  
"In MA applications, a single workflow may touch several components. Each one logs independently, but Elasticsearch gives us a centralized, searchable way to view everything that happened."

---

#### **Slide 5: Key Elasticsearch concepts (just enough detail)**

- **Index = like a collection or table of logs**
    
- **Document = single log entry (JSON)**
    
- **Field = key-value pair in a document (e.g., `log_level`, `component_name`)**
    
- **Near real-time = searchable within ~1 second of being written**
    

_Speaker notes:_  
"You don’t need to memorize this, but it helps to know that logs are stored as documents, grouped in indices, and can be queried almost instantly."

---

#### **Slide 6: Transition: Elasticsearch + Kibana together**

**Diagram:**  
`MA Components → Logs → Elasticsearch → Kibana (Discover Page) → You`

_Speaker notes:_  
"Everything you do in Kibana is powered by Elasticsearch in the background — but you don’t need to work with Elasticsearch directly. Kibana is your window into this system."

---

#### **Slide 7: Using Kibana as a consultant**

- **Discover page = where you browse logs**
    
- Time filtering:
    
    - Default = last 15 min
        
    - Use **absolute time ranges for consistency when sharing links**
        
- Query bar = search free text (e.g., `OrderId`)
    
- Filters = narrow by fields like Log Level, Component
    

_Speaker notes:_  
"Kibana’s Discover page will be your home base. I encourage you to get comfortable filtering logs efficiently and using absolute time ranges when sharing queries — this ensures your teammate sees exactly what you saw."

---

#### **Slide 8: Common fields to look at**

- Log Level
    
- Component Name
    
- Message
    
- Trace ID (critical for following workflows)
    

_Speaker notes:_  
"These fields give you context and make troubleshooting much easier. Trace ID especially helps you follow a single transaction or workflow across components."

---

#### **Slide 9: Best practices for consultants**

✅ Scope searches carefully  
✅ Use Trace ID where available  
✅ Filter out noise (e.g., exclude TRACE-level logs when not needed)  
✅ Use absolute time ranges  
✅ No API work required — **Kibana is your tool**

---

#### **Slide 10: Summary**

- Elasticsearch = backend engine for logs
    
- Kibana = your interface for exploring logs
    
- Consultants: focus on **using Kibana efficiently to troubleshoot and validate workflows**
    

_Speaker notes:_  
"Elasticsearch works quietly in the background. Your role is simply to use Kibana confidently, knowing that you’re tapping into a robust log search system."

---

### 📸 **Screenshots to prepare**

Here’s what you could grab for visuals:  
✅ Screenshot of **Kibana Discover page**, showing some logs  
✅ Screenshot showing how to select an **absolute time range filter**  
✅ Screenshot showing the **Query Bar and a query example (e.g., searching for an OrderId)**  
✅ Screenshot showing how to **add fields to the Selected Fields pane**  
✅ Optional: Screenshot of the **filters sidebar showing Log Level and Component filters**

---

✅ **Diagram suggestion for Slide 6:**  
If you want a simple diagram:

```
MA Components → Elasticsearch → Kibana → Consultant/User
```

With arrows and icons if possible (even basic shapes would work).

---

# Draft 2

# Elasticsearch & Kibana for Manhattan Active SCP

_For Implementation Consultants_

## Opening Hook

**Why start here:** Set the stage with SCP-specific consultant challenges

- "It's Monday morning, Pet Supplies Plus reports their replenishment calculations aren't running, and you need to trace what happened across Forecasting, Allocation, and Replenishment modules"
- "With SCP's event-driven continuous calculations, understanding the log flow is critical for successful implementations"

## 1. What is Elasticsearch & Why is it Critical for SCP? (Foundation)

**Manhattan Active SCP Context**

- Distributed document store that captures logs from all SCP modules
- Component of the Elastic Stack (Elasticsearch + Kibana) provisioned for every SCP stack
- Near real-time indexing: when SCP generates a log, it's searchable within 1 second

**Why SCP Needs Robust Logging**

- **Complex Event-Driven Architecture**: Continuous order calculations trigger cascading events
- **Multiple Planning Modules**: Forecasting → Allocation → Replenishment workflows
- **Real-Time Decision Making**: Unified Business Planning Console needs instant visibility
- **Integration Points**: SCP works with Omni and WM - need unified troubleshooting view

**GA Since October 2024**

- Rapid quarterly releases mean evolving functionality to monitor
- New implementations like Innovasport and Pet Supplies Plus require strong troubleshooting capabilities
- Proven science algorithms need detailed logging for optimization and debugging

## 2. How Elasticsearch Works with SCP (Simplified for Consultants)

**Document-based storage**

- Each SCP log entry = one JSON document with all metadata
- Planning calculations, allocation decisions, replenishment triggers all logged as structured documents
- Attribute inheritance framework events captured with hierarchical context

**The "Magic" - Inverted Index for SCP**

- Traditional approach: manually searching through planning calculation logs
- Elasticsearch: Instantly find "AllocationException" or "ReplenishmentFailure" across millions of events
- Why you can trace a specific SKU's planning journey in seconds, not hours

**SCP Integration Architecture**

- **Forecasting Module**: Demand planning calculations and model performance logs
- **Allocation Module**: Push/pull allocation decisions and constraint violations
- **Replenishment Module**: Order generation, supplier integration, and inventory optimization
- **Unified Business Planning Console**: Dashboard activity and KPI calculation logs
- **Event-Driven Calculations**: Continuous calculation triggers and dependencies

## 3. Primary Use Cases in SCP Implementations

**Planning Process Troubleshooting**

- Forecasting model failures and accuracy analysis
- Allocation constraint violations (capacity, financial, supplier limits)
- Replenishment calculation errors and order generation issues
- Event-driven calculation chain analysis

**Cross-Module Integration Debugging**

- Following demand signals from Forecasting → Allocation → Replenishment
- Canvas-widget dashboard performance and data loading issues
- Attribute inheritance propagation tracking
- Integration points with Manhattan Active Omni and WM

**Performance & Optimization Analysis**

- Planning calculation performance bottlenecks
- Event-driven continuous calculation efficiency
- Dashboard widget loading and KPI calculation times
- Large dataset processing (assortment planning for retailers like Innovasport)

**Business Process Monitoring**

- Short vs. long life cycle product handling differences
- Seasonal planning cycle performance
- Supplier integration and collaboration workflow tracking

## 4. SCP-Specific Architecture Understanding

**Module Integration & Log Flow**

- Each SCP module publishes to its own message queues
- Elasticsearch consumes and indexes automatically with SCP-specific patterns
- Index patterns: `scp-forecasting-{nodeId}-{date}`, `scp-allocation-{nodeId}-{date}`, `scp-replenishment-{nodeId}-{date}`

**Multi-Environment Support for SCP**

- Separate Elasticsearch clusters per environment (dev/test/prod)
- Independent Kibana instances per SCP stack
- URL pattern: `https://{stackcode}-logs.scp.manh.com`
- Examples: `https://innovasport-logs.scp.manh.com`, `https://petsuppliesplus-logs.scp.manh.com`

**Event-Driven Calculation Logging**

- Continuous calculation triggers logged with cause/effect relationships
- Planning horizon calculations tracked with time boundaries
- Canvas-widget performance metrics and user interaction logs

## 5. Kibana Deep Dive (Primary Tool for SCP Consultants)

**Navigation & Interface**

- Home vs. Discover pages for SCP-specific troubleshooting
- Dev Tools for advanced planning calculation queries (light introduction)
- Dashboard section for Unified Business Planning Console monitoring

**SCP Document Structure**

- How planning calculation logs appear with business context
- Module-specific fields: forecast accuracy, allocation constraints, replenishment triggers
- Understanding SCP-specific field mappings and data types

**Essential Fields for SCP Troubleshooting**

- **Log Level**: ERROR, WARN, INFO, DEBUG, TRACE
- **Module Name**: FORECASTING, ALLOCATION, REPLENISHMENT, CONSOLE
- **Calculation ID**: Following specific planning runs across modules
- **SKU/Product Context**: Item-specific planning information
- **Planning Horizon**: Time boundaries for calculations
- **Event Type**: TRIGGER, CALCULATION, COMPLETION, ERROR
- **Message/Log**: The actual planning process details
- **Timestamp**: Critical for event sequencing in continuous calculations

**Time Range Filtering**

- Absolute vs. Relative time ranges
- Best practices: Use absolute ranges when sharing links with team
- Timeline histogram for visual log volume analysis

## 6. SCP-Specific Search Strategies

**Query Bar Techniques for Planning Scenarios**

- Search for specific SKUs across planning modules: `"SKU-ABC123"`
- Find allocation constraint violations: `"constraint violation" OR "capacity exceeded"`
- Locate forecasting model errors: `"model failed" OR "accuracy threshold"`
- Track replenishment triggers: `"order generation" AND "supplier"`

**SCP Filtering Best Practices**

- **Filter by Module**: `module.keyword: "ALLOCATION"` vs `module.keyword: "FORECASTING"`
- **Filter by Calculation Type**: `calculation_type: "CONTINUOUS"` vs `calculation_type: "BATCH"`
- **Filter by Planning Horizon**: `horizon_start: "2025-01-01"`
- **Filter by Event Sequence**: `event_type: "TRIGGER"` → `event_type: "COMPLETION"`
- **Exclude Debug from Production**: `NOT log_level: "DEBUG"` for performance

**SCP Field Selection for Planning Analysis**

- Calculation ID for following planning runs
- SKU/Product information for item-specific analysis
- Planning horizon boundaries for time-based troubleshooting
- Module and event type for process flow understanding
- Performance metrics for optimization analysis

**Time Range Best Practices for SCP**

- **Event-Driven Calculations**: Use narrow time windows (1-2 hours)
- **Planning Cycles**: Align with business planning periods (daily/weekly)
- **Cross-Module Analysis**: Expand time range to capture full planning flow
- **Performance Analysis**: Use consistent time boundaries for comparison

## 7. Common SCP Troubleshooting Scenarios

**Planning Calculation Chain Analysis**

- Following demand signal from Forecasting → Allocation → Replenishment
- Using Calculation ID to trace planning runs across modules
- Identifying where planning chains break or stall
- Timeline analysis for planning cycle performance

**Allocation Constraint Debugging**

- Finding capacity, financial, or supplier constraint violations
- Analyzing push vs. pull allocation decision patterns
- Tracking attribute inheritance impact on allocation rules
- Correlating allocation failures with business rules

**Replenishment Investigation**

- Order generation failures and supplier integration issues
- Inventory optimization calculation errors
- Lead time and safety stock calculation problems
- Supplier collaboration workflow troubleshooting

**Console & Dashboard Performance**

- Canvas-widget loading performance analysis
- KPI calculation bottlenecks in Unified Business Planning Console
- Dashboard personalization and configuration issues
- Multi-widget performance impact analysis

## 8. Data Export & Collaboration

**Saving & Sharing Searches**

- Saving frequently used search patterns
- Generating shareable links with absolute time ranges
- Exporting search results to CSV for further analysis

**Best Practices for Team Collaboration**

- Creating descriptive names for saved searches
- Using consistent filtering approaches across team
- Documenting search strategies for common issues

## 9. Live SCP Kibana Demo

**Hands-On Walkthrough**

- Accessing Kibana for a sample SCP environment
- SCP-specific navigation and interface orientation
- Creating searches for planning calculation errors
- Adding SCP-relevant fields and module filters
- Following a planning calculation using Calculation ID
- Exporting planning analysis results

**Real SCP Scenarios**

- "Let's investigate why replenishment calculations failed for Pet Supplies Plus"
- "How do we trace a SKU's planning journey from Forecasting through Replenishment?"
- "Finding allocation constraint violations during Innovasport's peak season planning"
- "Analyzing Canvas-widget performance issues in the Unified Business Planning Console"
- "Troubleshooting attribute inheritance propagation across planning hierarchies"

## 10. Understanding SCP Index Patterns & Organization

**SCP-Specific Naming Conventions**

- Index structure: `scp-{module}-{nodeId}-{date}`
- Examples: `scp-forecasting-psp01-2025-01-22`, `scp-allocation-innovasport-2025-01-22`
- Module-specific patterns for targeted troubleshooting

**Planning Module Patterns**

- **Forecasting**: Demand planning, model training, accuracy metrics, statistical calculations
- **Allocation**: Push/pull decisions, constraint management, capacity planning, supplier optimization
- **Replenishment**: Order generation, supplier integration, inventory optimization, lead time calculations
- **Console**: Dashboard performance, KPI calculations, canvas-widget interactions, user activity
- **Integration**: Cross-system communication with Omni and WM, data synchronization

**Event-Driven Architecture Considerations**

- Continuous calculation logs vs. batch processing logs
- Event sequencing and dependency tracking across modules
- Performance impact of high-frequency event logging
- Planning horizon boundaries affecting log organization

## 11. SCP Environment Access & Setup

**Accessing SCP Kibana Instances**

- URL patterns for SCP environments: `https://{client}-logs.scp.manh.com`
- Authentication through Manhattan domain accounts
- Requesting access for new SCP implementations and client environments

**SCP Index Patterns in Kibana**

- Setting up module-specific index patterns for new implementations
- Understanding SCP field mappings and planning-specific data types
- Configuring canvas-widget and console-specific visualizations

**Client Implementation Considerations**

- Innovasport: Comprehensive ecosystem with Omni and WM integration logs
- Pet Supplies Plus: Transition from DFIO requiring comparative analysis capabilities
- New implementations: Template index patterns and search configurations

## 12. Performance Tips & Best Practices

**Efficient Searching**

- Start with time range filters to limit data volume
- Use specific component filters early in your search
- Prefer filters over free-text queries when possible
- Avoid overly broad wildcard searches

**Memory & Browser Performance**

- Limiting search result sizes for large datasets
- Using scroll functionality for large result sets
- Browser considerations when working with large log volumes

**Collaboration Efficiency**

- Establishing team conventions for search naming
- Creating reusable search templates for common scenarios
- Documentation practices for complex troubleshooting procedures

## Closing & Q&A

**Key Takeaways for Consultants**

- Elasticsearch + Kibana = Primary troubleshooting toolkit for MA implementations
- Master time range filtering, component filtering, and trace ID following
- Save and share effective search patterns with your team
- Remember: Most client issues can be diagnosed through systematic log analysis

**Next Steps**

- Hands-on practice with sample environments
- Building team search libraries for common issues
- Integration with existing troubleshooting workflows

**Open Floor for Implementation Questions**

- Environment-specific setup questions
- Client-specific use case discussions
- Integration challenges and solutions

---

## Presentation Tips

### **Engagement Techniques for Consultants**

- **Scenario-Based Learning**: Present real client situations rather than abstract examples
- **Interactive Troubleshooting**: Have audience suggest search strategies for sample problems
- **Hands-On Practice**: Provide access to sample environment during presentation
- **Problem-Solution Format**: Structure each section around consultant pain points

### **Visual Strategy**

- **Screenshots**: Heavy focus on actual Kibana interface screenshots
- **Before/After**: Show messy vs. clean search results
- **Workflow Diagrams**: How logs flow from MA components to Kibana
- **Time-Series Visuals**: Log volume patterns and anomaly identification

### **Practical Takeaways**

- **Quick Reference Sheet**: Common Kibana shortcuts and search patterns
- **Troubleshooting Checklist**: Step-by-step approach to log investigation
- **Environment Access Guide**: How to get connected to client Kibana instances
- **Search Template Library**: Pre-built searches for common MA scenarios

### **Success Metrics**

By the end of this presentation, consultants should be able to:

1. Navigate Kibana independently to investigate client issues
2. Construct effective searches using time ranges, filters, and trace IDs
3. Follow transactions across multiple MA components
4. Export and share findings with technical teams
5. Set up efficient troubleshooting workflows for their implementations
---
# Last Draft:
# Elasticsearch & Kibana for Manhattan Active SCP

_What Consultants Need to Know_

## Opening Hook

**Why start here:** Set the stage with SCP-specific consultant challenges

- "It's Monday morning, Pet Supplies Plus reports their replenishment calculations aren't running, and you need to trace what happened across Forecasting, Allocation, and Replenishment modules"
- "With SCP's event-driven continuous calculations, understanding the log flow is critical for successful implementations"
_Speaker notes:_  
"Today's session will keep things simple and practical — we'll cover what Elasticsearch and Kibana are,why we use them,  and how they fit into SCP applications
 
---

## Slide 2: Objectives

✅ Why Elasticsearch is used in MA applications  
✅ How Kibana helps us troubleshoot  
✅ What SCP consultants need to know  
✅ Best practices for log analysis

_Speaker notes:_  
"My goal is not to turn you into Elasticsearch engineers — it's to give you confidence using Kibana effectively and help you understand what's happening behind the scenes."

---

## Slide 3: What is Elasticsearch?

- Distributed, RESTful search and analytics engine built on Apache Lucene
- Instead of storing information as rows of columnar data, Elasticsearch stores complex data structures serialized as JSON documents
- Near real-time indexing: when a document is stored, it's indexed and fully searchable in near real-time—within 1 second
- Uses inverted index structure that supports very fast full-text searches
- **NoSQL database** - stores data in an unstructured way

_Speaker notes:_  
"Elasticsearch is the engine that makes all MA application logs searchable. It's optimized for the kind of searching and analysis you'll need to do as consultants."

---

## Slide 4: What does it have to do with SCP?

**SCP Planning Workflows Example:**

**Simple Task:**

> "Fetch the forecast policy for item X at location Y."

```json
{
    "item": "12345", 
    "location": "DC_East",
    "forecast_method": "croston",
    "time_granularity": "weekly", 
    "seasonality": "low"
}
```

**Complex SCP Task:**

> "Determine and apply the most appropriate forecast policy for item X across multiple locations, considering historical demand variability, item lifecycle stage, promotions, planned events, and capacity constraints — and automatically trigger a re-forecast if any conditions have changed."

_Speaker notes:_  
"SCP has launched with Forecasting, Allocation and Replenishment combined in a single application. These complex planning workflows generate logs that need to be searchable for troubleshooting."

---

## Slide 5: How MA Components Work Together

**Visual Aid - Component Integration:**

```
MA Components → Logs → Elasticsearch → Kibana → You
```

**The MA Platform Challenge:**

- MA Products sit on a componentized platform of individual servers
- Components work together to execute tasks
- Each component publishes its own log statements to Elasticsearch
- Elasticsearch consolidates and indexes these messages
- Kibana permits users to query and review logs in near-real time across all components

_Speaker notes:_  
"This is from our actual documentation - MA's componentized architecture means logs come from many different sources, and Elasticsearch brings them all together."

---

## Slide 6: What is Kibana?

- Open source data visualization & exploration tool by Elastic
- **Provisioned for all Manhattan Active (MA) stacks**
- At runtime, MA applications generate logs, which are published to Kibana
- Kibana's primary utility is as a tool to view and query these logs
- Gives us insight into application behavior and troubleshooting

_Speaker notes:_  
"Every MA stack gets its own Kibana instance. This is your window into understanding what's happening in your SCP implementations."

---

## Slide 7: Basic Elasticsearch Concepts

- **Index**: Like a collection of documents (similar to a database table)
- **Document**: A single log entry stored as JSON
- **Fields**: Key-value pairs within documents (like columns in a table)
- **Inverted Index**: Data structure that lists every unique word and identifies all documents each word occurs in

_Speaker notes:_  
"You don't need to be an expert, but understanding these basic concepts helps you use Kibana more effectively."

---

## Slide 8: Using Kibana - The Discover Page

**Primary Interface for Log Analysis:**

**Key Features:**

- **Time Range Filtering**: Default shows "Last 15 minutes"
- **Document Browsing**: View logs as structured documents with key-value pairs
- **Field Selection**: Add relevant columns to results table
- **Query Bar**: Search across all fields
- **Filters**: Narrow results by specific field values

**Common Fields for Troubleshooting:**

- Log Level
- Component Name
- Message/Log content
- Trace ID (for following transactions)
- Timestamp

_Speaker notes:_  
"The Discover page is where you'll spend most of your time. These are the core features from our Kibana documentation that you'll use for troubleshooting."

---

## Slide 9: Effective Search Strategies & Best Practices 

✅ **Start with time range filtering** to limit data volume  
✅ **Use Trace ID** where available to follow workflows  
✅ **Filter out noise** (exclude DEBUG logs when not needed)  
✅ **Use absolute time ranges** when sharing with team  
✅ **Focus on Kibana interface** - no API work required  
✅ **Save useful search patterns** for reuse

_Speaker notes:_  
"These practices come from our documentation on effective Kibana usage. The key is being systematic and sharing your findings effectively."

**Query Bar Techniques:**

- Simple text search across all fields
- Quoted phrases for exact matches: `"specific error message"`
- Boolean operators: `AND`, `OR`, `NOT`
- Wildcard searches with asterisks

**Filtering Best Practices:**

- Use filters for structured data (log levels, component names)
- Use query bar for free text searching
- **Time Range**: Use absolute ranges when sharing links with team members

_Speaker notes:_  
"These techniques come directly from our browsing Kibana documentation. The key is knowing when to use filters vs. the query bar."

---

## Slide 12: Live Demo

**Screenshots to show:**

1. **Kibana Discover page** with sample logs
2. **Time range selection** and filtering
3. **Field selection** for relevant columns
4. **Query bar usage** with examples
5. **Filter application** by log level or component

**Demo Focus:**

- Navigate Kibana interface
- Perform basic log searches
- Apply useful filters
- Export or save results

_Speaker notes:_  
"We'll walk through the actual Kibana interface using the features documented in our materials. This gives you hands-on experience with the tools you'll use."

---

## Slide 13: Summary

- **Elasticsearch** = backend engine that indexes MA application logs as JSON documents
- **Kibana** = your interface for exploring and analyzing those logs
- **SCP Consultants**: Focus on using Kibana's Discover page effectively for troubleshooting
- **Key skill**: Understanding how to search, filter, and analyze logs from componentized MA applications

_Speaker notes:_  
"The main takeaway is that Kibana gives you visibility into what's happening across all MA components. For SCP implementations, this visibility is essential for troubleshooting and validation."

---

## Slide 14: Questions & Discussion

**Open floor for:**

- Kibana interface questions
- Log analysis challenges
- Access and setup questions
- Integration with SCP implementation workflows

---

## Visual Assets Needed (Based on Provided Screenshots):

✅ **Kibana Discover page** (from provided screenshots)  
✅ **Time range selector** demonstration ✅ **Query bar and filtering** examples ✅ **Field selection** interface ✅ **Log document structure** showing key-value pairs

## Key Points from Documentation:

- **MA componentized architecture** requires consolidated logging
- **Kibana provisioned for all MA stacks** with independent instances
- **Near real-time searchability** within 1 second
- **JSON document structure** for flexible log storage
- **Inverted index** enables fast full-text search