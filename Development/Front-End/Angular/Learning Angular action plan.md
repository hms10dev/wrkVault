(Shout Out to Chat GPT:)

1. Learn the basics of JavaScript: 
	1. Angular is built on top of JavaScript, so it's important to have a solid understanding of the language. Start with the basics, such as variables, functions, loops, and conditionals.
2. Familiarize yourself with TypeScript: 
	1. Angular is written in TypeScript, which is a superset of JavaScript that adds static typing and other features. Learn the basics of TypeScript, such as types, interfaces, and classes.
3. Learn Angular fundamentals: 
	1. Once you have a solid understanding of JavaScript and TypeScript, start learning the fundamentals of Angular. This includes components, templates, services, dependency injection, and routing.
4. Build a small application: 
	1. Practice what you've learned by building a small [[example application]], such as a to-do list or a simple calculator. This will help you solidify your understanding of Angular and its concepts.
5. Learn advanced Angular features: 
	1. Once you're comfortable with the fundamentals, start learning more advanced Angular features, such as reactive forms, animations, and server-side rendering.
6. Participate in the Angular community: 
	1. Join the Angular community, such as forums, meetups, or online groups. You can also contribute to open-source Angular projects or participate in code reviews to gain more experience.
7. Keep learning: 
	1. Angular is constantly evolving, so it's important to keep learning and staying up-to-date with the latest changes and updates. Stay updated with Angular news and blogs, attend webinars, or take online courses to keep your knowledge up-to-date.




## JavaScript Basics:



## TypeScript:
- more features than vanilla JS
- SuperSet to JS
- Strongly-typed (vs JS dynamic typing)
- much more robust code that gets checked at time of writing
- gets compiled to JS thanks to the CLI
- Angular is not written in JS becuase a lot of features only exist in TypeScript
- Easy to pick up
- 
- 


# Angular & the command line:

## Running Angular Project Locally :

To start running your Angular project locally using the command line, you will need to follow these steps:

1. Open your terminal/command prompt and navigate to your Angular project directory.
2. Make sure you have Node.js and Angular CLI installed on your machine. You can check whether you have installed these tools by running the following commands in your terminal/command prompt:


```
node -v
```


```
ng version
```


3. Install project dependencies by running the following command in your terminal/command prompt:

```
npm install
```

4. Once the dependencies are installed, you can run your project by using the following command:

```
ng serve
```

5. After running this command, you should see a message indicating that the Angular development server is running and that your application is available at http://localhost:4200/.

6. Open your web browser and navigate to http://localhost:4200/ to view your Angular application.

That's it! You should now be able to run your Angular project locally using the command line.

--- 

## Updating Angular:

To update Angular to the latest version, you can follow these steps:
1. First, check your current Angular version by running the following command in your terminal:

```
ng version
```

2. Next, update the Angular CLI by running the following command:

```
npm install -g @angular/cli
```

3. Once the Angular CLI is updated, you can update your Angular project by navigating to the project directory and running the following command:

```
ng update @angular/core
```

This command will update your Angular project to the latest version of Angular.
If you have any other Angular dependencies in your project, you can update them using the following command:

```
ng update
```

This command will update all the Angular dependencies in your project to their latest versions.

>[!info]
Note: Before updating Angular, make sure to backup your project files and test the updated version in a separate branch or environment to ensure that everything works as expected.



## Tips:

put Angular project on Docker Container


## Popular Commands:

#### Angular commands you have to know

Save this sheet for later and refer to it whenever you need a quick refresher:

  

`ng new projectName`

Creates a new Angular project with the specified project name.
  
---

`ng serve`

Builds the application and starts a web server to serve your application during development.


---

`ng serve --open`

or

`ng serve -o`

Same as ng serve, but also opens your default web browser to the application.

  
---
  

`ng generate component componentName`

or

`ng g c componentName`

Generates a new component with the specified name.

---

`ng generate service serviceName`

or

`ng g s serviceName`

Generates a new service with the specified name.

---  

`ng build`

Builds your application for production, creating a dist/ folder with the output.

---

`ng update`

Checks your application for outdated dependencies, and can also update them.

>[!info]
Remember, these commands should be run in a terminal or command prompt from within your Angular project's root directory.


Happy coding!

Jannick & TutorialsEU

## Components:

- The building blocks of angular files
- composition of HTML, CSS, and TS Class

## One Way Data Binding :
- We can access a component class property in its corresponding view template
- also when we can access a value from view template in corresponding component class property

### What is Data Binding?
- Data Binding in Angular allows us to communicate between a component class and its corresponding view template
- ![[Screenshot 2023-07-13 at 12.03.53 PM.png]]

- Data only flows in one direction
	- This makes code easier to understand and more predictable
	- flow of data has a clear and consistent path
	- **Model (TypeScript Code) → Data flows to → HTML template**
- Here are two common ways to use one-way data binding in Angular:
	1. **Interpolation**: This is the simplest form of one-way data binding, where you use double curly braces (`**{{ }}**`) to display variables from your component in your view.
    
	2. **Property binding**: This allows you to set the property of a DOM element to a value. For example, you might use `**[disabled]="isDisabled"**` to disable a button based on the value of `**isDisabled**`.

## Event Binding
- click)="add(newTask.value)"
- 