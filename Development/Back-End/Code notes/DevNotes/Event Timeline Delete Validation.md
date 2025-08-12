
## 🔎 **What this requirement means:**

When a delete action is attempted:

- If the **Event** is associated with any records in `Event Timeline` or `Event Timeline Details`:
    
    - **Block deletion**
        
    - Display this message:
        
        > "Deleting an event that is already associated to Event Timeline and Event Timeline Details is not permitted. The corresponding Event Timeline and Event Timeline Details records must first be deleted."
        
- If **no association exists**, allow deletion as normal.
    

---

## 📝 **How to implement this:**

### 1️⃣ **Backend: Add validation logic in service layer**

Even if MUP lets you control some UI behavior, this type of validation is fundamentally a **business rule** that should live on the backend (to avoid UI-only enforcement).

In your `EventService.deleteEvent(eventId)`:

```java
@Transactional
public void deleteEvent(String eventId) {
    Event event = eventRepository.findById(eventId)
        .orElseThrow(() -> new EntityNotFoundException("Event not found"));

    boolean hasTimeline = eventTimelineRepository.existsByEventId(eventId);
    boolean hasTimelineDetails = eventTimelineDetailsRepository.existsByEventId(eventId);

    if (hasTimeline || hasTimelineDetails) {
        throw new BusinessValidationException(
            "Deleting an event that is already associated to Event Timeline and Event Timeline Details is not permitted. The corresponding Event Timeline and Event Timeline Details records must first be deleted."
        );
    }

    eventRepository.delete(event);
}
```

---

### 2️⃣ **Frontend: MUP UI behavior**

Since MUP automatically binds to backend responses, this can remain minimal on UI:

- Ensure that **any `400`/`422` error coming back from your backend validation displays properly in MUP as an error message popup or inline error on the grid.
    

---

### 3️⃣ **Test case reminder**

- Test deleting:
    
    - ✅ Event with no associations: deletion should succeed.
        
    - ❌ Event with associated `EventTimeline` or `EventTimelineDetails`: deletion should fail and show the specific message.
        

---

✅ **Summary of steps you should take:**  
1️⃣ Implement `deleteEvent` validation in `EventService`  
2️⃣ Ensure your backend throws an appropriate error with that message if the condition is met  
3️⃣ Make sure MUP UI properly renders error responses from backend delete attempts (MUP should do this automatically with standard error handling)

---

# Questions:
> so I noticed entities with type master don't have any services generated for them . why is that?
> and if that is the case:
> 
> I confirmed with Sara that the validation actually does have to be completed on the backend. so if there is no service for the Event Entity, would I put that validation logic on the Event Type  config entity ? 
> 
> especially since as described, the event type Entity  determines the logic on how to configure the event policy and rules associated with the event
> 
> thank you ! 

---
# Other Notes:


EVENT_DELETE_VALIDATION_ERROR("FRC::00077");

{
  "ErrorDefinitionId": "FRC::00077",
  "ErrorText": "Deleting an event that is already associated to Event Timeline and Event Timeline Details is not permitted. The corresponding Event Timeline and Event Timeline Details records must first be deleted.",
  "ShortErrorText": "Event cannot be deleted due to associated timelines.",
  "DefaultErrorLevelId": "ERROR",
  "MinErrorLevelId": "ERROR",
  "MaxErrorLevelId": "ERROR"
}


---
So we gotta override the delete and put the validation in there, which will call the error code