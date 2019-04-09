## Errors
- p. 31
  - `But first thing’s first` -> `things`
- p. 16
  - `accepts an array as it’s argument` -> `its`

## Introduction
### 19: Running Code Examples
- `npm install`
- `npm start`
### 20: Angular CLI
- `ng serve`
- `ng build`
- `ng e2e`
### 22: Getting Help
- Community chat room: https://gitter.im/ng-book/ng-book
- Email: mailto:us@fullstack.io

## Writing Your First Angular Web Application
### 4: Node.js and npm
- Instal Node directly; using homebrew has been known to cause some issues
- `npm -v`
- `npm install -g typescript`
- `npm install -g @angular/cli`
- `ng --version`
- `brew install watchman`
- `ng --help`
### 6: Example Project
- `ng new angular-hello-world`
- `tree -F -L 1`
  - Can be installed via `brew install tree`
- https://github.com/ReactiveX/rxjs/issues/4540
- `ng serve`
- http://localhost:4200
- `ng serve --port 9001`
### 12: Making a Component
- `ng generate component hello-world`
- 14:
  - Notice that we suffix our TypeScript file with .ts instead of .js The problem is our browser doesn’t know how to interpret TypeScript files. To solve this gap, the ng serve command live-compiles our .ts to a .js file automatically.
  - Notice that the structure of this import is of the format import { things } from wherever. In the { things } part what we are doing is called destructuring. 
- 15:
  - Personally, if our templates are shorter than a page, we much prefer to have the templates alongside the code (that is, within the .ts file). When we see both the logic and the view together, it’s easy to understand how they interact with one another.
- 16
  - Angular uses a concept called “style-encapsulation” which means that styles specified for a particular component only apply to that component.
  - You may have noticed that this key is different from template in that it accepts an array as it’s argument. This is because we can load multiple stylesheets for a single component.
- 19
  - On the template notice that we added a new syntax: {{ name }}. The brackets are called template tags (or sometimes mustache tags).
  - Whatever is between the template tags will be expanded as an expression. Here, because the template is bound to our Component, the name will expand to the value of this.name i.e. 'Felipe'.
- 21
  - The first change to point out is the new string[] property on our UserListComponent class. This syntax means that names is typed as an Array of strings. Another way to write this would be `Array<string>`.
- 22
  - The *ngFor syntax says we want to use the NgFor directive on this attribute.
  - The value states: "let name of names". names is our array of names as specified on the UserListComponent object. let name is called a reference. When we say "let name of names" we’re saying loop over each element in names and assign each one to a local variable called name.
  - Note that the capitalization here isn’t a typo: NgFor is the capitalization of the class that implements the logic and ngFor is the “selector” for the attribute we want to use.
- 25
  - To pass values to a component we use the bracket [] syntax in our template - let’s take a look at our updated template:
- 26
  - In Angular when we add an attribute in brackets like [foo] we’re saying we want to pass a value to the input named foo on that component.
- 27
  - ng will look at the file angular.json to find the entry point to our app.
- 28
  - main.ts is the entry-point for our app and it bootstraps our application
  - We use the AppModule to bootstrap the app. AppModule is specified in src/app/app.module.ts
  - AppModule specifies which component to use as the top-level component. In this case it is
     AppComponent
  - declarations
    - declarations specifies the components that are defined in this module. This is an important idea in Angular
    - when we generated a new component, the ng tool assumed we wanted it to belong to the current NgModule.
- 29
  - imports
    - imports describes which dependencies this module has.
  - providers
    - providers is used for dependency injection. So to make a service available to be injected throughout our application, we will add it here.
  - bootstrap
    - bootstrap tells Angular that when this module is used to bootstrap an app, we need to load the AppComponent component as the top-level component.
#### The Application Component
- 33
  - We tell Angular we want to respond to an event by surrounding the event name in parentheses ().
- 34
  - Notice that the addArticle() function can accept two arguments: the title and the link arguments. We need to change our template button to pass those into the call to the addArticle(). We do this by populating a template variable by adding a special syntax to the input elements on our form. 
- 35
  - Binding `input`s to values
    - Notice that in the input tags we used the # (hash) to tell Angular to assign those tags to a *local variable*.
    - This markup tells Angular to *bind* this `<input>` to the variable `newtitle`. The `#newtitle` syntax is called a *resolve*. 
    - `newtitle` is now an **object** that represents this `input` DOM element (specifically, the type is `HTMLInputElement`). Because `newtitle` is an object, that means we get the value of the input tag using `newtitle.value`.
  - Binding actions to events
    - On our button tag we add the attribute `(click)` to define what should happen when the button is clicked on.
#### Adding the Article Component
- 39
  - Notice that we can use template strings in **attribute values**, as in the href of the a tag: `href="{{ link }}"`.
- 41
  - In Angular, a component *host* is the **element this component is attached to**. We can set properties on the host element by using the `@HostBinding()` decorator. In this case, we’re asking Angular to keep the value of the host elements class to be in sync with the property `cssClass`.
  - Using the `@HostBinding()` is nice because it means we can encapsulate the `app-article` markup *within* our component. That is, we don’t have to both use an `app-article` tag and require a `class="row"` in the markup of the parent view. By using the `@HostBinding` decorator, we’re able to configure our host element from *within* the component.
