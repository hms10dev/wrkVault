
# 🌱MA Frameworks Overview

Date: Aug 1, 2022
Time: 10:07
Attendees:

---

# Goals / agenda
1. Manhattan Active Cloud and Cloud Plartform Overview

# Discussion notes
> Framework is used by components
> 
- core products:


- Efficiency, Flexibility, open
	- high avail. high scal. cost effectivness
- Configurable, extensible, adaptable
- open: build on open source, modern and up to date, future friendly

- everything developed should be stateless
- all services should be stateless, can be ramped up or ramped down at anytime
- stateful service will not scale
- At manh we use linux for docker (duh)

## Orchestration with Kubernetes
> Stack = Kubernetes cluster
 
 > sidekick/chancler- helps manage and deploy stacks



## Continuous Integration and Release
Mapa

cloudops - handles scheduling release
MRE - handles actual release

## CI Pipeline
- runs 2000+ builds/day
- covers all Manh Active applications
- Tools:
	- Kibana (logging)
	- fluentd


## Component Communication
- ### Synchronous Communication
- HTTP calls(synchronous)
	- When customer component comes up, it communicates with customer DB
		customer component has to call rest api to access order component to reach order db to get the order information

### Asynchronous Communication
- messaging (Asynchronous)

### Message based Communication
dealing with failed messages:
failed mssgs sent to its own queue and has its own processing logic
common util can retry message set number of times before it's permanantly pulled into Common Util

### Rabbit MQ console
- internal messaging queue
	- customers cannot have access
- 

### Batch/Scheduled Processing

Scheduler-

Controller -

Order DB - 

Self-healing and Autoscaling


### Base Customization


### Extension components
in the base code, 

# [[Entity Framework]]
## modules in Entity Framework
- entity framework
- code generator
- database Upgrader
	- DDL [(Data definition language)]
	- DML(Data manipulation language, seed data)

Advantages:
- unified data access layer,
- consistency
- Maintainability
- Cost
- Flexibility
- Extensibility

### Entity Framework Features
- security
- extended attributes
- extension points
- [[change management]]
- audit
- data localization
- interface Mapping
- Caching 
- Swagger Documentation
- Excel Export and Import
- More ...



# [[Cloud Framework]]
## Label Management
### Types of Labels

==There are four types of Labels:==
1. Annotations
2. AttributeLabels
3. InheritedLabels
4. RuleLabels
#### Annotations
- Annotations are the labels, which are created based on the user request. Request payload should have annotations labels details.
Example Payload:

```json
"EntityLabels":
	{ 
		"Annotations": 
		{ 
			"Domestic": true,
			"Fragile": true,
			"Hazmat": "ApplyActionDelete",
			"LabelsAction": "Reset" 
		}
	 }
```

`ApplyActionDelete` is the _reserve word_ and used for removal of label.

`"LabelsAction": "Reset"` is used to remove all annotations labels.

##### How to update Annotations ?

- EFW will extract the Annotations from the request payload and persist it in to the JSON_STORE column of the table. 
- If payload does not have annotations, then it will keep the old value as it is (might be null)
- If new Key or old key value has been changed in update flow, then It will be updated accordingly.
- New key will be added in the annotations.
#### Attribute Labels

#### Rule Based Labels
# Questions
- [ ] REST and Load balancers

# Vocab:
- MAPA
- MAQL
- Load Balancer
	-  **a device that acts as a reverse proxy and distributes network or application traffic across a number of servers**. Load balancers are used to increase capacity (concurrent users) and reliability of applications.
		- The following are few examples of software load balancers: **HAProxy – A TCP load balancer.** **NGINX – A http load balancer with SSL termination support**. (install Nginx on Linux)
- bomb
- AWPF
	- Asynch workload processing framework

#meeting
#Framework 
#Overview