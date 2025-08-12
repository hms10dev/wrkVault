## Option 1: Prevent Addition (Recommended)

**Modify the validation to prevent duplicates from being added to the list in the first place**

```java
private void validateForecastSummaryGroupingAttributes(Context context, ForecastSummaryPolicy entity,
        ErrorHandlerService errorHandlerService)
{
    Set<String> attributeNameSet = new HashSet<>();
    if (CollectionUtils.isNotEmpty(entity.getForecastSummaryGroupingAttributeList()))
    {
        Optional<ForecastSummaryGroupingAttribute> itemGroupingAttribute = entity.getForecastSummaryGroupingAttributeList()
                .stream().filter(attribute -> ENTITY_TYPE_ITEM.getValue().equals(attribute.getEntityType()))
                .findFirst();

        // Create a new list without duplicates
        List<ForecastSummaryGroupingAttribute> validAttributes = new ArrayList<>();
        
        for (ForecastSummaryGroupingAttribute condition : entity.getForecastSummaryGroupingAttributeList())
        {
            List<String> groupingAttributeFields = new ArrayList<>();
            groupingAttributeFields.add(condition.getEntityType());
            groupingAttributeFields.add(condition.getGroupingAttribute());
            groupingAttributeFields.add(condition.getGroupingAttributeId());
            
            // Check if this attribute is already in our valid set
            String attributeName = condition.getGroupingAttribute();
            if (attributeNameSet.add(attributeName)) {
                // Only add if it's not a duplicate
                validAttributes.add(condition);
                validateGroupingAttributesFields(context, errorHandlerService, groupingAttributeFields,
                        attributeNameSet, ForecastSummaryPolicyBase.ENTITY_NAME, itemGroupingAttribute, entity);
            }
            // Silently skip duplicates - no error thrown
        }
        
        // Update the entity with the cleaned list
        entity.setForecastSummaryGroupingAttributeList(validAttributes);
    }
}
```

## Option 2: Remove Duplicates After Detection

**As your comment suggests, manually remove the duplicate when detected**

```java
public void validateGroupingAttributesFields(Context context, ErrorHandlerService methodErrorHandlerService,
        List<String> groupingAttributeFields, Set<String> attributeNameSet, String entityName,
        Optional<ForecastSummaryGroupingAttribute> itemGroupingAttribute, ForecastSummaryPolicy entity)
{
    // ... existing validation code ...
    
    if(!attributeNameSet.add(attributeName)){
        // Instead of throwing error, remove the duplicate from the entity
        entity.getForecastSummaryGroupingAttributeList().removeIf(attr -> 
            attributeName.equals(attr.getGroupingAttribute()) && 
            // Remove the one we just processed (keep the first occurrence)
            entity.getForecastSummaryGroupingAttributeList().indexOf(attr) > 
            entity.getForecastSummaryGroupingAttributeList().stream()
                .map(ForecastSummaryGroupingAttribute::getGroupingAttribute)
                .collect(Collectors.toList()).indexOf(attributeName)
        );
        
        // Don't throw the error
        // handleGroupingAttributeErrors(context,methodErrorHandlerService,DUPLICATE_GROUPING_ATTRIBUTE,
        //         ENTITY_TYPE.getValue(),entity);
    }
}
```

## Option 3: Clean Approach with Helper Method

**Most maintainable solution**

