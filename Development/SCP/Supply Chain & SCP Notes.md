# 📦 Supply Chain & SCP Notes

## 1. Order Lifecycle – Statuses & Events

*Source: [[Order Lifecycle : Statuses & Events]]*

### **Order Information**

* **Order Header:** OrderId, CreatedTimestamp, OrderType, CustomerId, FirstName, LastName, Email, etc.
* **Pricing:** OrderTax, OrderCharge, Payment.
* **Extended Attributes:** Salutation, etc.

### **Base Statuses**

| Code   | Status Name    |
| ------ | -------------- |
| 1000   | Open           |
| 1500\* | Back Ordered   |
| 2000   | Allocated      |
| 3000   | Released       |
| 3500   | In Progress    |
| 3600   | Picked         |
| 3700   | Packed         |
| 7000   | Fulfilled      |
| 8000   | Pending Return |
| 8500   | Returned       |
| 9000\* | Canceled       |

*Back Ordered* and *Canceled* cannot be extended.

### **Return Statuses**

| Code    | Status Name      |
| ------- | ---------------- |
| 11000   | Pending Return   |
| 13000   | Pending Approval |
| 15000   | Received         |
| 18000   | Returned         |
| 19000\* | Canceled         |

### **Pipeline Configuration**

* **Base Pipelines:** Standard workflows.
* **Custom Pipelines:** e.g., Aigle-specific.
* Each pipeline includes:

  * **PickupService** → Services to call for each `FromStatus`.
  * **DropStatusDetermination** → Target statuses post-service.
* API Endpoints for save/configuration.

### **Order Events**

* **Ship:** Updates fulfillment, reduces inventory.
* **Short:** Moves qty to Back Ordered.
* **Pickup:** Marks fulfilled in inventory.

---

## 2. SCP Forecast Training

See also: [[Forecasting]]

*Source: [[SCP Forecast Training]]*

### **Key Concepts**

* **Inventory:** Stock of goods at various stages.
* **Forecast:** Predicting future demand.
* **Inventory Optimization:** Balancing cost & service levels.
* **Demand Metrics:** Measures for planning efficiency.

### **Tech Stack**

* Java (IntelliJ), Angular frontend, REST APIs.
* Git, Bitbucket, Jira for collaboration.
* Testing: Postman & Cucumber.
* Containerization: Docker, deployed on GCS (GKE, Cloud Run, Compute Engine).
* Frameworks: MUP, Entity Framework.

### **SCP Forecasting Setup**

1. Environment & Tool setup.
2. Multi-tenancy & Telepresence configuration.
3. Clone repos.
4. Learning Resources: IntelliJ, Java, Docker, Spring Boot.

---

## 3. PFIO Overview

*Source: [[PFIO Overview]]*

### **Components**

1. **Planning** – Strategic resource allocation.
2. **Forecasting** – Predicting demand.
3. **Inventory Optimization** – Balancing stock vs. service goals.

### **Key Inventory Concepts**

* Safety Stock, EOQ, Inventory Turnover.
* Allocation strategies (demand-based, priority-based).
* KPIs: Order fill rates, turnover.

---

## 4. Active SCP – Training Plan

*Source: [[Active SCP - Training Plan]]*

### **Training Categories**

* Supply Chain Fundamentals.
* SCP Basics: Components, Master Data, Forecasting, Replenishment.
* Deep Dives: Demand Forecasting, Replenishment, Allocation.
* Framework Knowledge: Entity Framework, Batch, Logging, Scheduler.
* Agile & BA skills.
* PE & Monitoring Training.
* API & Postman basics.

---

## 5. Life Cycle Policy

*Source: [[ASCP-Life Cycle Policy]]*

### **Purpose**

* Controls replenishment behavior based on product life stage (Active, Discontinued, Inactive).
* Impacts forecasting, ordering, lost demand estimation.

### **Hierarchy**

Enterprise → Item → ItemLocation → Life Cycle Policy.

