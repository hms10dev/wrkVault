# 🌱 Note: Forecast Entity MUP UI Card View 
##  ⌚️ Date: Aug 16, 2023
##  🎫 Story Ticket: https://manhattanassociates.atlassian.net/browse/AI-4920

> [!info] Today's Goals:
> > 
> > - [x] Finish writing test for ModelStoreSetupMapServiceImpl.java today
> > - [ ] simple
> > - [ ] task
> > - [ ] simple
> > 
> >
> > 


# To-do list 📝
---

- [x] New menu, “Forecasts” menu should be nested under Forecast parent folder.

- [x] - Clicking on this menu should load card view with below details:     
    
- [ ] - Forecast Policy
        
- [ ]    - Description
        
- [ ]    - Forecast
        
  - [ ]  - Seasonal Index
        

- [x] Below Actions should be added:

	- [ ] - Details  ->  scope of this is limited to just button addition. Implementation will be separate story
    
	- [ ] - Export
    
	- [ ] - Initialize Forecast (ONLY button addition)

- [x] make branch for changes and migrate them there please
- [x] Filters
# Notes:📝 
---

### Reference Code:

##### Add-Edit flow, aka the popup when you click on the card view
###### ui-metadata/com-manh-cp-ai-forecast/pages/ForecastPolicy/ForecastPolicyAddEditFlow.json


```json
{
  "Data": [
    {
      "EntityName": "ForecastPolicy",
      "ActionKey": "ForecastPolicy_Wizard",
      "ActionFlow": [
        {
          "Groups": [
            {
              "Name": "ForecastPolicy.step1.stepTitle",
              "WidgetType": "FormGroup",
              "Required": true,
              "SupportsCatchAll": true,
              "Groups": [
                {
                  "Alignment": "Left",
                  "Attributes": [
                    {
                      "AttributeName": "ForecastPolicyId",
                      "UID":"ActionFlow1-Column1-Attribute1"
                    },
                    {
                      "AttributeName":"Description",
                      "UID":"ActionFlow1-Column1-Attribute2"
                    },
                    {
                      "AttributeName": "ForecastPolicyRank",
                      "UID":"ActionFlow1-Column1-Attribute3"
                    },
                    {
                      "AttributeName": "ForecastPurpose.ForecastPurposeId",
                      "UID":"ActionFlow1-Column1-Attribute4"
                    },
                    {
                      "AttributeName": "ForecastPeriodType.ForecastPeriodTypeId",
                      "UID":"ActionFlow1-Column1-Attribute5"
                    },
                    {
                      "AttributeName": "ForecastMethod.ForecastMethodId",
                      "UID":"ActionFlow1-Column1-Attribute6"
                    },
                    {
                      "AttributeName": "ItemHierarchyId",
                      "UID":"ActionFlow1-Column1-Attribute7"
                    },
                    {
                      "AttributeName": "LocationHierarchyId",
                      "UID":"ActionFlow1-Column1-Attribute8"
                    }
                  ],
                  "UID": "ActionFlow1-Groups1-Groups1"
                },
                {
                  "Alignment": "Right",
                  "Attributes": [
                    {
                      "AttributeName": "ForecastHistoryUsedType.ForecastHistoryUsedTypeId",
                      "UID":"ActionFlow1-Column2-Attribute7"
                    },
                    {
                      "AttributeName": "LastNumberOfPeriods",
                      "UID":"ActionFlow1-Column2-Attribute8"
                    },
                    {
                      "AttributeName": "ForecastHistoryFromDate",
                      "UID":"ActionFlow1-Column2-Attribute9"
                    },
                    {
                      "AttributeName": "ForecastHistoryToDate",
                      "UID":"ActionFlow1-Column2-Attribute10"
                    },
                    {
                      "AttributeName": "UpdateTrendFactor",
                      "UID":"ActionFlow1-Column2-Attribute11"
                    },
                    {
                      "AttributeName": "SmoothingPolicy.SmoothingPolicyId",
                      "UID":"ActionFlow1-Column1-Attribute12"
                    },
                    {
                      "AttributeName": "ForecastControlPolicy.ForecastControlPolicyId",
                      "UID":"ActionFlow1-Column1-Attribute13"
                    },
                    {
                      "AttributeName": "ForecastExceptionPolicy.ForecastExceptionPolicyId",
                      "UID":"ActionFlow1-Column1-Attribute14"
                    }
                  ],
                  "UID": "ActionFlow1-Groups1-Groups2"
                }
              ],
              "UID": "ActionFlow1-Groups1"
            },
            {
              "Name": "ForecastPolicy.ForecastFilterCondition.step2.stepTitle",
              "Description": "ForecastPolicy.ForecastFilterCondition.step2.stepTitle",
              "WidgetType": "List",
              "ViewName": "ForecastFilterCondition",
              "UID": "ActionFlow1-Groups2"
            }
          ],
          "Dependencies": [
            {
              "Target": "attribute",
              "Id": "LastNumberOfPeriods",
              "Type": "hidden",
              "Condition": "${ForecastPolicy.ForecastHistoryUsedType.ForecastHistoryUsedTypeId} === 'A' || ${ForecastPolicy.ForecastHistoryUsedType.ForecastHistoryUsedTypeId} === 'R'",
              "UID": "ListConfig1-Dependencies8"
            },
            {
              "Target": "attribute",
              "Id": "ForecastHistoryFromDate",
              "Type": "hidden",
              "Condition": "${ForecastPolicy.ForecastHistoryUsedType.ForecastHistoryUsedTypeId} === 'A' || ${ForecastPolicy.ForecastHistoryUsedType.ForecastHistoryUsedTypeId} === 'L'",
              "UID": "ListConfig1-Dependencies9"
            },
            {
              "Target": "attribute",
              "Id": "ForecastHistoryToDate",
              "Type": "hidden",
              "Condition": "${ForecastPolicy.ForecastHistoryUsedType.ForecastHistoryUsedTypeId} === 'A' || ${ForecastPolicy.ForecastHistoryUsedType.ForecastHistoryUsedTypeId} === 'L'",
              "UID": "ListConfig1-Dependencies10"
            }
          ],
          "HideStepIndicator": false,
          "HideGroupHeader": false,
          "UID": "ActionFlow1"
        }
      ]
    }
  ]
}
```
![[Screenshot 2023-08-24 at 11.54.48 AM.png]]
  