```java
private void validateForecastSummaryGroupingAttributes(Context context, ForecastSummaryPolicy entity,
        ErrorHandlerService errorHandlerService)
{
    if (CollectionUtils.isNotEmpty(entity.getForecastSummaryGroupingAttributeList()))
    {
        // Remove duplicates first, before validation
        removeDuplicateGroupingAttributes(entity);
        
        // Then proceed with normal validation
        Set<String> attributeNameSet = new HashSet<>();
        Optional<ForecastSummaryGroupingAttribute> itemGroupingAttribute = entity.getForecastSummaryGroupingAttributeList()
                .stream().filter(attribute -> ENTITY_TYPE_ITEM.getValue().equals(attribute.getEntityType()))
                .findFirst();

        for (ForecastSummaryGroupingAttribute condition : entity.getForecastSummaryGroupingAttributeList())
        {
            List<String> groupingAttributeFields = new ArrayList<>();
            groupingAttributeFields.add(condition.getEntityType());
            groupingAttributeFields.add(condition.getGroupingAttribute());
            groupingAttributeFields.add(condition.getGroupingAttributeId());
            validateGroupingAttributesFields(context, errorHandlerService, groupingAttributeFields,
                    attributeNameSet, ForecastSummaryPolicyBase.ENTITY_NAME, itemGroupingAttribute, entity);
        }
    }
}

private void removeDuplicateGroupingAttributes(ForecastSummaryPolicy entity) {
    if (CollectionUtils.isNotEmpty(entity.getForecastSummaryGroupingAttributeList())) {
        Set<String> seen = new HashSet<>();
        List<ForecastSummaryGroupingAttribute> uniqueAttributes = entity.getForecastSummaryGroupingAttributeList()
                .stream()
                .filter(attr -> seen.add(attr.getGroupingAttribute())) // Keep first occurrence
                .collect(Collectors.toList());
        
        entity.setForecastSummaryGroupingAttributeList(uniqueAttributes);
    }
}
```

Ah, I see! Looking at the interface, there's no `setForecastSummaryGroupingAttributeList()` method - only methods to manipulate individual items. This is a **read-only list** managed through individual CRUD operations.

Looking at the available methods:

- `getForecastSummaryGroupingAttributeList()` - returns the list
- `createForecastSummaryGroupingAttribute(key)` - adds a new one
- `removeForecastSummaryGroupingAttribute(attribute)` - removes one
- `clearForecastSummaryGroupingAttributeList()` - clears all

## Updated Solution: Remove Duplicates During Validation

Since we can't replace the whole list, we need to **remove duplicates** when we detect them:

```java
public void validateGroupingAttributesFields(Context context, ErrorHandlerService methodErrorHandlerService,
        List<String> groupingAttributeFields, Set<String> attributeNameSet, String entityName,
        Optional<ForecastSummaryGroupingAttribute> itemGroupingAttribute, ForecastSummaryPolicy entity)
{
    String attributeName = null;

    // ... existing validation code ...

    attributeName = groupingAttributeFields.get(1);

    if (attributeName.isEmpty())
    {
        handleGroupingAttributeErrors(context, methodErrorHandlerService, GROUPING_ATTRIBUTE_REQUIRED_FIELD_ERROR,
                ENTITY_TYPE.getValue(), entity);
    }
    // ... other validations ...

    // Check for duplicates and remove them silently
    if(!attributeNameSet.add(attributeName)){
        // Find and remove the duplicate we just encountered
        String currentAttributeName = attributeName;
        entity.getForecastSummaryGroupingAttributeList().removeIf(attr -> 
            currentAttributeName.equals(attr.getGroupingAttribute()) && 
            // Remove duplicates beyond the first occurrence
            isDuplicateOccurrence(entity.getForecastSummaryGroupingAttributeList(), attr, currentAttributeName)
        );
        
        // Don't throw the error - silently handle the duplicate
        // handleGroupingAttributeErrors(context,methodErrorHandlerService,DUPLICATE_GROUPING_ATTRIBUTE,
        //         ENTITY_TYPE.getValue(),entity);
    }
}

// Helper method to determine if this is a duplicate occurrence
private boolean isDuplicateOccurrence(List<ForecastSummaryGroupingAttribute> list, 
                                     ForecastSummaryGroupingAttribute current, 
                                     String attributeName) {
    int currentIndex = list.indexOf(current);
    int firstOccurrenceIndex = -1;
    
    for (int i = 0; i < list.size(); i++) {
        if (attributeName.equals(list.get(i).getGroupingAttribute())) {
            firstOccurrenceIndex = i;
            break;
        }
    }
    
    return currentIndex > firstOccurrenceIndex;
}
```

## Alternative: Cleaner Approach with Pre-Processing

Or, clean duplicates **before** validation starts:

