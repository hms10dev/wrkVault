2023-04-24
9:42

## [[MUP]] Screen

- for MUP its basically JSON plug and play
- generate UI metadata screen using the base and then edit as needed 


## There will be a seperate session (Tuesday @ 9 to cover metadata framework)

# UI Design Presentation Notes

* MUP- One single UI app containing one or more applicaton
* Shares code with each MUP app in form of dependencies
* CSS4 variables and theming
* Has mobile support
* MUP-CLI used to maintain and manage MUP application

### Elements:
![[Screenshot 2023-05-30 at 3.59.24 PM.png]]

### MUP Framework Repositories 
- Command Line Interface and Starter
1. mup-cli 
	1. based on Ionic CLI
	2. modified for Ionic 4 and plays nice with ManH Cloud offerings
	3. Contains common set of commands to 
		1. get started from scratch 
		2. start from exisiting project( mup init)
		3. incr. productivity
		4. Run tests
		5. Pull latest code, check outdated projects
		6. and repair node modules installations
2. mup-starter
	1. Template Project
	2. This repo is the themplate used by CLI to generate Ionic 4 application
	3. needed only for creating a new application
	4. once made, create and add to bit bucket

### MUP Dependencies
- Core and Common
- [Bitbucket repos that conatin all the ionic/ angular code that can be shared across other MUP applications]
1. ui-sc-core
- Core screens and services
- Login support, i18n support, logger support, 404 errors and menu support
	- Breadcrumb
	- Hamburger Menu 
	- Error validation popup
	- idle overlay
	- translate pipes
	- Data model for cards, search filter, attribute filter, etc.
2. ui-sc-common
- Common components and services
- Dynamic UI builder
- Table views
- Tooltip
- Actions, dropdown list, slider etc.
- List expand, grid expand etc.

### Allocation UI APP archetecture:
![[Screenshot 2023-05-30 at 4.09.10 PM.png]]


![[Screenshot 2023-05-30 at 4.09.26 PM.png]]

### ui-allocation Repository
- important files
- dependencies.json - all external dependencies(npm, web-components) are listed here. ==Keep it out of the root "package.json" file!
- /assets folder: place all your assets here ==Do not put inside the root aszets folder++
- **themes.scss:** all custom styling goes here (CSS4 variables)





# SCP - Components

- ![[Screenshot 2023-06-06 at 11.16.08 AM.png]]