##### List/ Card view example:
###### ui-metadata/com-manh-cp-ai-forecast/pages/ForecastPolicy/ForecastPolicyList.json
```json
{
  "CreatedDateTime": "Tue Nov 08 17:38:30 UTC 2022",
  "CreatedBy": "admin@scp-org.com",
  "Version": "1",
  "Data": [
    {
      "EntityName": "ForecastPolicy",
      "ListConfig": [
        {
          "PrimaryList": {
            "Columns": [
              {
                "Attributes": [
                  {
                    "AttributeName": "ForecastPolicyId",
                    "UID": "ListConfig1-PrimaryList-Columns1-Attributes1"
                  },
                  {
                    "AttributeName": "Description",
                    "UID": "ListConfig1-PrimaryList-Columns1-Attributes2"
                  }
                ],
                "UID": "ListConfig1-PrimaryList-Columns1"
              },
              {
                "Attributes": [
                  {
                    "AttributeName": "ForecastPolicyRank",
                    "UID": "ListConfig1-PrimaryList-Columns2-Attributes1"
                  },
                  {
                    "AttributeName": "ForecastPurpose.ForecastPurposeId",
                    "LabelKey": "ForecastPolicy.ForecastPurpose.displayText",
                    "UID": "ListConfig1-PrimaryList-Columns2-Attributes2"
                  }
                ],
                "UID": "ListConfig1-PrimaryList-Columns2"
              },
              {
                "Attributes": [
                ],
                "UID": "ListConfig1-PrimaryList-Columns3"
              }
            ],
            "Actions": [
              "Details",
              "Delete",
              "ForecastInit"
            ],
            "UID": "ListConfig1-PrimaryList"
          },
          "Actions": [
            "Create"
          ],
          "UID": "ListConfig1"
        }
      ]
    }
  ]
}
```

![[Screenshot 2023-08-24 at 11.56.26 AM.png]]

##### Actions Example
###### ui-metadata/com-manh-cp-ai-forecast/pages/ForecastPolicy/ForecastPolicyActions.json

