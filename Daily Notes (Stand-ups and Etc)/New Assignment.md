 # 🌱 QuickNote: New Assignment

####  ⌚️ Date: Sep 4, 2022

---
### 📝  Notes
1. Write API That will take LPN using LPN ID
	1. figuring out url of api
	2. figuring out that what needs to be passed through
2. take the testquantity from that LPN and then apply math to it
3. save that multiplied testquantity to the db
4. return the lpn with the _updated_ testquantity 
5. Unit test

### Api Attributes:
- passes through LPNID
- returns LPNID and other attributes, with the modified testquantity

#### Property We're Modifying:
Test Quantity:
__Code:__
```xml
<property name="testQuantity" type="shortInteger" nullable="true" description="test quantity"/>
```

__type:__ shortInteger
__nullable:__ yes

### Logic:
getLpnByPkorBk();
- this returns document



- Controller

- MapService
	method doing most of that 

- how to fetch 

fetch Quantity number from LPN document using method getLpnByLpnId();

return number

multiply it using api call

update LPN 

return LPN document with new info using Get LPN by LPN ID

## Tips:

go into controller find method that does the same, 
extend the controller and write method

Use the previously written code as reference

use **get** and **update** methods

## Dev notes:
//because I implemented using getLpnByBusiness Keys and there is not a specific implementation for that, custom implementation was created
- I changed the Logger.trace API call from:
```
logger.trace(() -> ">> getLpn()")
```
to:
```
logger.trace(() -> "<< getByLpnId()");
```
### Questions:
- [x] how to reach the quantity data of lpn all the way from the document  using the api call
- [ ] reaching the quantity data of a SINGLE LPN 
- [ ] Create method:
- [x] Constructing the key and validating and creating has private access , not public?
	- [x] 'constructKey(com.manh.cp.fw.common.Document)' has private access in 'com.manh.cp.itemlocation.trackLpn.impl.service.LpnMapServiceImplBase'
- [x] Update Method:
	- [x] validate and Update has the same issues, it is private 
- [ ] What is firepost
- [x] Why can't the Component symbol be resolved when I add the private firepost methods




Meetings:


api's buisness key driven
stay away from PK( external use)

shift pk to bk

After multiplication: I'm going to call the update method again

_ take shoes off_

keep best practices

try to use error code doc instead of inline validation

no exception handling
don't swallow ( catch ) exceptions unless you have a real good reason


rest call cone: everything needs to succeed, or fail not inbetween.

Never forget @Transactional

unit

component

integration testing

-- ask for defect sev(erity) 4/3

- singleclick
- postman running 
- ssh into it if possible 
- access to gcloud project

- get lpn with ID out of document

```
// PK given in the URL takes the precedence.  
document.put(Lpn.Fields.PK.getCode(), pk);
```


logger.trace(() -> ">> multiplyLpn()"