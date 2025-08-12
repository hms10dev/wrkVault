Manhattan UI Platform (Mup)
- Flexible Angular app architecture
	- allows for easy source sharing
	- allow for management of products and Dependencies from MUP CLI
	- They allow application pages to be portable and easier to upgrade

# [File System Layout](https://manhattanassociates.atlassian.net/wiki/spaces/CLOUDUI/pages/1142595241/Manhattan+UI+Platform+MUP#File-System-Layout)

Mup architecture follows a specific file structure:
![[Pasted image 20230509102701.png|400]]

## products
- Bitbucket repos that provide Angular code _specific_ to your MUP application. MUP applications can have multiple products in them . 
- found within ==src/app/products== folder

## Dependencies
- Bit bucket repos that provide Angular code and functionality for _any_ MUP application. 
- by default, ==dependency ui-sc-core== is added to your application. ==ui-sc-core== provides basic functionality to your MUP application so that it integrates with Manhattan cloud structure
	- (i.e. login support, i18n support, logger support, 404 errors, and menu support).
- found within ==src/app/deps== folder


## MUP CLI

- command line interface that allows a user to create a new MUP application of interact with an already exisiting MUP application. Through the MUP CLI a developer can manage products and dependencies. A Lsit of availiable commands can be found at the end of this section. The MUP CLI uses MUP STARTER
- the MUP application will be named as ==ui-app-<app_name>,== and will contain the products and dependencies necessarry for development.

## MUP STARTER
- A template used to generate your application. MUP STARTER provides MUP specific config files 

## Why use MUP?
- Scenario: dev is tasked with hot-fix that needs issue to be replicated. 
	- this involves chekcing out commits and branches for many repos.
	- more complex the issue, the more tedious this process is. 
	- have to spend time setting up things correctly, which takes away from time actually fixing the issue.
- MUP allows for products and deps to be added and managed from the command line, removing the need to dedicate copious amounts of time to setup. 
- MUP's Biggest advantages:
	- Easy Developer setup
	- Code portability across projects,
	- Easier code adoptins due to build configurability
	- [[Metadata Overview]]

## What is the Metadata Framework?
- [[Metadata Overview]]


# Setting up a MUP Application

- fairly strightforward process
- _Adopting the MUP app within a facade is another story however, involving setting up the required docker containers, Jenkins builds, etc. But, before we can do that we must have a MUP app in the first place._

## Prerequisites:

- NVM.
- Once nvm is installed, run the following commands to install node v10.16.0 and use this version:

```
nvm install 10.16.0 nvm use 10.16.0
```

**Note**: To see all versions of npm available, run this command:

```
nvm ls-remote
```

**MUP-CLI**: This will let you create your MUP app and add/manage products and dependencies for it.

```
npm install -g @manh/mup-cli
```

1.  Clone the MUP-CLI repo: [manhattanassociates/mup-cli](https://bitbucket.org/manhattanassociates/mup-cli/src/master/)
    
2.  cd into the cloned MUP-CLI repo
    
3.  Run the following commands:
    
 ```
   npm install
   npm run build
   npm link
```
    

This will link MUP to this repo’s src folder and pull any updates from here

## MUP App Setup

_Now for the main event!_ Find a directory that you want to install the MUP app in. From there, run:

```
mup start
```

- The CLI will ask for a project name. The standard for MUP apps is **ui-app-<app_name>**. 
- Once a name is entered, the app should be created and you can cd into it. 
- Commit and push your changes from this repo. 
- _Voila!_ You’ve created your MUP application.

# [Enabling the MUP UI and Metadata Generation](https://manhattanassociates.atlassian.net/wiki/spaces/CFW/pages/1167472328/How+to+Use+FrameworkUIFacade+s+MUP+Application#Enabling-the-MUP-UI-and-Metadata-Generation)

We’ll start off by running `npm install` in your MUP app to install all dependencies.

Next, we’ll go into the **dependencies.json** in the src/ folder and add ui-sc-common, which will enable us to generate metadata UIs. The dependencies.json should look like this:

```
{ 
	"dependencies": {}, 
	"devDependencies": {}, 
	"repoDependencies": { 
		"common": { 
			"upstream": { 
				"protocol": "ssh", 
				"host": "bitbucket.org", 
				"repoOwner": "manhattanassociates", 
				"repo": "ui-sc-common.git", 
				"trackingBranch": "master"
				} 
			}, 
			"core": { 
				"upstream": { 
					"protocol": "ssh", 
					"host": "bitbucket.org", 
					"repoOwner": "manhattanassociates", 
					"repo": "ui-sc-core.git", 
					"trackingBranch": "master" 
					} 
				}
			}, 
			"webComponents": {} 
		}
```


...


# MUP INIT
- what does it do?




# MUP tips and tricks:
- front end tips:
  
 is there a way to formate/truncate the numbers on the ui to a specific tenths place on the UI ? I thought I saw something like that on the docs, but I wanted to confirm real quick.
 
  it's this field: SupportsPrecision in attributes.json


```json

{

"AttributeName": "ActivityDuration",

"AttributeType": "double",

"SupportsPrecision": 4,

"UID": "AttributeConfig10"

 }
 ``````

you can also set SupportsEnforcePrecision = true if you want to force the precision to always show that number of spaces and not drop trailing 0s