```java
private void validateForecastSummaryGroupingAttributes(Context context, ForecastSummaryPolicy entity,
        ErrorHandlerService errorHandlerService)
{
    if (CollectionUtils.isNotEmpty(entity.getForecastSummaryGroupingAttributeList()))
    {
        // Remove duplicates first
        removeDuplicateGroupingAttributes(entity);
        
        // Then proceed with normal validation
        Set<String> attributeNameSet = new HashSet<>();
        Optional<ForecastSummaryGroupingAttribute> itemGroupingAttribute = entity.getForecastSummaryGroupingAttributeList()
                .stream().filter(attribute -> ENTITY_TYPE_ITEM.getValue().equals(attribute.getEntityType()))
                .findFirst();

        for (ForecastSummaryGroupingAttribute condition : entity.getForecastSummaryGroupingAttributeList())
        {
            List<String> groupingAttributeFields = new ArrayList<>();
            groupingAttributeFields.add(condition.getEntityType());
            groupingAttributeFields.add(condition.getGroupingAttribute());
            groupingAttributeFields.add(condition.getGroupingAttributeId());
            validateGroupingAttributesFields(context, errorHandlerService, groupingAttributeFields,
                    attributeNameSet, ForecastSummaryPolicyBase.ENTITY_NAME, itemGroupingAttribute, entity);
        }
    }
}

private void removeDuplicateGroupingAttributes(ForecastSummaryPolicy entity) {
    if (CollectionUtils.isNotEmpty(entity.getForecastSummaryGroupingAttributeList())) {
        Set<String> seen = new HashSet<>();
        List<ForecastSummaryGroupingAttribute> toRemove = new ArrayList<>();
        
        for (ForecastSummaryGroupingAttribute attr : entity.getForecastSummaryGroupingAttributeList()) {
            if (!seen.add(attr.getGroupingAttribute())) {
                // This is a duplicate - mark for removal
                toRemove.add(attr);
            }
        }
        
        // Remove all duplicates
        for (ForecastSummaryGroupingAttribute duplicate : toRemove) {
            entity.removeForecastSummaryGroupingAttribute(duplicate);
        }
    }
}
```

## Which Approach?

 So there are **two separate duplicate validations** needed:

1. **Duplicate grouping attributes** (already handled) - can't have multiple "ItemId" entries
2. **Duplicate sequence numbers** (new requirement) - can't have Item sequence=1 AND Location sequence=1

Looking at the existing code, I can see there's already some sequence validation in `validateForecastSummarySequence()`, but it's grouping by entity type first, which would allow duplicates across Item/Location.

## Updated Solution

Here's how to fix both issues:

```java
private void validateForecastSummaryGroupingAttributes(Context context, ForecastSummaryPolicy entity,
        ErrorHandlerService errorHandlerService)
{
    if (CollectionUtils.isNotEmpty(entity.getForecastSummaryGroupingAttributeList()))
    {
        // Remove duplicates first (both attribute and sequence duplicates)
        removeDuplicateGroupingAttributes(entity);
        removeDuplicateSequences(entity);
        
        // Then proceed with normal validation
        Set<String> attributeNameSet = new HashSet<>();
        Optional<ForecastSummaryGroupingAttribute> itemGroupingAttribute = entity.getForecastSummaryGroupingAttributeList()
                .stream().filter(attribute -> ENTITY_TYPE_ITEM.getValue().equals(attribute.getEntityType()))
                .findFirst();

        for (ForecastSummaryGroupingAttribute condition : entity.getForecastSummaryGroupingAttributeList())
        {
            List<String> groupingAttributeFields = new ArrayList<>();
            groupingAttributeFields.add(condition.getEntityType());
            groupingAttributeFields.add(condition.getGroupingAttribute());
            groupingAttributeFields.add(condition.getGroupingAttributeId());
            validateGroupingAttributesFields(context, errorHandlerService, groupingAttributeFields,
                    attributeNameSet, ForecastSummaryPolicyBase.ENTITY_NAME, itemGroupingAttribute, entity);
        }
    }
}

private void removeDuplicateGroupingAttributes(ForecastSummaryPolicy entity) {
    if (CollectionUtils.isNotEmpty(entity.getForecastSummaryGroupingAttributeList())) {
        Set<String> seen = new HashSet<>();
        List<ForecastSummaryGroupingAttribute> toRemove = new ArrayList<>();
        
        for (ForecastSummaryGroupingAttribute attr : entity.getForecastSummaryGroupingAttributeList()) {
            if (!seen.add(attr.getGroupingAttribute())) {
                // This is a duplicate attribute - mark for removal
                toRemove.add(attr);
            }
        }
        
        // Remove all duplicate attributes
        for (ForecastSummaryGroupingAttribute duplicate : toRemove) {
            entity.removeForecastSummaryGroupingAttribute(duplicate);
        }
    }
}

private void removeDuplicateSequences(ForecastSummaryPolicy entity) {
    if (CollectionUtils.isNotEmpty(entity.getForecastSummaryGroupingAttributeList())) {
        Set<Integer> seenSequences = new HashSet<>();
        List<ForecastSummaryGroupingAttribute> toRemove = new ArrayList<>();
        
        for (ForecastSummaryGroupingAttribute attr : entity.getForecastSummaryGroupingAttributeList()) {
            Integer sequence = attr.getSequence();
            if (sequence != null && !seenSequences.add(sequence)) {
                // This is a duplicate sequence across Item/Location - mark for removal
                toRemove.add(attr);
            }
        }
        
        // Remove all duplicate sequences
        for (ForecastSummaryGroupingAttribute duplicate : toRemove) {
            entity.removeForecastSummaryGroupingAttribute(duplicate);
        }
    }
}
```

