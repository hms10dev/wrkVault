# Identify Hardcoded Lifecycle Statuses

Relevant Ticket: AI-20833
End Date: November 15, 2024 3:00 PM (EST)
Focus Time: 4
Status: In progress

### 1. **Identify Hardcoded Lifecycle Statuses**

- **Task**: Review the codebase of demand cleansing, seasonal profiling, and forecast initialization/update modules to locate any instances where lifecycle statuses (`Active`, `Inactive`, `Discontinued`, etc.) are hardcoded.
- **Subtasks**:
    - Search for keywords such as =="Active,"== =="Inactive,"== =="Discontinued"== directly in the code.
    - Look for _if-else conditions_, _switch cases_, __or__ any other logic that handles these statuses.
    - Check both function parameters and return values for hardcoded status values.

### 2. **Document Findings**

- **Task**: Create a document or spreadsheet listing each occurrence of hardcoded lifecycle statuses.
- **Subtasks**:
    - Note the file path and line number for each occurrence.
    - Briefly describe the context (e.g., "used in conditional statement," "status assigned as default value").
    - Indicate the potential impact or complexity of removing the hardcoding.

| File Path | line # | Code | Context | impact |
| --- | --- | --- | --- | --- |
| com/manh/cp/ai/forecast/engine/legacy/service/DemandCleansingBatchProcessor.java | 452 | `if (productLocation.getStatus() != null && productLocation.getStatus().equals("INACTIVE"))` |  |  |
| com/manh/cp/ai/forecast/engine/legacy/service/DemandCleansingBatchProcessor.java | 457 | `if (originalHistory == null && !demandClassification.isInActive())` |  |  |
| com/manh/cp/ai/forecast/engine/legacy/service/DemandCleansingBatchProcessor.java | 478 | `if (!demandClassification.isInActive())` |  |  |
| com/manh/cp/ai/forecast/engine/legacy/service/DemandCleansingBatchProcessor.java | 546 | `if (!zeroFilledList.isEmpty() && !demandClassification.isInActive() && !demandClassification.isNew())` |  |  |
| com/manh/cp/ai/forecast/engine/legacy/service/DemandCleansingBatchProcessor.java | 832 | `if (demandClassification.isInActive()){` |  |  |
| com/manh/cp/ai/forecast/engine/legacy/domain/EngineDemandCleansingResult.java | 351 | `demandCleansingResult.setInactive(engineDemandCleansingResult.isInActive());` |  |  |
| com/manh/cp/ai/forecast/engine/legacy/service/SPGenBatchProcessor.java | 1015 | `if (seasonalProfile.getDemandClassification().isInActive())` |  |  |
| com/manh/cp/ai/forecast/engine/legacy/service/SPGenBatchProcessor.java | 1107 | `if (!seasonalProfile.getDemandClassification().isInActive())` |  |  |
| com/manh/cp/ai/forecast/engine/legacy/domain/ForecastStatusEnum.java | File | `public static ForecastStatusEnum getByStatusId(String statusId){    for (ForecastStatusEnum e : *values*())    {        if (e.statusId.equals(statusId))            return e;    }    return null;}` |  |  |