### **Automation**

* Activation/Deactivation dates trigger policy changes automatically.
* `IsActive = False` overrides lifecycle settings in SOQ calculations.

---

## 6. Release Notes – MASCP 25.2

*Source: [[ASCP-MA SCP Release Notes v25.2]]*

### **Key Enhancements**

* **Supplier Changes:** Support subgroup edits, temporary supplier config.
* **PO Projection:** Improved with bracketing & deals.
* **Order Auto Release Enhancements:** Prevents release on IMS error.
* **Order Split:** Requirement-based & line-based.
* **Planogram:** Auto-replenish based on updated layouts.
* **Activation/Deactivation Dates:** Seasonal control of availability.
* **Bulk Update:** Across ItemLocation & Sourcing Relationship.
* **Forecast Details UI:** Unified seasonal forecast adjustments.
* **Forecast Summary:** Grouped forecast management with proportional disaggregation.
* **Upper Echelon Std Dev:** Variability analysis at higher network levels.
* **Aggregate/Manual Seasonal Profiles.**
* **Constrained Supply Allocation.**
* **New Store Modeling.**
* **MESIS:** Network-level service investment strategy.
* **Item Relationship Enhancements.**
* **Life Cycle Config Changes:** Centralized configs in global entity.
* **Seed Data Changes:** Removal of certain forecast exception types.

---
# Development Chat History - Consolidated Notes (2022-2025)

## Timeline Overview

### **2022**

#### **August 2022** - Testing & Framework Development
- Unit Course Review, Docker Course Review
- Entity Framework, **Framework implementation
- Cucumber issues resolution with terminal
- Test method development and mock data creation

#### **October 2022** - Location & Filter Development
- Create locations and filter functionality
- Test method implementation with 6 persist forecast policies
- Manual testing and QA processes
- Return last forecast policy rank implementation

#### **November 2022** - Technical Implementation
- Todo list and calendar placement for demonstrations
- Technical readiness for next Wednesday demonstrations
- Make a todo list focusing on technical stuff
- Technical demonstrations and story completion

#### **December 2022** - Testing & Coverage
- Could do curriculum test, add more than 20 locations
- Cucumber test development and forecast integration
- Page count greater than one for code coverage
- Make 40 locations and mock two pages implementation

### **2023**

#### **January 2023** - Service & Error Handling
- Recreate ad try to troubleshoot error
- Service method calling and queue management
- Creating ad hoc job to postman functionality
- Should be only about 10 lines of code
- Attend all scp meetings to update David

#### **February 2023** - Documentation & Extraction
- Extract forecast policy id from doc first
- Extract list of item ids from document
- Present refex* contains list of item ids
- Populate pboth values in forecast request dto object

#### **March 2023** - System Optimization
- Docker purge volume, remove faulty images first
- Clean up system and register with eureka attempt
- Scheduler initialization waiting for update since told it had to be tested

#### **May 2023** - Team Development
- Work giving feedback during grooming meetings
- Asking questions during standup
- Don't be afraid to question things, helps stand out

#### **August 2023** - Quality & Reviews
- Cucumber issues, solve them with terminal
- JUnit Course Review, Docker Course Review
- Entity Framework, **Framework

#### **September 2023** - Leadership & Vision
- Try to understand actual reqs and talk to BAs directly
- During meetings and calls, have voice heard
- AT+ visibility once work on few things, get better picture of scope
- Women in STEM leadership conference
- Sarah works on MuJP it, teams channel for specific questions in metadata
- Technical docs and functional docs

#### **October 2023** - JSON & Configuration
**Key Development Work**:
- Multiple JSON configuration files created and managed:
  - `ForecastActions.json`
  - `ForecastDetails.json`
  - `ForecastFilters.json`
  - `ForecastList.json`
  - `Details with 3 groups Json`

**Testing & Validation**:
- Stack trace error resolution: dates work as of 10/09/23
- Restart docker container shell work
- Change attribute names in details view and corresponding attributes
- Push changes for labels and metadata

