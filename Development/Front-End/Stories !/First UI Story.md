 # 🌱 QuickNote: First UI Story

####  ⌚️ Date: May 5, 2023

---
> [!abstract] Don't forget to:
> > 
> > - [ ] Check teams for new messages
> > - [ ] Check Jira & Update story status
> > - [ ] Check Outlook
> > - [ ] Review Component and any issues/questions
> > 

# First UI Story
Current Story Ticket: [AAL-21184](https://manhattanassociates.atlassian.net/browse/AAL-21184)
Date: 2023-05-19
Time: 10:07

---


# Goals / agenda
1. Fulfillment options - ‘Ship to Address’ and ‘PickInStore’ values are by default ‘Yes’ in Product screen
    
2.  Fulfillment options - ‘Ship to Address’ and ‘PickInStore’ values are by default null in item entity
    

Expected: The default values for these two attributes should be ‘Yes’.

Refer screenshot.

# Discussion notes
- Screenshots:
![[image-20230408-125428.png]]
![[image-20230408-125446.png]]

# Action items
- [ ] Read Documentation on how to make the default values true
- [ ] Figure out where to make changes
- [ ] make changes
- [ ] test



# Notes:

Local changes will be made in metadata/com-manh-cp-ai-product/entities/ProductAttributes.json

product fulfilment options json:
![[Screenshot 2023-05-19 at 10.21.16 AM.png]]

item's fulfilment options json:

![[Screenshot 2023-05-19 at 10.19.20 AM.png]]

## Checking in MetaData Changes:
https://manhattanassociates.atlassian.net/wiki/spaces/SC2020/pages/1020297402/Checking+In+Metadata+Changes



![[Screenshot 2023-05-23 at 12.08.51 PM.png]]



## UI Support channel :

[5/8 9:51 AM] Jayagurusurya Balakrishnan

Hi ui framework support, 

We are trying to set a radio button with default value as true. And using the below value in Attribute.json.

"DefaultValue": true,

But for some reason it is not working in the add/edit flow wizard form field. So does it require a different method of configuration.

Below code is been used & for reference:
```json
{​​​​​​​​
 "EntityName":"SellingAttributes",
 "AttributeName": "SellingAttributes.ShipToAddress",
 "AttributeType": "boolean",
 "DefaultValue": true,
 "UID": "AttributeConfig174"
            }​​​​​​​​,
```


​

[5/9 3:25 AM] Sowjanya Ramprasad

Jayagurusurya Balakrishnan As communicated, please add the property in AddEditFlow.

​

[5/9 3:25 AM] Jayagurusurya Balakrishnan

Thanks, we will check on it.

​

[5/9 11:10 AM] Michael Dumars

Have you tried using string true?

<https://teams.microsoft.com/l/message/19:a5702d31fa2f4f09a079947da787e3f3@thread.tacv2/1683553865956?tenantId=1b212e38-787d-48cb-83bb-5e4302f225e4&amp;groupId=291c1182-5224-40f1-bc90-c9c59b203ccd&amp;parentMessageId=1683553865956&amp;teamName=Cloud Platform - UI&amp;channelName=ui framework support&amp;createdTime=1683553865956&amp;allowXTenantAccess=false>