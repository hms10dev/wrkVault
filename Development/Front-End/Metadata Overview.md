

https://manhattanassociates.atlassian.net/wiki/spaces/ASCP/pages/4265574601/Metadata+UIs


https://bitbucket.org/manhattanassociates/component-commonui-facade/src/ea51e126b0a9da92146f3b9f46fc7b5c888c2293/src/main/resources/seedData/io/menu_40__CommonUi.json#lines-8

## What is the Metadata Framework?

- specializes in :
	- Publishing to consul
	- providing APIs to metadata UIs for:
		- Metadata retrieval
		- Translating the metadata UI
		- Searching entity data
		- PErforming actions on UI,
		- and Performing schema validations for the metadata UI
Included in Framework ui Facade as a dependency in the build.gradle;
The MetadataGenerator java classes (in metadatagen folder) are used as an extension of fw-ui-metadata (Metadata Framework) to generate metadata for the UIs and subsequently publish the metadata to the key/value store Consul.
- MetadataGenerator is responsible for 
	- Generating the metadata for UI
	- Checking if Metadata exisits or not
	- 




## Setting up a framework Screen:

- First steps: Get a hold of all the webpages you'll need and finding an environment that works. 
	- need to find a BA or Dev that will grant access. 
		- they will give you username and password for the webpages and environments. 
- Neeed to understand what an environment is . 
	- There is a UI screen where the changes made will be seen.
	- There is a Consul screen where said updates and changes will be made. 

The following environment down below is called dm-1d. It's called this because it has the letter and number combination of dm-1d. Another environment would have a different letter and number combination.

One environment is called [https://gcpside-dm-1d.manh-dev.com/udc/dm/screen/lmcore/AdjustmentSummaryDetail](https://gcpside-dm-1d.manh-dev.com/udc/dm/screen/lmcore/AdjustmentSummaryDetail)

### Pulling Up Component Data
- if you tried to pull up screen  and put all appropriate data, there is likely no background data. 
- Best way is to use Postman:
	- to gather info needed to propagate data, click vertical three dots on upper right hand side . dropdown click, more tools click, droupdown develeoper tools click, and then refresh your webpage
- Click on the sequence name under the Name heading that begins with the word "Root." Gather the following information. The Authorization, Content- Type, Location, Organization. By now Postman should be loaded. In the Post search bar enter the URL of your screen with the first word of the screen name as low case and the following words upper case.

==Example Down Below==

[https://side-sc-5b.manh-dev.com/lmcore/api/lmcore/punchCard](https://side-sc-5b.manh-dev.com/lmcore/api/lmcore/punchCard)