```json
{
  "CreatedDateTime": "Tue Nov 08 17:38:30 UTC 2022",
  "CreatedBy": "admin@scp-org.com",
  "Version": "1",
  "Data": [
    {
      "EntityName": "ForecastPolicy",
      "ActionConfig": [
        {
          "ActionName": "Create",
          "LabelKey": "Create",
          "IconName": "edit.svg",
          "ActionType": "wizard",
          "ActionKey": "ForecastPolicy_Wizard",
          "ActionResourceId": "scpui::ai-forecast::forecastpolicy::create",
          "UID": "ActionConfig1"
        },
        {
          "ActionName": "Edit",
          "LabelKey": "Edit",
          "IconName": "edit.svg",
          "SupportsMultiple": false,
          "ActionArguments": [
            "ProfileId",
            "ForecastPolicyId",
            "ForecastPolicyRank",
            "ForecastPurpose"
          ],
          "ActionType": "wizard",
          "ActionKey": "ForecastPolicy_Wizard",
          "ActionResourceId": "scpui::ai-forecast::forecastpolicy::edit",
          "UID": "ActionConfig2"
        },
        {
          "ActionName": "Delete",
          "LabelKey": "Delete",
          "IconName": "delete.svg",
          "ActionArguments": [
            "ProfileId",
            "ForecastPolicyId",
            "ForecastPolicyRank",
            "ForecastPurpose"
          ],
          "SupportsMultiple": false,
          "ActionType": "warningpopup",
          "ActionHttpType": "DELETE",
          "ActionResourceId": "scpui::ai-forecast::forecastpolicy::delete",
          "UID": "ActionConfig3"
        },
        {
          "ActionName": "View",
          "ActionKey": "ForecastPolicy_Wizard",
          "LabelKey": "ForecastPolicy.View",
          "IconName": "view.svg",
          "ActionType": "wizard",
          "SupportsMultiple": false,
          "ActionResourceId": "scpui::ai-forecast::forecastpolicy::view",
          "UID": "ActionConfig4"
        },
        {
          "ActionName": "ForecastInit",
          "LabelKey": "ForecastPolicy.ForecastInit.displayText",
          "SupportsMultiple": false,
          "ActionType": "warningpopup",
          "QuestionLabelKey": "ForecastPolicy.ForecastInitQuestion.displayText",
          "ActionHttpType": "POST",
          "ActionURL": "/api/ai-forecast/forecastPolicy/initializeForecast/${ForecastPolicyId}",
          "ActionResourceId": "scpui::ai-forecast::forecastpolicy::forecastinit",
          "UID": "ActionConfig5"
        },
        {
            "ActionName": "Details",
            "LabelKey": "Details",
            "IconName": "Icon_Details.svg",
            "SupportsMultiple": false,
            "ActionType": "details",
            "ActionKey": "Details",
            "ActionResourceId": "scpui::ai-forecast::forecastpolicy::details",
            "UID": "ActionConfig6"
        }
      ]
    }
  ]
}
```