#### **November 2022** (appears to be mislabeled, likely 2023)
- Make a todo list of technical stuff to do
- Technical demonstration preparation
- Story breakdown and calendar coordination

#### **December 2022** (appears to be mislabeled, likely 2023)
- Technical presentation setup
- MASCP Retro meeting notes and solution planning
- Set recurring meetings with Mike for support
- Ask David and Akshay for presentation nodes in grooming doc

### **2024**

#### **February 2024** - Feature Enhancement
- `ForecastSmoothing... Json` configuration
- Make sure David approves last ten days of Ramadan

#### **March 2024** - Bug Fixes & Testing
- 20 21.2-f3afe2-260328T246 issue resolution
- Breakpoint in foreach loop in updateForecastHistory
- Write test for updateForecastHistory with breakpoints
- Test and engine forecast entity getting populated correctly

#### **July 2024** - Major Development Push

##### **July 10** - PR Management
**PRs for Approval**:
- https://bitbucket.org/manhattanassociates/component-commonui-facade/pull-requests/3264
- https://bitbucket.org/manhattanassociates/ui-metadata/pull-requests/14842
- **Back End PR**: https://bitbucket.org/manhattanassociates/component-ai-forecast/pull-requests/956

##### **July 15** - Feature Flags
- **"FeatureFlag"**: "AI-36029#2025-07"
- Jul 31st Sarah birthday
- I NEED TO UPDATE RESIDENCY STUFF

##### **July 17** - Navigation Design
**"Next Story" Navigation Planning**:
From **Forecast Entity (FE) details page** → back to **parent Forecast Summary (FS) page**

**Functional Requirements Investigation**:
- Does every Forecast Entity have exactly one parent Forecast Summary?
- Confirm one-to-one relationship from FE → FS (likely many-to-one from FS → FEs)

**Technical Investigation**:
- Entity relationship: Look at how Forecast Entity (FE) knows its parent Forecast Summary (FS)
- Is this modeled clearly in entity (`ForecastEntity.getForecastSummaryId()` or equivalent)?
- Service methods: Check for existing backend service or join like `findAllForecasts`
- FE Details page context: When rendering Forecast Entity Details page, do we already load Forecast Summary ID?

**Frontend Pattern to Mimic**:
- Look at other detail pages (like Forecast Analysis Details or Item Location Analysis Details) that add "Go to parent" related links
- What's the standard UI/UX pattern for consistency?

**Suggested Checklist**:
- Confirm one-to-one relationship from FE → FS
- Identify how Forecast Summary ID is available on FE Details page
- Already loaded in page context?
- Do we need to query for it (and if so, which service/API)?
- Locate existing backend service that exposes FS ID from FE ID
- Check example UI implementations of "navigate to parent" related links for placement
- Clarify any edge cases: What happens if FE is orphaned / no parent FS?

##### **July 18** - BitBucket Integration
- Talk about: https://bitbucket.org/manhattanassociates/component-commonui-facade/pull-requests/3264/overview
- How this url is not letting me merge manually on bit bucket, do I need to do it through git instead?
- The description vs item id

##### **July 21** - Presentation Week
- https://bitbucket.org/manhattanassociates/ui-metadata/pull-requests/14842/overview
- **PRESENTATION THIS WEEK**

##### **July 24** - Communication Protocol
- Send regular updates to leads, especially when early online or late
- India and US team coordination
- Tell them what I am working on or who I talked to

##### **July 28** - Questions for Dev Time
**Dev Time Questions**:
1. **PR Approval**: AI-38584
2. **As Promo is default value in dropdown, there should not be 'Select' on the same**
   - I put this but it still isn't showing
3. **Promo Id label is not matching with validation error (event id)**
   - Is it possible to even change this? How?

##### **July 29** - Backend Validation
- Add custom validation on backend

##### **July 30** - Defect Clarification
**Hi @Milly, I had a few questions I wanted to clarify with you Regarding Defect – AI-39326**:

1. **Event vs. Promo Id Label**
   - Right now, the label shows as "Promo ID on the UI", but the entity attribute is "Event ID"
   - Since we have an existing Promotion Events page, wanted to check if that's still the correct label to use — or if it might be confusing for users

2. **Export: Event Type Id vs. Event Type Description**
   - The UI currently shows both in the export menu, and both are being exported
   - Would you prefer to only export one of them? If so, which one: the ID or the Description?

**Process Notes**:
- Ways to improve cafe: extension cables and own cafe/bar situation, more milk, aprons
- Notes: moving the subpackage does in fact break the application
- Go into devops chat and ping and ask if no one else has experienced it
- Tag people in a public chat so they can sound off
- Create a groupchat and ask as well

##### **July 30** - System Discovery
- My back end and ui stories should be different
- Make sure whole backend is working, then do UI
- Sarah and I can work on story breakdown
- When I cant get responses from people, reach out to dev lead
- I found out that the standard value displaying method that's been being done in SCP is actually incorrect
- The conditional way is actually correct way

#### **August 2024** - Process Optimization

##### **August 4** - Delivery & Communication
**Current Work**:
- Submit reimbursement
- "its not when they say they will deliver, just deliver when you say it will get delivered"
- "gain deeper understanding of something and spend more time upfront"
- Active dev logs when UI is not working, ask Milly as well

**Team Dynamics**:
- "no one dives on details, they just see the average story pts"
- "spend half a day focusing intently on stuff"
- "Next time when asked to refactor: ask to add 3 days on estimate and add notes on story"

##### **August 4** - Blocker Management Protocol
**Steps for blockers and PR Reviews**:

1. **As soon as I get an issue**:
   - Make a chat with Manager and BA and say that I am blocked until we get clarification from BA
   - Make sure we keep all of the communication in the chat with manager and BA
   - **HOLD YOURSELF TO IT** - make it someone else's issue
   - **BE VOCAL ABOUT IT IN SCRUM**
     - MENTION EXACTLY WHO YOU PINGED
   - **DRAG PEOPLE INTO MEETINGS**

2. **Confront with facts**
3. **CYA**

**Key Phrases**:
- "I am blocked, I have messaged XXX, and I have not heard back"
- "I am blocked and idk who to ping, can anyone give me a name?"

**Planning Guidelines**:
- When working unknown component: Add 3 days to the estimate
- For new components, check how long it takes for CI to run
- Use that for planning and for pushback
- Check merge permissions and if I don't, call it out on estimate

##### **August 5** - Story Completion & Team Structure
**Today's Accomplishments**:
- Finished Defect AI-39725
- Finished Story and Re-Recorded Demo Video for AI-38817
- Got a new ticket and maybe another one

**Documentation Philosophy**:
"Document Everything. So it can be shown that I was doing what I was told. And doing what I was told was right"

**Team rainmakers - cody lee [extremely knowledgeable on web dev stuff]**

**Knowledgeable folks**:
- Daniel Corely - DC Allocation
- Johnathan Rice -
- Ananth Swaminathan - outbound Execution  
- Katelyn Barnes - outbound Planning

**End of Day Protocol**:
At end of the day before I sign out, send Ramya and David a message on my progress, and tell them I will need to sign off and will not be available till tomorrow

### **2025 (Current Year)**

#### **January 2025** - Strategic Development Philosophy
**Master the scope creep move immediately** - this one's huge. The moment someone changes requirements, you stop, smile, and say "That sounds like great feedback for the next iteration. Let me finish what we scoped for this sprint first." Then you create that new ticket. This alone will probably cut your spillover in half.

**Time-box your help requests** - instead of that detailed message format (which honestly, I love and think shows great thinking), try this: "Quick question - stuck on [specific thing]. Tried X and Y. Can we hop on a 15-minute call?" Then you can give all that beautiful context verbally where it feels more collaborative.