## Also Update the Existing Sequence Validation

The current `validateForecastSummarySequence()` method needs to be updated to check for duplicates **across** entity types, not within them:

```java
public void validateForecastSummarySequence(Context context, ForecastSummaryPolicy entity,
        ErrorHandlerService methodErrorHandlerService, List<ForecastSummaryGroupingAttribute> groupingAttributes)
{
    if (CollectionUtils.isNotEmpty(entity.getForecastSummaryGroupingAttributeList()))
    {
        // Validate individual sequences are > 0
        for (ForecastSummaryGroupingAttribute groupingAttribute : entity.getForecastSummaryGroupingAttributeList())
        {
            Integer sequence = groupingAttribute.getSequence();
            if (sequence != null && sequence < 1)
            {
                Map<String, Object> parameter = Collections.singletonMap(
                        ForecastSummaryGroupingAttributeBase.Fields.SEQUENCE.getCode(), sequence);
                errorHandlerService.collectError(context, INVALID_SEQUENCE_NUMBER.getCode(), parameter);
                logger.error(() -> MessageFormat.format(
                        "--validateForecastSummarySequence() Sequence - {0} must be greater than 0 in ForecastSummaryPolicyId - {1}",
                        sequence, entity.getForecastSummaryPolicyId()));
            }
        }
        
        // Check for duplicate sequences ACROSS all entity types (Item + Location)
        Map<Integer, Long> sequenceCounts = groupingAttributes.stream()
                .filter(attribute -> attribute.getSequence() != null)
                .collect(Collectors.groupingBy(
                    ForecastSummaryGroupingAttribute::getSequence, 
                    Collectors.counting()));
                    
        sequenceCounts.forEach((sequence, count) -> {
            if (count > 1) {
                Map<String, Object> parameter = Collections.singletonMap(
                        ForecastSummaryPolicyBase.Fields.FORECAST_SUMMARY_POLICY_ID.getCode(),
                        entity.getForecastSummaryPolicyId());
                errorHandlerService.collectError(context, ErrorCode.INVALID_SEQUENCE_NUMBER.getCode(), parameter);
                logger.error(() -> MessageFormat.format(
                        "--validate() duplicate Sequence Number {0} across Item/Location in ForecastSummaryPolicyId {1}.",
                        sequence, entity.getForecastSummaryPolicyId()));
            }
        });
    }
}
```

still getting

 |Error Code|Error Description|
|---|---|
|FRC::00071|Each Grouping Attribute can only be selected once for the same forecast summary policy.|
|FRC::00071|Each Grouping Attribute can only be selected once for the same forecast summary policy.|

I see the issue! You're still calling `handleGroupingAttributeErrors()` in the `removeDuplicate*` methods, which is **adding the errors** to the error handler. The whole point was to remove duplicates **silently** without showing errors to the user.

## Fix: Remove the Error Calls

Update your `removeDuplicate*` methods to **not** call `handleGroupingAttributeErrors`:

