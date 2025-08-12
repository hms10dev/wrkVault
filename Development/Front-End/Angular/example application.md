https://angular.io/start

- Angular applications are built with components. 
	- component: define areas of responsibility in the UI that let you reuse sets of UI functionality.
 | **COMPONENT PART** | **DETAILS** |
|--------------------|-------------|
| A component Class                   |   Handles data and funct.          |
|  An HTML Template                  |  Determines the UI           |
|  Component- Specific styles                  |   Define the look and feel          |

The guide we are going through today demonstates building an app with the following components:

| **COMPONENT** | **DETAILS** |
|---------------|-------------|
| `<app-root>`              |   The first component to load and the container for the other components          |
| `<app-top-bar>`              |The store name and checkout button|
|`<app-product-list>`               |   The product list          |
| `<app-product-alerts>`             |      A component that contains the application's alerts       |

## Example Screen Shot:

![[Screenshot 2023-05-04 at 10.11.41 AM.png | 500]]

## Notes:

- With [`*ngFor`](https://angular.io/api/common/NgFor), the `<div>` repeats for each product in the list.
	- [Structural directives](https://angular.io/guide/structural-directives) shape or reshape the DOM's structure, by adding, removing, and manipulating elements. 
	
- On a `<p>` element, use an [`*ngIf`](https://angular.io/api/common/NgIf) directive so that Angular only creates the `<p>` element if the current product has a description.

- The [`@Component()`](https://angular.io/api/core/Component) decorator indicates that the following class is a component. It also provides metadata about the component, including its selector, templates, and styles.
	- key features:
		- -   The `selector`, `app-product-alerts`, identifies the component. 
		- By convention, Angular component selectors begin with the prefix `app-`, followed by the component name.
		-   The template and style filenames reference the component's HTML and CSS
		-   The @Component() definition also exports the class, `ProductAlertsComponent`, which handles functionality for the component
Example Code:
```
@Component({
  selector: 'app-product-alerts',
  templateUrl: './product-alerts.component.html',
  styleUrls: ['./product-alerts.component.css']
}) 
export class ProductAlertsComponent {

}
```

>[!info]
>In new components, the Angular Generator includes an empty `constructor()`, the [`OnInit`](https://angular.io/api/core/OnInit) interface, and the `ngOnInit()` method. Since these steps don't use them, the following code examples omit them for brevity.

For more information on communication between components, see [Component Interaction](https://angular.io/guide/component-interaction "Component interaction").