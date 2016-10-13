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