```java
private void removeDuplicateSequences(ForecastSummaryPolicy entity, Context context, ErrorHandlerService methodErrorHandlerService){
    if(CollectionUtils.isNotEmpty((entity.getForecastSummaryGroupingAttributeList()))){
        Set<Integer> seen = new HashSet<>();
        List<ForecastSummaryGroupingAttribute> toRemove = new ArrayList<>();

        for(ForecastSummaryGroupingAttribute attribute:
                entity.getForecastSummaryGroupingAttributeList()){
            Integer sequence = attribute.getSequence();
            if(sequence != null && !seen.add(sequence)){
                // DON'T call handleGroupingAttributeErrors - just mark for removal
                // handleGroupingAttributeErrors(context,methodErrorHandlerService,ErrorCode.INVALID_SEQUENCE_NUMBER,
                //         ENTITY_TYPE.getValue(),entity);
                toRemove.add(attribute);
            }
        }
        for(ForecastSummaryGroupingAttribute duplicate : toRemove){
            entity.removeForecastSummaryGroupingAttribute(duplicate);
        }
    }
}

private void removeDuplicateGroupingAttributes(ForecastSummaryPolicy entity, Context context, ErrorHandlerService methodErrorHandlerService){
    if(CollectionUtils.isNotEmpty((entity.getForecastSummaryGroupingAttributeList()))){
        Set<String> seen = new HashSet<>();
        List<ForecastSummaryGroupingAttribute> toRemove = new ArrayList<>();

        for(ForecastSummaryGroupingAttribute attribute:
        entity.getForecastSummaryGroupingAttributeList()){
            if(!seen.add(attribute.getGroupingAttribute())){
                // DON'T call handleGroupingAttributeErrors - just mark for removal
                // handleGroupingAttributeErrors(context,methodErrorHandlerService,DUPLICATE_GROUPING_ATTRIBUTE,
                //         ENTITY_TYPE.getValue(),entity);
                toRemove.add(attribute);
            }
        }
        for(ForecastSummaryGroupingAttribute duplicate : toRemove){
            entity.removeForecastSummaryGroupingAttribute(duplicate);
        }
    }
}
```

## Also Remove the Duplicate Check in validateGroupingAttributesFields

Since you're now handling duplicates **before** validation, you should also remove the duplicate check in `validateGroupingAttributesFields`:

```java
public void validateGroupingAttributesFields(Context context, ErrorHandlerService methodErrorHandlerService,
        List<String> groupingAttributeFields, Set<String> attributeNameSet, String entityName,
        Optional<ForecastSummaryGroupingAttribute> itemGroupingAttribute, ForecastSummaryPolicy entity)
{
    String attributeName = null;

    // ... existing validation code ...

    attributeName = groupingAttributeFields.get(1);

    if (attributeName.isEmpty())
    {
        handleGroupingAttributeErrors(context, methodErrorHandlerService, GROUPING_ATTRIBUTE_REQUIRED_FIELD_ERROR,
                ENTITY_TYPE.getValue(), entity);
    }
    // ... other validation ...

    // REMOVE THIS BLOCK - duplicates are already handled in removeDuplicateGroupingAttributes
    // if(!attributeNameSet.add(attributeName)){
    //     handleGroupingAttributeErrors(context,methodErrorHandlerService,DUPLICATE_GROUPING_ATTRIBUTE,
    //             ENTITY_TYPE.getValue(),entity);
    // }
    
    // Just add to the set for tracking, but don't check for duplicates
    attributeNameSet.add(attributeName);
}
```




--- 

Okay but I thought I was suposed to show the errors?

also now it just leaves sequence number blank and throwing the error even when the grouping attributes are not the same.

am I getting grouping types and grouping attributes mixed up ??



I can see several issues in your updated validator code. Let me help you fix them:

## Issues I Found

### Issue 1: Sequence Validation Logic is Wrong

You added this check:

```java
if (StringUtils.isEmpty(String.valueOf(groupingAttribute.getSequence())) || "null".equalsIgnoreCase(String.valueOf(groupingAttribute.getSequence()))) {
    handleGroupingAttributeErrors(context, methodErrorHandlerService, GROUPING_ATTRIBUTE_REQUIRED_FIELD_ERROR, "Sequence", entity);
}
```

This is problematic because:

