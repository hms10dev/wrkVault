

## Environment

Freedom VM with the current quarter ARID enabled

|   |   |
|---|---|
|PFIO_CURRENT_RELEASE_GOLD_GKE_LARID|Latest(2023-03)|


## Acceptance Criteria: 

1. User should be able to create Aggregate Plan Metric with 
	1. Product ID opening the ITem Lookup
2. New Item Lookup should have the following:
	1. Filter Fields: 
		1. Item Id
		2. Short Description
		3. Brand
		4. Vendor
		5. Department
		6. Class, 
		7. SubClass,
		8. Color
		9. Size
		10. Style
3. User should be able to Edit the Aggregate Plan Metric and edit Product Id
	1. Click on the Lookup Icon of the Product Id. The Item Lookup will have the 'Item Id' Populated from the Aggregate Plan Metric screen and the search result will show one record
	2. User can edit and select a new record and save the aggregate Plan Metric



## Reference Documentation:


### MD UI Impacted with Product/Style Lookup Usage: Aggregate Plan Metric
https://manhattanassociates.atlassian.net/wiki/spaces/AINV/pages/4215898122/MD+UI+Impacted+with+Product+Style+Lookup+Usage+Aggregate+Plan+Metric

### Aggregate Plan Metric UI Changes

1. **Product Look up** →. This look up will be changed to Item Lookup . Refer to #6 and #7 below for the lookup changes to be done

> [!info]
> Label , Tooltip , Help Text changes to update “Product to Item” will be done as the part of separate story

>[!info] Remember
>Credentials:
>AIAdmin/AIAdmin@123



Notes from meeting with Mandar:

https://pfio-13.pfio.manh.cloud/ai/screen/ai-plan/AggregatePlanMetric/wizard 
this is where the change is happening

and I also need to map the front end changes to a different entity (item component)

Metadata changes
 -Look for metadata for lookups