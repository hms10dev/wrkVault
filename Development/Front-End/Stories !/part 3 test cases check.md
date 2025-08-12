



- [x]  Menu Placement and Name - Passed
    
- [x]  UI Name - Passed
    
- [x]  List/Card View:
    
    - [x] Label and placement of each field are correct: Passed, except for Current Forecast field should be called “Forecast” per confluence page.
        
    - [x]  Field values are popuplated correctly: Passed, except for Forecast Policy - the value shown was [object Object], not the policy Id.
        
    - [x] . Pagination: Passed. Pagination is visible on the bottom of the page.
        
- [x]  Detail View:
    
  - [x]  UI Name - Passed
        
   - [x] Maine section - Failed.
        
      - [x]  Forecast Id is not supposed to be displayed.
            
    - [x]  Field positions are not the same as described in the confluence page.
            
      - [x] . Forecast Policy value is displayed as [object Object], not the policy Id.
            
    - [ ] . Additional Information section - Failed.
        
        - [x] Section Tittle - Labels are not translated to display the correct section tittle (has curly brackets).
            
        - [x]  Forecast Method is supposed to be labeled “Method Type”
            
       - [ ]  Period Type field is missing label translation.
            
        - [ ] . None of the policy fields have the field value. All of them are shown as [object Object], not the policy Id.
            
       - [ ]  A couple fields are missing: Initial Smoothing Factor, Use Trend
            
        - [ ] . None of the date values are displayed, not even the Forecast Initialization Date. Are those date attributes populated in the entity?
            
   - [x] Forecast Audit section - Failed.
        
        - [x]  Section Tittle - Labels are not translated to display the correct section tittle (has curly brackets).
            
    - [ ] Action Buttons:
        
       - [x] . Details - Passed
            
       - [ ]  Initialize Forecast label - Failed. Button is labeled as “Generate Forecast”.
            
       - [ ]  -Initialize Forecast action backend code - Failed. Select one of the forecast with value > 0. When the button was clicked, Internal Server Error was displayed with the following details in the dev tools:-