- `String.valueOf(null)` returns `"null"` (the string), not an empty string
- You're treating sequence as required, but your screenshot shows it can be blank
- You removed the duplicate removal methods we added

### Issue 2: Missing Duplicate Removal

You removed the `removeDuplicateGroupingAttributes()` and `removeDuplicateSequences()` methods that we added to fix the original problem.

### Issue 3: Duplicate Check Still Present

The duplicate check in `validateGroupingAttributesFields()` is still there and will cause the same error messages.

## Fixed Code

Here's the corrected version:

```java
private void validateForecastSummaryGroupingAttributes(Context context, ForecastSummaryPolicy entity,
        ErrorHandlerService errorHandlerService)
{
    if (CollectionUtils.isNotEmpty(entity.getForecastSummaryGroupingAttributeList()))
    {
        // Remove duplicates BEFORE validation (silently)
        removeDuplicateGroupingAttributes(entity);
        removeDuplicateSequences(entity);
        
        Set<String> attributeNameSet = new HashSet<>();
        Optional<ForecastSummaryGroupingAttribute> itemGroupingAttribute = entity.getForecastSummaryGroupingAttributeList()
                .stream().filter(attribute -> ENTITY_TYPE_ITEM.getValue().equals(attribute.getEntityType()))
                .findFirst();

        for (ForecastSummaryGroupingAttribute condition : entity.getForecastSummaryGroupingAttributeList())
        {
            List<String> groupingAttributeFields = new ArrayList<>();
            groupingAttributeFields.add(condition.getEntityType());
            groupingAttributeFields.add(condition.getGroupingAttribute());
            groupingAttributeFields.add(condition.getGroupingAttributeId());
            validateGroupingAttributesFields(context, errorHandlerService, groupingAttributeFields,
                    attributeNameSet, ForecastSummaryPolicyBase.ENTITY_NAME, itemGroupingAttribute, entity);
        }
    }
}

public void validateForecastSummarySequence(Context context, ForecastSummaryPolicy entity,
        ErrorHandlerService methodErrorHandlerService, List<ForecastSummaryGroupingAttribute> groupingAttributes)
{
    if (CollectionUtils.isNotEmpty(entity.getForecastSummaryGroupingAttributeList()))
    {
        for (ForecastSummaryGroupingAttribute groupingAttribute : entity.getForecastSummaryGroupingAttributeList())
        {
            Integer sequence = groupingAttribute.getSequence();
            
            // Only validate if sequence is provided (since it can be optional based on your screenshot)
            if (sequence != null && sequence < 1)
            {
                Map<String, Object> parameter = Collections.singletonMap(
                        ForecastSummaryGroupingAttributeBase.Fields.SEQUENCE.getCode(), sequence);
                methodErrorHandlerService.collectError(context, INVALID_SEQUENCE_NUMBER.getCode(), parameter);
                logger.error(() -> MessageFormat.format(
                        "--validateForecastSummarySequence() Sequence - {0} must be greater than 0 in ForecastSummaryPolicyId - {1}",
                        sequence, entity.getForecastSummaryPolicyId()));
            }
        }
    }
    
    // Check for duplicate sequences across ALL entity types (not within entity types)
    Map<Integer, Long> sequenceCounts = groupingAttributes.stream()
            .filter(attribute -> attribute.getSequence() != null)
            .collect(Collectors.groupingBy(
                ForecastSummaryGroupingAttribute::getSequence, 
                Collectors.counting()));
                
    sequenceCounts.forEach((sequence, count) -> {
        if (count > 1) {
            Map<String, Object> parameter = Collections.singletonMap(
                    ForecastSummaryPolicyBase.Fields.FORECAST_SUMMARY_POLICY_ID.getCode(),
                    entity.getForecastSummaryPolicyId());
            methodErrorHandlerService.collectError(context, ErrorCode.INVALID_SEQUENCE_NUMBER.getCode(), parameter);
            logger.error(() -> MessageFormat.format(
                    "--validate() duplicate Sequence Number {0} across all grouping attributes in ForecastSummaryPolicyId {1}.",
                    sequence, entity.getForecastSummaryPolicyId()));
        }
    });
}

public void validateGroupingAttributesFields(Context context, ErrorHandlerService methodErrorHandlerService,
        List<String> groupingAttributeFields, Set<String> attributeNameSet, String entityName,
        Optional<ForecastSummaryGroupingAttribute> itemGroupingAttribute, ForecastSummaryPolicy entity)
{
    String attributeName = null;

    if (!(StringUtils.equals(ENTITY_TYPE_ITEM.getValue(), groupingAttributeFields.get(0)) || StringUtils.equals(
            ENTITY_TYPE_LOCATION.getValue(), groupingAttributeFields.get(0))))
    {
        handleGroupingAttributeErrors(context, methodErrorHandlerService,
                INVALID_ENTITY_TYPE_ERROR_FORECAST_SUMMARY_POLICY, ENTITY_TYPE.getValue(), entity);
    }

    attributeName = groupingAttributeFields.get(1);

    if (attributeName.isEmpty())
    {
        handleGroupingAttributeErrors(context, methodErrorHandlerService, GROUPING_ATTRIBUTE_REQUIRED_FIELD_ERROR,
                ENTITY_TYPE.getValue(), entity);
    }
    else if (!ENTITY_TYPE_ITEM.getValue().equals(groupingAttributeFields.get(0)) && !ENTITY_TYPE_LOCATION.getValue()
            .equals(groupingAttributeFields.get(0)))
    {
        handleGroupingAttributeErrors(context, methodErrorHandlerService,
                INVALID_ENTITY_TYPE_ERROR_FORECAST_SUMMARY_POLICY, ENTITY_TYPE.getValue(), entity);
    }

    if (ENTITY_TYPE_ITEM.getValue().equals(ENTITY_TYPE.getValue()) && !itemGroupingAttribute.isPresent())
    {
        handleGroupingAttributeErrors(context, methodErrorHandlerService,
                FORECAST_SUMMARY_ITEM_GROUPING_ATTRIBUTE_REQUIRED, ENTITY_TYPE.getValue(), entity);
    }
    
    // REMOVE THE DUPLICATE CHECK - handled in removeDuplicateGroupingAttributes()
    // Just add to set for tracking
    attributeNameSet.add(attributeName);
}

// Add these helper methods back
private void removeDuplicateGroupingAttributes(ForecastSummaryPolicy entity) {
    if (CollectionUtils.isNotEmpty(entity.getForecastSummaryGroupingAttributeList())) {
        Set<String> seen = new HashSet<>();
        List<ForecastSummaryGroupingAttribute> toRemove = new ArrayList<>();

        for (ForecastSummaryGroupingAttribute attribute : entity.getForecastSummaryGroupingAttributeList()) {
            if (!seen.add(attribute.getGroupingAttribute())) {
                toRemove.add(attribute);
            }
        }
        
        for (ForecastSummaryGroupingAttribute duplicate : toRemove) {
            entity.removeForecastSummaryGroupingAttribute(duplicate);
        }
    }
}

private void removeDuplicateSequences(ForecastSummaryPolicy entity) {
    if (CollectionUtils.isNotEmpty(entity.getForecastSummaryGroupingAttributeList())) {
        Map<Integer, List<ForecastSummaryGroupingAttribute>> sequenceGroups = new HashMap<>();
        
        for (ForecastSummaryGroupingAttribute attribute : entity.getForecastSummaryGroupingAttributeList()) {
            Integer sequence = attribute.getSequence();
            if (sequence != null) {
                sequenceGroups.computeIfAbsent(sequence, k -> new ArrayList<>()).add(attribute);
            }
        }
        
        for (List<ForecastSummaryGroupingAttribute> attributesWithSameSequence : sequenceGroups.values()) {
            if (attributesWithSameSequence.size() > 1) {
                // Remove all but the first one
                for (int i = 1; i < attributesWithSameSequence.size(); i++) {
                    entity.removeForecastSummaryGroupingAttribute(attributesWithSameSequence.get(i));
                }
            }
        }
    }
}
```

## Key Changes:

1. **Sequence is optional** - no required field validation for blank sequences
2. **Silent duplicate removal** - no error messages for duplicates
3. **Cross-entity sequence validation** - sequences must be unique across Item AND Location
4. **Proper duplicate handling** - removes duplicates before validation runs

This should fix both the error messages and the blank sequence issue you're seeing.