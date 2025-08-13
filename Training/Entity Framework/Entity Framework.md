 # Intro to Entity Framework

## Date: Aug 5, 2022

---
See [[MA Frameworks Overview]] for a broader overview of Manhattan Active frameworks.


## What is it?
- Most difficult and most important framework
	- maintains consistency throughout the whole suite of applications we develop
- Set of technologies that enable application devs to work with relational data using domain-specific objects
- provides consistent set of APIs to create/update or access data
- Includes features like [[change management]] for tracking entity updates.
- devs can work with a higher level of abstraction upon dealing with data

## Architecture
![[Screen Shot 2022-08-29 at 2.10.58 PM.png]]
## Advantages:
Advantages:
- unified data access layer,
	- all data access calls would go through EF which enables more features like security and tracing
- consistency
	- code will be consistent across all modules / entities
- Maintainability
	- changes b/c of enhancements and defects are done at framework level
- Cost
	- cost to change at a specific location is far less than changing the whole codebase
- Flexibility
	- Even though code is generated using centralized framework, app devs have choice to extend the classes and override default behavior
- Extensibility
	- services team and customers can use entity framework to extend domain entities to add implementation specific behavior
## Concept of Profile

- In general: Profile = describing the nature of something
- in MANH case, the data(base data, master data, config data) belongs to a set profile depending on the purpose. 
- Those preset profiles will then be linked to one or more organization

### Why do this?
- orgs can share sets of data for certain purposes without having to duplicate the data
- data between different sets of profiles can be switched based on the business needs.
	- ==Example:==
		- I can have 2 profiles for items: Winter Item Profile, Summer Item Profile 
		- they can be switched between them based on the seasonal demand. 
		- I can have a set of rules - profile and would apply a specific rule profile based on the market demand.

### Example Situation:
1. Ann Taylor and Loft are two different brands that want to share the same Customer data.
	 - Ann Taylor and Loft may also share certain items and have their own set of items.
2. Ascena wants to use a set of promotions and store tagging for autumn. 
	- They would want to shift to different set of rules and promotions for the Christmas season.

### SubSubject

- four-color theorem
- GPS/maps

### SubSubject 2

- Social networks, such as facebook, twitter, and instagram
- gene/protein expression networks

### Generated Classes Example:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<component xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" name="testing"
           basePackage="com.manh.cp.testing"
           tablePrefix="TST" xsi:noNamespaceSchemaLocation="EntityMetaData.xsd">
    <entities subPackage="product">
        <entity name="product" serviceLevelEntity="true" type="master" profilePurpose="tst::product" description="List of testings the shipper works with">
            <property name="productId" type="id" uiFilterable="true" description="Unique identifier of the product."
                      nullable="false" />
            <property name="description" type="longText" localize="true" description="Item description"
                      nullable="true" />
            <property name="name" type="longText" localize="true" uiFilterable="true" description="Product Name"
                      nullable="true" />
            <property name="style" type="text" uiFilterable="true" localize="true" description="Product style"
                      nullable="true" />
            <property name="color" type="text" localize="true" uiFilterable="true" description="Product color"
                      nullable="true" />
 
 
            <businessKeys>
                <businessKey>
                    <property name="productId" />
                </businessKey>
            </businessKeys>
        </entity>
 
    </entities>
</component>
```

## Entity Metadata

### Schema Definition:
#### Layout:
```xml
<component (1 only)>
	<entities (1-n)>
		<entity (1-n)>
			<property (1-n)/>
			<businessKeys (0-1)>
				<businessKey (1-n)>
					<property (1-n)/>
				</businessKey>
			</businessKeys>
			<indexes (0-n)>
				<index (1-n)>
					<property (1-n)/>
				</index>
			</indexes>
		</entity>
	</entities>
	<relationships (0-1)>
		<relationship (1-n)>
			<joins (0-1)>
				<join (0-n)/>
			</joins>
		</relationship>
	</relationships>
</component>
```

## Elements:
```
<component>
```
| Attribute                     | Description                                                                              | required? |
| ----------------------------- | ---------------------------------------------------------------------------------------- | --------- |
| name                          | name of the component, used in generated REST endpoints                                  | yes       |
| basePackage                   | based package name for all generated classes in the component                            | yes       |
| uiResourceBundle              | resource bundle name to load translations for the config UI                              | no        |
| tablePrefix                   | 1-3 letter prefix to be appended to all default table name                               | yes       |
| xmlns:xsi                     | “[http://www.w3.org/2001/XMLSchema-instance](http://www.w3.org/2001/XMLSchema-instance)” | yes       | 
| xsi:noNamespaceSchemaLocation | “EntityMetaData.xsd”                                                                     | yes       |

```
<entities>
```
| Attribute  | Description                                                                                          | Required? |
| ---------- | ---------------------------------------------------------------------------------------------------- | --------- |
| subPackage | appended to component's basePackage to create base package for all generated code within this entity | Yep       |
|            |                                                                                                      |           |

```
<entity>
```
| Attribute      | Description                                                                                     | Required |
| -------------- | ----------------------------------------------------------------------------------------------- | -------- |
| name           | name of the entity. needs to be camelcase. needs to be singular                                 | yes      |
| type           | One of “config”, “master”, “transaction” Both "config" and "master" are profile based entities. | yes      |
| profilePurpose | profile purpose id [[#Concept of Profile]]                                                      | nope     |
| etc...         |                                                                                                 |          |
|                |                                                                                                 |          |
|                |                                                                                                 |          |

```
<property>
```
| Attribute    | Description                                                     | Required |
| ------------ | --------------------------------------------------------------- | -------- |
| name         | name of the entity. needs to be camelcase. needs to be singular | yes      |
| [[type]]         | logical type for the property                                   | yes      |
| nullable     | flag to indicate nullabilty                                     | no       |
| description  | description                                                     | no       |
| externalName | Public name of the property                                     | no       |
| columnName   | DB column name associated with the property                     | no       |
| ...          |                                                                 |          |
|              |                                                                 |          |


### Item Location Component Example:
``` xml