##### Details Example
###### ui-metadata/com-manh-cp-ai-forecast/pages/ForecastPolicy/ForecastPolicyDetails.json
```json
{
  "CreatedDateTime": "Tue Nov 08 17:38:30 UTC 2022",
  "CreatedBy": "admin@scp-org.com",
  "Version": "1",
  "Data": [
    {
      "EntityName": "ForecastPolicy",
      "ListConfig": [
        {
          "PrimaryList": {
            "Columns": [
              {
                "Attributes": [
                  {
                    "AttributeName": "ForecastPolicyId",
                    "UID": "ListConfig1-PrimaryList-Columns1-Attributes1"
                  },
                  {
                    "AttributeName": "Description",
                    "UID": "ListConfig1-PrimaryList-Columns1-Attributes2"
                  },
                  {
                    "AttributeName": "ForecastPolicyRank",
                    "UID": "ListConfig1-PrimaryList-Columns1-Attributes3"
                  },
                  {
                    "AttributeName": "ForecastPurpose.ForecastPurposeId",
                    "LabelKey": "ForecastPolicy.ForecastPurpose.displayText",
                    "UID": "ListConfig1-PrimaryList-Columns1-Attributes4"
                  },
                  {
                    "AttributeName": "ForecastPeriodType.Description",
                    "LabelKey": "ForecastPolicy.ForecastPeriodType.displayText",
                    "UID": "ListConfig1-PrimaryList-Columns1-Attributes5"
                  },
                  {
                    "AttributeName": "ForecastMethod.Description",
                    "LabelKey": "ForecastPolicy.ForecastMethod.displayText",
                    "UID": "ListConfig1-PrimaryList-Columns1-Attributes6"
                  },
                  {
                    "AttributeName": "ItemHierarchyId",
                    "LabelKey": "ForecastPolicy.ItemHierarchy.displayText",
                    "UID": "ListConfig1-PrimaryList-Columns1-Attributes7"
                  },
                  {
                    "AttributeName": "LocationHierarchyId",
                    "LabelKey": "ForecastPolicy.LocationHierarchy.displayText",
                    "UID": "ListConfig1-PrimaryList-Columns1-Attributes8"
                  }
                              ],
                "UID": "ListConfig1-PrimaryList-Columns1"
              },
              {
                "Attributes": [
              {
                "AttributeName": "ForecastHistoryUsedType.Description",
                "LabelKey": "ForecastPolicy.ForecastHistoryUsedType.displayText",
                "UID": "ListConfig1-PrimaryList-Columns2-Attributes1"
              },
                  {
                    "AttributeName": "LastNumberOfPeriods",
                    "UID": "ListConfig1-PrimaryList-Columns2-Attributes2",
                    "Condition": "${ForecastPolicy.ForecastHistoryUsedType.ForecastHistoryUsedTypeId} === 'L'"
                  },
                  {
                    "AttributeName": "ForecastHistoryFromDate",
                    "UID": "ListConfig1-PrimaryList-Columns2-Attributes3",
                    "Condition": "${ForecastPolicy.ForecastHistoryUsedType.ForecastHistoryUsedTypeId} === 'R'"
                  },
                  {
                    "AttributeName": "ForecastHistoryToDate",
                    "UID": "ListConfig1-PrimaryList-Columns2-Attributes4",
                    "Condition": "${ForecastPolicy.ForecastHistoryUsedType.ForecastHistoryUsedTypeId} === 'R'"
                  },
                  {
                    "AttributeName": "UpdateTrendFactor",
                    "UID": "ListConfig1-PrimaryList-Columns2-Attributes5"
                  },
                  {
                    "AttributeName": "SmoothingPolicy.SmoothingPolicyId",
                    "LabelKey": "ForecastPolicy.SmoothingPolicy.displayText",
                    "UID": "ListConfig1-PrimaryList-Columns2-Attributes6"
                  },
                  {
                    "AttributeName": "ForecastControlPolicy.ForecastControlPolicyId",
                    "LabelKey": "ForecastPolicy.ForecastControlPolicy.displayText",
                    "UID": "ListConfig1-PrimaryList-Columns2-Attributes7"
                  },
                  {
                    "AttributeName": "ForecastExceptionPolicy.ForecastExceptionPolicyId",
                    "LabelKey": "ForecastPolicy.ForecastExceptionPolicy.displayText",
                    "UID": "ListConfig1-PrimaryList-Columns2-Attributes8"
                  }
                ],
                "UID": "ListConfig1-PrimaryList-Columns2"
              }
            ],
            "Actions": [
              "Delete",
              "ForecastInit"
            ],
            "UID": "ListConfig1-PrimaryList"
          },
          "ExpandedList": [
            {
              "Groups": [

                {
                  "Name": "FilterCondition",
                  "LabelKey": "FilterCondition",
                  "EntityName": "ForecastFilterCondition",
                  "LayoutType": "Grid",
                  "Columns": [
                    {
                      "Attributes": [
                        {
                          "AttributeName": "FilterConditionId",
                          "UID": "ListConfig1-ExpandedList1-Groups3-Columns1-Attributes1"
                        },
                        {
                          "AttributeName": "EntityType",
                          "UID": "ListConfig1-ExpandedList1-Groups3-Columns1-Attributes2"
                        },
                        {
                          "AttributeName": "FilterExpression",
                          "UID": "ListConfig1-ExpandedList1-Groups3-Columns1-Attributes3"
                        }
                      ],
                      "UID": "ListConfig1-ExpandedList1-Groups3-Columns1"
                    }
                  ],
                  "UID": "ListConfig1-ExpandedList1-Groups3"
                }
              ],
              "UID": "ListConfig1-ExpandedList1"
            }
          ],
          "Actions": [],
          "UID": "ListConfig1"
        }
      ]
    }
  ]
}
```

### Errors
![[Screenshot 2023-08-24 at 11.54.21 PM.png]]

![[Screenshot 2023-08-25 at 12.09.29 AM.png]]

# Sub-pages 📑

---
- [[Sub Page]]
- [[Sub Page]]
- [[Sub Page]]
- [[Sub Page]]

# Reference links 🔗
---

[Beyond Frank Lloyd Wright: A Broader View of Art in Chicago](https://www.nytimes.com/2018/03/08/arts/chicago-museums-art.html?rref=collection%2Fsectioncollection%2Ftravel)

  
[Havana's Symphony of Sound](https://www.nytimes.com/2018/03/12/travel/havana-cuba.html?rref=collection%2Fsectioncollection%2Ftravel)