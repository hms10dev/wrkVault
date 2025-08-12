
# Key Terms:

| Term |Definition   |
|---|---|
|Request   |Input   |
|Response   |output   |
|Message Exchange Format  | format of request and response   |
|XML   |   |
|JSON   |   |
|transport  | defines how service is called [HTTP or MQ]   |


# Soap Web Services
- soap and rest not apples to apples comparison
- Simple Object Access Protocol
- 
![[SOAP.png]]
**Soap Header is Optional
- no restrictions on Transport
- Web Service Definition Language (WSDL)
# RESTful Web Services
- REpresentational State Transfer
- defines an archetectual approach
- ## Key Abstraction - Resource :
	- resource has URL (Uniform Resource Identifier)
	- A Resource can have different reprensentations:
		- XML
		- HTML
		- JSON
	- __Example:__
		- Create a User
			- POST /users
		- Delete a User
			- DELETE /users/1
		- Get all Users
			- GET /users
		- Get one Users
			- GET /users/1
- ## REST
	- You have to think in terms of Resources
	- make use of HTTP and use verbs already defined (GET POST DELETE etc...)
	- Data Exchange Format
		- No Restriction, JSON is popular
	- Transport
		- only HTTP
	- Service Definition:
		- No Standard. (WADL/Swagger, etc.)
			- can be drawback in some instances

# SOAP vs RESTful Web Services:
- remember: not apples to apples

## Restrictions vs Architectual Approach

| **SOAP** | **REST** |
|----------|----------|
|          |          |
|          |          |


## Data Exchange Format
| **SOAP** | **REST** |
|----------|----------|
|Format always XML , SOAP XML.should always adhere to SOAP formatting       |  JSON        |
|          |          |

## Service Definition
| **SOAP** | **REST** |
|----------|----------|
| WSDL         |  does not have standard definition language   ( can use SWAGGER)      |
|          |          |

## Transport
| **SOAP** | **REST** |
|----------|----------|
| no restriciton         |  best use of HTTP Protocol        |
|          |          |

## Ease of implementation
| **SOAP** | **REST** |
|----------|----------|
|    have to define WSDL and complexities with parsing.      |    JSON so easy to parse and etc      |
|          |          |
  
