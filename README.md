#Angular 2

**Angular** is a framework for creating Single Page Applications. In a traditional application, visiting a different URL requires a new request/response; a completely new page is loaded onto the client. This leads to sluggish load-time. With Single Page Applications, this is all handled by the client (as opposed to the server and database). The HTML is re-rendered with JavaScript. This is faster. Server-side operations are not entirely eliminated, of course; there are simply minimized. Where the server is not necessary, it is not used. Angular handles request events, routing, and re-rendering of the DOM (through the use of directives, components, data binding, etc).

###angular-cli

We can type `sudo npm install -g angular-cli` to install this tool. Once installed, running `ng new project-name` will create a new project. Then, running `ng serve` will start a development server. We can preview the app at `http://localhost:4200/`.

###Typescript

A superset of JavaScript which is eventually compiled to plain JavaScript. It adds types, classes, modules, etc. Benefits include: strong typing, next-generation JS features (classes, imports, exports), missing JS features (interfaces, generics). We also benefit from using Typescript in this setting because Angular 2 uses Typescript as its main language.

###Components

Components are essentially custom HTML elements.

Decorators (`@Component`) allow us to transform normal Typescript classes into something more powerful ... components for example. Each component in Angular 2 needs HTML to display. This HTML belonging to a component is stored in a template; either in an external file or directly in the .ts file. Styles are optional, but templates *are not*. **Each component needs one and only one template**. The selector is what allows us to use a component throughout our application.

###index.html

The index.html at the root our our `src/` directory is the only file that gets loaded by the server (since Angular is a single-page application framework). This is where we insert our components. Since this HTML file does not have any script tags, how is it that we start or load the Angular app?

The CLI will dynamically add the script imports whenever we run the application; they are added during the compilation/build step. `main.bundle.js` (which can be seen by inspecting element after running the app) contains our code plus all the Angular and 3rd party code. This file also starts our application. The `main.ts` file is the first file to be executed. This bootstraps the `app.module.ts` module, which in turn bootstraps the `app.component.ts` file. We tell Angular that this will be our root component, it recognizes the selector, and then knows that the component template must be rendered in the `index.html` file where it finds the matching selector.

###Templates and Styles

If we want to include inline templates or styles in `app.component.ts`, we can use backticks in order to take advantage of template literals:

```Typescript
@Component({
  selector: 'app-root',
  templateUrl: `
    <h1>just like this</h1>
  `,
  styleUrls: [`
    h1 {
      font-size: 40px;
    }
  `]
})
```

More substantial templates or styles should be included in external files (`app.component.html` and `app.component.css`).

###Adding new components

To create a new component using the CLI, we type `ng generate component new-thing`. You may also use the shorthand `ng g c new-thing`. This will create a directory called "new-thing" within the app directory. In here, we will see four new files:

* new-thing.component.css
* new-thing.component.html
* new-thing.component.spec.ts
* new-thing.component.ts

This component is intended to be inserted into `<app-root>`, not alongside it. This is done by adding the tags `<fa-other></fa-other>` into `app.component.ts` if you have an inline template or in `app.component.html` if you have an external template (given that the value of the "selector" property in the new component is "fa-other"). Keep in mind that when we ask the CLI to generate a new component, it also adds the value of the selector of that component as a value of the "declarations" property AND the name of the file as the associated import in the `app.module.ts` file. (Also keep in mind that the selector needn't be the same as the name of the file).

###Unique selectors

It is a good idea to create prefixed (e.g. "fa-form" or "js-form") selector values in order to avoid clashing with future HTML tags, etc.

###View encapsulation and styling

Angular is able to encapsulate styles (restrict styles to certain components) by inserting unique attributes onto certain elements. We can observe this by inspecting element on some element; we will see attributes that look something like `_ngcontent-dhu-2`. The styles (which are ultimately inserted into the head of the document) will utilize attribute selectors that target these generated attributes.

###Inserting Content

What if we want to add markup inside of custom elements? Imagine we have the following code in our main `app.component.ts`:

```
@Component({
  selector: 'fa-app',
  template: '
    <fa-container>
      <div>
        <h2>Hello</h2>
        <p>World</p>
      </div>
    </fa-container>
  ',
  styles: ['
    h1 {
      color: red;
    }
  ']
})
```

...and this code in our custom component:

```
@Component({
  selector: 'fa-container',
  template: '
    <article></article>
  ',
  styles: ['
    article {
      border: 2px solid gray;
    }
  ']
})
```

Angular, by default, throws away everything within these custom tags and inserts the content of your component template. To carry this out successfully, we need to place `<ng-content></ng-content>` between the article tags. This will allow us to render HTML content within other components.

###Property & Event Binding Syntax

**DOM properties (native)**
```html
<img [src]="...">
<img (click)="...">
```

**Directive properties (built into Angular)**
```html
<img [ngClass]="...">
<img (ngSubmit)="...">
```

**Component properties (built into Angular)**
```html
<cmp [initObj]="...">
<cmp (rndEvent)="...">
```

###Custom Bindings

**Property Binding**: `@Input() propertyName: string;`

**Event Binding**: `@Output() eventName: new EventEmmitter();`

###Two-way Binding

Not the default in Angular 2; it's slow and has some problems. We're often fine without it. Here is an example of how to configure this:

```
@Component({
  selector: 'app-two-way-binding',
  template: `
    <input type="text" [(ngModel)]="person.name">
    <input type="text" [(ngModel)]="person.name">
  `
})
export class TwoWayBindingComponent {
  person = {
    name: 'Max',
    age: 33
  };
}

```
