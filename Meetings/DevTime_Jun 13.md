### Related Meeting:
[[Quick Sync on Forecast Summary UI Behavior & Validation Flow]]

### 🎯 **Main Issue:**

The UI continues to display deleted or invalid grouping attributes after backing out of the input screen, even though they are correctly removed from the backend and not persisted in the database.

---

### 🧩 **Key Findings:**

- The issue **only happens when the user backs out (via “X” or back button)** instead of using “Save and Continue.”
    
- The UI **preserves temporary state**, making it seem like the entry still exists even after deletion.
    
- The **backend is functioning correctly**; invalid or duplicate entries are not persisted.
    
- The problem is a **UI-side behavior**, possibly due to **framework design** intending to preserve user input state across multi-step workflows.
    

---

### 💡 **Discussion Points & Suggestions:**

1. **Validation Behavior:**
    
    - Validation happens in two places: during creation and again at save time.
        
    - Even if duplicates appear in the UI temporarily, the save operation **correctly blocks them** from persisting.
        
2. **Interim Solution:**
    
    - Users should **back out one step**, switch the drop-down value (item ↔ location), or **manually delete** the duplicate before proceeding.
        
    - Add **clear error messages** to help users identify which entry is causing issues.
        
    - **Message prompt** could guide users to go back and fix duplicates if present.
        
3. **Recommended UX Fix (if possible):**
    
    - Combine the two current steps (selecting item/location and setting sequence) into **a single screen** so users can make changes without needing to backtrack.
        
    - Let users **swap the attribute value** on the same screen when a validation error occurs.
        
4. **Next Steps:**
    
    - Hawa to:
        
        - Show the current behavior and fix to Milly.
            
        - Confirm if the workaround (backtracking and manual deletion) is acceptable.
            
        - Ensure enhanced error messages are correctly showing.
            
    - Sarah to:
        
        - Reach out to the framework team to confirm if this is expected behavior or a bug.
            
        - Share the defect link to help escalate or log a formal UI defect if needed.
            

---

### ✅ **Conclusion:**

- Backend logic is correct; issue lies with **UI temporarily preserving invalid state**.
    
- **No further changes are required** unless Milly requests a different UX.
    
- Await response from framework team to determine if a permanent fix is possible.
    

---

## Email to Milly:

**Subject:** Quick Sync on Forecast Summary UI Behavior & Validation Flow

Hi Milly,

Hope you're doing well! I wanted to quickly run something by you regarding the forecast summary grouping attribute behavior—specifically around how the UI handles entries when a user backs out of the add/edit flow. 
(Defect: [https://manhattanassociates.atlassian.net/browse/AI-34333](https://manhattanassociates.atlassian.net/browse/AI-34333 "https://manhattanassociates.atlassian.net/browse/ai-34333"))

Here’s what’s happening:

- When a user adds a duplicate grouping attribute and backs out (via the X or back button), the UI still temporarily preserves the invalid entry,even though it’s not saved to the database.
    
- The backend validation correctly blocks duplicates from being persisted, but the UI maintains the unsaved state, which may confuse users.
    
- We've implemented logic so that users cannot proceed unless they delete the duplicate or go back and change the dropdown selection (e.g., from "Item" to "Location").
    
- I've also added validation messaging, though I’m following up on ensuring the correct error message appears on the front end.
    

**Potential Next Steps:**

- We can guide users through this flow via a message that prompts them to go back and make the necessary correction.
    
- Alternatively, a more intuitive fix would be to merge the two-step flow (selecting item/location and setting sequence number) into a single screen, so the user can modify values directly without backing out.
    

Sarah also flagged this as potentially being a framework limitation (the UI saving local state after backing out), and she’s planning to follow up with the framework team to confirm.

 I’d love to  to hop on a quick call to confirm that the current approach is okay with you or hear any preferences you have before finalizing.

Thank you,  

Hawa


[]