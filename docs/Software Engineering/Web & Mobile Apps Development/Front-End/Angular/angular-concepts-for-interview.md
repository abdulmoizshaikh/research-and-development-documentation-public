# Angular Concepts for interview

### Decorator:

Decorator are those which enhance the component by adding some features like selector ,templateURL,stylesURL these are called meta data for that class component

Table of Contents

- [Angular Decorators](https://ultimatecourses.com/blog/angular-decorators#Angular_Decorators)
  - [Class Decorators](https://ultimatecourses.com/blog/angular-decorators#Class_Decorators)
  - [Property Decorators](https://ultimatecourses.com/blog/angular-decorators#Property_Decorators)
  - [Method Decorators](https://ultimatecourses.com/blog/angular-decorators#Method_Decorators)
  - [Parameter Decorators](https://ultimatecourses.com/blog/angular-decorators#Parameter_Decorators)
- [Creating a decorator](https://ultimatecourses.com/blog/angular-decorators#Creating_a_decorator)
  - [Decorator functions](https://ultimatecourses.com/blog/angular-decorators#Decorator_functions)
  - [Passing data to a decorator](https://ultimatecourses.com/blog/angular-decorators#Passing_data_to_a_decorator)
- [What Angular decorators actually do](https://ultimatecourses.com/blog/angular-decorators#What_Angular_decorators_actually_do)
  - [Storing metadata](https://ultimatecourses.com/blog/angular-decorators#Storing_metadata)
  - [Chaining decorators](https://ultimatecourses.com/blog/angular-decorators#Chaining_decorators)
- [How decorators are applied](https://ultimatecourses.com/blog/angular-decorators#How_decorators_are_applied)
- [Summary](https://ultimatecourses.com/blog/angular-decorators#Summary)

### Selector

Selector are the property of @Component decorator which assign name to element which we use to render into UI like selector :’app-root’ convention is that its name start with app-(name of element or tag)

We can define selector by
Element name, - Attribute, -class name

E.g:

```jsx showLineNumbers
@Component({
// 1 select by component tag name
// your typically user by element name but you have some cases where you use attribut and class selectors
selector: 'app-servers',

// 2 select by attribute name
// here we can also define selectors as a attribute
// selector: '[app-servers]',

// 3 select by class (note selected by id won't works and sudo selectors like hover and so on also don't work)
// selector: '.app-servers',

// templateUrl: './servers.component.html',
template: `<app-server></app-server>
 <app-server></app-server>`,
styleUrls: ['./servers.component.css']
})
```

```jsx showLineNumbers
<!-- <router-outlet></router-outlet> -->

<app-servers></app-servers>

<!-- now below here angular selects the element by attribute -->
<!-- <div app-servers></div> -->

<!-- selector by class name -->
<!-- <div class="app-servers"></div> -->
```

### Data binding:

Data binding = Communication
Communication between your typescript code (your business logic) and the template(your html code what the user see)
Like you want to show data after fetch from server to your user through html that is the place where data binding come into play

4 forms of data binding we can user data binding in these forms

**Output data**

**One Direction:**<br/>

1. string interpolation (`jsx {{ data }} `)
2. property binding (`[property]=”data”`)

**Second Direction:**<br/>

**React to ( user ) Event 3 Event Binding** ( ( event )= “expression ”) like we can bind click event to show data when ever it occurs

**Two Way binding:**<br/>
Combination of both above directions E.g ( [ ( ngModel ) ] = ”data” )

Square bracket around propert name like [disabled]=”true or false” called property binding
Property binding vs string interpolations
In property binding we show dynamic variables and in string interpolation we use to show user a value property binding we use to change the state of btn or any controled element to change its status like btn enable or disable after click to btn
