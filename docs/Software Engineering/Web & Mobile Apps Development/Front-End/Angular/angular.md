# Angular

https://stackblitz.com/edit/angular-xrkntz?file=src%2Fapp%2Fproduct-details%2Fproduct-details.component.html

**Error fixing**

must declare component in declaration before use it

```bash showLineNumbers
Add FooterComponent in declaration.

declarations: [
AppComponent.
FooterComponent
]
```

https://stackoverflow.com/questions/59212318/angular-6-cant-bind-to-ngif-since-it-isnt-a-known-property

**RouterModule**

router module is used for routing in angular

**Router-outlet**

router-outlet is used for render component for given path in routermodule

**routerLink**

like `<Link to="path" >` in react

```jsx showLineNumbers
<a
[title]=""product.name + ' details'""
[routerLink]=""['/products', product.id]"">
{{ product.name }}
</a>
```

**ActivatedRoute**

ActivatedRoute is specific to each component that the Angular Router loads. ActivatedRoute contains information about the route and the route's parameters.

https://angular.io/start/start-routing

[ ] **Property binding [ ]** lets you use the property value in a template expression.
e.g

```jsx showLineNumbers
<a [title]=""product.name + ' details'"">
{{ product.name }}
</a>
```

( ) **Event binding** uses a set of parentheses, ( ) e.g

```jsx showLineNumbers
<button (click)=""share()"">
Share
</button>
```

angular generator slackbiz

https://stackoverflow.com/questions/58881956/angular-generator-vscode-plugin-similar-to-one-from-angular-documentation
https://marketplace.visualstudio.com/items?itemName=cyrilletuzi.angular-schematics

**@Component()**

decorator

Open product-alerts.component.ts. The @Component() decorator indicates that the following class is a component. @Component() also provides metadata about the component, including its selector, templates, and styles.

The @Component() definition also exports the class, ProductAlertsComponent, which handles functionality for the component.

**@Input()**

In the ProductAlertsComponent class definition, define a property named product with an @Input() decorator.

The @Input() decorator indicates that the property value passes in from the component's parent, ProductListComponent.

```jsx showLineNumbers
import { Component, OnInit } from "@angular/core";
import { Input } from "@angular/core";
import products from "../products";

@Component({
  selector: "app-product-alerts",
  templateUrl: "./product-alerts.component.html",
  styleUrls: ["./product-alerts.component.css"],
})
export class ProductAlertsComponent implements OnInit {
  constructor() {}

  ngOnInit() {}
}
```

```jsx showLineNumbers
<app-product-alerts
[product]=""product"">
</app-product-alerts>"

```

**@Output()**

Pass data to a parent component

@Output() notify = new EventEmitter();

https://angular.io/start#pass-data-to-a-parent-component

**Injectable Or dependency injection**

https://angular.io/guide/dependency-injection
