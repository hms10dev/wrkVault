# Tues March 11 – Forecast Summary Policies Meeting

Related training: [[Training/Enterprise Supply Chain Management/Enterprise Supply Chain Management|Enterprise Supply Chain Management Book Log]]

## 1. Context & Overall Discussion
- Conversation centered on Forecast Summary Policies, grouping attributes, UI wizard flow, and validations.
- Reviewed design differences between preactive setup and current approach.
- Addressed technical feasibility of certain wizard configurations with UI team feedback pending.
- Discussed validation rules for grouping attributes, especially null handling.
- Talked through filters, exports, and field additions in the FE list and forecast summary screens.

## 2. Key Decisions & Agreements
- Null should not be allowed in grouping lists; either no grouping attribute ("all") or specific attributes.
- Add validation to disallow null grouping attributes.
- Ensure item grouping attribute is required; location grouping attribute optional.
- Grouping attribute must be unique for a given parent summary ID.
- Grouping entity choice (item/location) must be made early due to backend entity save structure.
- Sequence ID can default to next number; exact numeric value not functionally critical.
- Add export data loader for forecast summaries and policies.
- Related link navigation from FE entity to parent summary depends on backend field availability; may require association table.
- Add new filter `itemGroupingAttribute`.
- Keep grouping attribute values in place; ensure clarity in UI display.

## 3. Tasks & Story Breakdown
- **Story 1: Filters & Field Additions**
  - Add item grouping attribute field to left filter panel.
  - Ensure grouping attribute values are displayed properly in FE list.
  - Include export loader for forecast summaries.
  - Update relevant Confluence documentation for field definitions.
- **Story 2: Validations**
  - Disallow null in grouping attribute list.
  - Ensure at least one grouping attribute if item-level grouping.
  - Grouping attribute uniqueness validation.
  - Sequence ID default logic (auto-increment or user entry validation).
- **Story 3: Wizard Tooltip Updates**
  - Correct tooltip in step 1.
  - Add additional tooltips in remaining wizard steps.

## 4. Open Questions / Pending Items
- UI team feedback on whether wizard can support grouping attribute choice at multiple steps for the same entity.
- Confirm technical feasibility of related link navigation without direct FE field in entity.
- Validate wildcard filtering support for new grouping attribute fields.
- Verify with QE/testing if validations will be manual test cases or automated.

## 5. Additional Context / Side Notes
- Ramadan fasting discussion (13-hour fast, behavior/character improvement focus, exemptions for certain cases).
- Historical note on promo lift modeling vs. event lift: promo lift runs on-the-fly but design must stay flexible for future rule additions; event lift historically required pre-calculation due to large data sets.

Related:
- [[Meetings/Quick Sync on Forecast Summary UI Behavior & Validation Flow|Forecast Summary UI Validation]]
- [[Development/SCP/Demand Cleansing Notes|Demand Cleansing Notes]]
