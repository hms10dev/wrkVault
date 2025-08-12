Milly says behavior is fine
way to validate without user going back
whatever supports the framework, she'll take it 


A.K.A **NO CHANGES**

### 📝 **Meeting Notes: Forecast Summary Validation Behavior 

**Topic:**  
Handling validation during save/update flow for forecast summary grouping attributes.

---

### 🔄 **Current Behavior**

- When **"Save and Finish"** or **"Save and Continue"** is clicked, the process always calls the **update method**.
    
- The update method **automatically invokes the validator**, which in turn **triggers a validation error** if the entry is invalid (e.g., duplicate).
    
- This validation step is **inherent to the framework's entity update process**.
    

---

### ❓ **Main Concern (Hawa)**

- Is there a way to **bypass the validation** during this specific flow (i.e., exiting without saving)?
    
- The goal is to **avoid duplicate validation errors** when a user backs out of an entry instead of completing it.
    

---

### ✅ **Clarifications (Sarah)**

- The validation **on add** was not triggered before Hawa’s recent change, but is now.
    
- The system **always runs validation on update**, and the generated update logic routes through `BusinessValidationManager.validateEntity`.
    
- This is likely a **framework limitation**: the UI is saving local state even when the user exits, which causes the validator to still process that entry.
    

---

### 🛠️ **Next Steps**

- **Sarah will create a defect for the framework team** to explore adding a **flag or mechanism** that prevents saving or validation when exiting an "add" flow without completion.
    
- Until then, **users will need to manually delete** duplicates if they accidentally back out and encounter validation issues.
    
- This workaround will remain in place unless a framework-level enhancement is made.