**Build your informal support network** - that principal engineer who gets it? She's your new best friend. Ask her specifically: "Hey, when you need help with [framework thing], who do you go to and how do you approach them?" Sometimes it's not what you ask, it's who you ask and how.

**Document differently** - keep your detailed analysis skills but package them for your audience. Instead of one big document, try: "Noticed a pattern with PR reviews - would it help if we batched feedback?" Just one small suggestion at a time, positioned as helping the team, not fixing problems.

**Protect your energy** - this is survival mode, remember? Set boundaries around nights and weekends. You're not going to solve broken processes by burning yourself out. Trust me, I've tried.

## Core Technical Projects

### Forecast Summary Policy Management
**Main Feature**: Comprehensive deletion system with data integrity

**Deletion Order** (Refined May 2024):
1. `forecastSummary` [batching triggers here]
2. `forecastSummaryForecastAssociation` [separate method, pagination]
3. `forecastSummaryGroupingAttribute`
4. `forecastSummaryFilterAttribute`
5. `forecastSummaryFilterCondition`
6. `forecastSummaryPolicy`

**Technical Challenges Resolved**:
- Transaction management: `java.lang.IllegalStateException: Cannot start new transaction without ending existing transaction`
- Context management: `java.lang.IllegalStateException: TransactionContext is not active`
- Asynchronous processing for large datasets
- Error handling and rollback procedures

### Event Management System (2024)
**Comprehensive Implementation**: Full CRUD system with validation

### JSON Configuration Management (2023)
**Key Files Managed**:
- `ForecastActions.json`
- `ForecastDetails.json`
- `ForecastFilters.json`  
- `ForecastList.json`
- `ForecastSmoothing.json`

### Feature Flag Evolution
**Historical Flags**:
- `"FeatureFlag": "AI-16521W2024-12"`
- `"FeatureFlag": "AI-36029#2025-07"`
- `"DisableOutFeatureFlag": true`

## Development Environment & Tools

### System Configuration (2024)
- **ClusterName**: mtpfio01
- **WorkloadName**: com-manh-cp-ai-forecast
- **ComponentName**: ai-forecast
- **Ports**: 17401 (main), 17406 (debug)
- **ComponentSrcCodePath**: /Users/hsylla/Desktop/Desktop_April2024/components/component-ai-forecast

### Test Environment Access
- **URL**: https://omniscp01.cp.manh.cloud/scp/screenitem/items
- **Organization**: terminators
- **Credentials**: Documented in June 2024 entries

### Development Tools
- **Version Control**: Bitbucket with Git integration
- **Deployment**: Docker containers, Telepresence
- **Testing**: JUnit, Cucumber, manual QA processes
- **Monitoring**: Goblin tools (https://goblin.tools/)

## Professional Development Journey

### Skills Evolution (2022-2025)
- **2022**: Foundation building, testing frameworks, basic implementation
- **2023**: Complex JSON management, team collaboration, technical presentations
- **2024**: Advanced project management, blocker handling, scope management
- **2025**: Strategic thinking, energy management, professional boundaries

### Process Maturation
- **Early**: Basic code review and testing
- **Mid**: Systematic documentation and team communication
- **Current**: Advanced scope management and energy protection strategies

### Team Leadership Growth
- **Initial**: Individual contributor focus
- **Developing**: Cross-team collaboration and knowledge sharing
- **Advanced**: Process improvement and team optimization strategies

---

**Timeline Coverage**: 2022 - 2025 (3+ years)  
**Key Contributors**: Milly, Hawa, David, Akshay, Abhilash, Ramya, Sarah, Cody Lee, Daniel Corely, Johnathan Rice, Ananth Swaminathan, Katelyn Barnes  
**Documentation Philosophy**: "Document Everything. So it can be shown that I was doing what I was told. And doing what I was told was right"  
**Current Status (2025)**: Strategic development with emphasis on scope management and sustainable work practices


[[SCP|← Back to SCP]]
