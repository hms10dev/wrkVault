# 🌱 QuickNote: Forecasts UI
 #### Reference link: https://manhattanassociates.atlassian.net/wiki/spaces/ASCP/pages/4402085959/Forecasts+Entity+UI
####  ⌚️ Date: Aug 2, 2023

Tasks
--- 
- [ ] Make sure you break it up  
- [ ] add description field
- [ ] and concat the desciptions for l3

---
### 📝  Notes
1. MUP screen that will get replaced by custom UI in future

==ForecastEntities.xml== : https://bitbucket.org/manhattanassociates/component-ai-forecast/src/master/src/main/resources/metaData/ForecastEntities.xml
#### Forecast Entity:
- contains info that can be understood by a typical user ,
- any common information is stored in here

#### Forecast Factors:
- information that is more scientific in nature
- any information that is different due to forecast method, update, or manual forecast is stored in here
- store transactional forecast data that is generated and maintained from forecast policy alongside ==FORECAST==

- for current release , _Forecast and Forecast factors will be created and maintained for every item/location (leaf level) combination_ 
- multiple Forecasts and Forecast Factors can be created for the same item and location, but with different levels. 
- Policy priority will be copied into corresponding forecast...


## Forecast UI Notes:
Forecasts UI displays information in Forecast entity. From the Forecasts UI, a user can also access information in Forecast Factors entity. At this point, all of the fields on this MUP UI are for display only and are non-editable.

- Menu: 
	- “Forecasts” menu should be nested under Forecast parent folder.
    
- UI: 
	- L3/L4
    
- Permission/Role/Grant: 
	- Manager and Allocator
    
- UI Name: 
	- “Forecasts” for L3, 
	- “Forecast” for L4.
    
- Actions:
    
    - Details: 
	    - View only. Edit action will be available in the future, after backend functionalities are completed.
        
    - _**Initialize Forecast**_**:** 
	    - Re-initializes all forecast entities until the latest manual change.
        
    - _**Initialize and Override Forecast**_**:** 
	    - Re-initializes all forecast entities overriding all manual changes. 
	    - (These is no use for this action right now. It will be added when edit is permitted in the future.)
        
- Filters: 
	- Forecast Policy, Location, Item, Description
    
- Import/Export Data Loader: 
	- Asynchronous export only
    
- Related Links: 
	- **Items, Locations
	- (**We need to figure out how to display item and location in separate fields on the UI, or else, we can’t link to the particular item or location.)
    
- **Hyperlink**: 
	- Forecast Policy from the main L3 page.
    
- Entity Name: 
	- forecast

![[Screenshot 2023-08-15 at 2.17.57 PM.png]]

### Forecast Card View(L3):

From the card view, a user can click on the “Details” button to view the details of a forecast on the detail screen. Display the following fields on the card view in the following order:

![[Screenshot 2023-08-15 at 2.19.27 PM.png]]

- ==Description replaces Item + Location fields for now.== 
- MK: Add a “Description field” in the Forecast entity. 
- When records are created in Forecast, populate it with **itemId +_____+locationId.** ==Dev Team  add a story for this==.
- This field will be added strictly for this UI.

>[!info] Note:
>someone noted it might be a good idea to display Forecast Purpose and Forecast Rank on the Forecast UI. 
>but since those two fields are part of the Forecast Policy entity, not possible to display them on a MUP UI without some extension API.
>Since this UI will be temporary, probably will not add for now 


### ### Forecast Details View (L4)

Forecast Details UI will have the following sections:

- (Main) - no section heading
    
- Additional Information
    
- Forecast Audit
    
- Details (from Forecast Factors entity)
    

==look up the entity type to decide the field type to add on the UI,== e.g., a checkbox (or two radio buttons) for a Boolean, a calendar widget for a date. A drop down that currently doesn’t have a value in the seed data should be able to be displayed as a non-editable drop down.

_**Additional Information** (collapsible section)_
This section displays the following attributes in the following order:
![[Screenshot 2023-08-15 at 2.26.52 PM.png]]
![[Screenshot 2023-08-15 at 2.26.12 PM.png]]

### Additional Notes: 
- When we have multiple forecast factors in the future, we need to add an indicator to know which forecast factor is used in the forecast.
    
- Forecast Projection already has its own SCP Thin slice UI. While a Forecast record is created for each leaf level item location, a Forecast Projection record is created for each forecast period (52 week in a year).
    
- Forecast & forecastFactors entities both have Method attribute. Eventually we need to only display or highlight the corresponding factors with the same method, and the UI will need to handle this.
## Application/Todo:
- [ ] item 