<?xml version="1.0" encoding="UTF-8"?>
<component name="itemlocation" basePackage="com.manh.cp.itemlocation" tablePrefix="ITL" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="EntityMetaData.xsd">
    <entities subPackage="itemlocation">
        <entity name="itemLocation" type="master" serviceLevelEntity="true" restAPIs="all" securityScope="profile" profilePurpose="itl::itemlocation"
                description="Entity to hold configuration parameters for an item for a specific location">
            <property name="itemId" type="id" description="Item ID" />
            <property name="locationId" type="id" description="Location holding the inventory" />
            <businessKeys>
                <businessKey>
                    <property name="itemId" />
                    <property name="locationId" />
                </businessKey>
            </businessKeys>
        </entity>
        <entity name="itemLocationSource" type="master" serviceLevelEntity="true" restAPIs="all" securityScope="profile" profilePurpose="itl::itemlocation"
                description="Holds items associated to a relationship">
            <property name="itemId" type="id" description="Item ID" />
            <property name="locationId" type="id" description="Location holding the inventory" />
            <property name="sourceLocationId" type="id" description="Source Location" />
            <property name="purchasePrice" type="moneyAmount" description="Purchase price of the item from the shipping location to receiving location"/>
            <property name="currencyCode" type="text" description="Currency of the charge amount for the service"/>
            <businessKeys>
                <businessKey>
                    <property name="itemId" />
                    <property name="locationId" />
                    <property name="sourceLocationId" />
                </businessKey>
            </businessKeys>
        </entity>
    </entities>

</component>


```


## Relationships
- the relationship element describes relationship between two entities within the same component
>   
It is not intended (at this point) to describe relationships to entities that reside in other components. ( or in different entity xml)


### Primary Key based Relationship
#### Parent - Child Relationship
![[Screen Shot 2022-08-31 at 2.20.41 PM.png]]
Multiple relationships with this configuration are not allowed between the same pair of entities.

Examples: 
- Order => Order line
- Item => Item Media
- 

#### One to One Relationship

![[Screen Shot 2022-08-31 at 2.23.38 PM.png]]
- this relationship is intended for dependent relationships only
- multiple relationships with this config are not allowed between the same pair of entities

Examples:
- Item -> Item selling attributes
- Customer -> Customer preferences

--- 




## Fetching Entity Metadata at Runtime
- many of the metadata values from the entity xml are available at runtime

### Serverside
- on the server, the metadata for a particular entity can be retrieved by calling:
```java
Metadata metadata = DomainEntity.getMetadata("<entityname");
```

This returns an instance of the Metadata class(or null if the metadata for the given entity had not been found)

Metadata class contains:
- Entity Class
- Security scope
- Security Key
- several flags (importable, supportsExtendedAttributes, serviceLevelEntity, etc.)

### Client side
- REST endpoint can be called like so:
```java
String entityName = "University";  
ResponseEntity<RestApiResponse<Map<String, Object>>> response = restTemplate.exchange(getBaseURL() + "/api/fwcore/metadata/{entityName}",  
        HttpMethod.GET, null, mapTypeReference, entityName);
```




---

# REVIEW :

# Vocab:

- **undirected** graph
    
    $e =(u,v)∈ E ⇒ (v,u)∈ E$
    
    in other words, its possible to go from u to v, and vice versa
    
- **directed** graph
    
    it is not possible to go from u to v and vice versa
    
    so the 
    
    $e =(u,v)∈ E ⇒ (v,u)∈ E$
    
    equation does not hold..
    
- self loop
    
    the starting and ending vertices are the same 
    
    i.e. e=(v,v))
    
- path
    
    A path is a sequence of vertices (v1,v2,...,vk), such that vi+1 is a neighbor of vi .
    


## The notes review:

- question 1
- question 2
- question 3
- question 4

## Questions for next time

- [ ]  question 1
- [ ]  2
- [ ]  3
- [ ]  4
- [ ]  5
- [ ]  6
- [ ]  7
- [ ]  8
- [ ]  9
- [ ]  10
