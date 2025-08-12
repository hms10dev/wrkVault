
When testing and wanting to see live changes locally, go to /Users/hsylla/Desktop/components/UI/ui-app-activeinventory/proxy.conf.js,

Then allocate a freedom VM, change the testing url in this file to correspond with the freedom VM url, 

but never check-in the changes, always revert back to original URL from file when checking in code for the UI component.


use the following url to check : https://gcpside-pfio-ca.manh-dev.com
Front end changes


First things first:

angular 14 adoption issue,
check docs Shreesh sent
	https://manhattanassociates.atlassian.net/wiki/spaces/CLOUDUI/pages/4091380178/Angular+14+upgrade+steps
- [x] check diff in angular.json and apply those changes :)
ask who did angular 14 adoption in standup tomorrow (Harsha)



## Actual Changes:

So the Angular 15 adoptions seems to be incomplete, hence the problems logging into localhost/8100.
The following are the changes I made to `angular.json` *(/Users/hsylla/Desktop/components/UI/ui-app-activeinventory/angular.json)* in order to make sure it runs locally correctly:


### Line 16:
**Old:**
```json
"baseHref": "/ai/",
```

**Change:** (--)
```json
"baseHref": "/",
```



### Line 148:
**Old:**
```json
},

"production": {

"budgets": [

{
```

**Change:** (++)
```json
},

"production": {

"baseHref": "/ai",

"budgets": [

{
```



### Line 16:
**Old:**
```json
},

"production-with-proxy": {

"budgets": [

{
```

**Change:** (++)
```json
},

"production-with-proxy": {

"baseHref": "/ai",

"budgets": [

{
```
