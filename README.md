#Angular 2

**Angular** is a framework for creating Single Page Applications. In a traditional application, visiting a different URL requires a new request/response; a completely new page is loaded onto the client. This leads to sluggish load-time. With Single Page Applications, this is all handled by the client (as opposed to the server and database). The HTML is re-rendered with JavaScript. This is faster. Server-side operations are not entirely eliminated, of course; there are simply minimized. Where the server is not necessary, it is not used. Angular handles request events, routing, and re-rendering of the DOM (through the use of directives, components, data binding, etc).

###angular-cli

We can type `sudo npm install -g angular-cli` to install this tool. Once installed, running `ng new project-name` will create a new project. Then, running `ng serve` will start a development server. We can preview the app at `http://localhost:4200/`.

###Typescript

A superset of JavaScript which is eventually compiled to plain JavaScript. It adds types, classes, modules, etc. Benefits include: strong typing, next-generation JS features (classes, imports, exports), missing JS features (interfaces, generics). We also benefit from using Typescript in this setting because Angular 2 uses Typescript as its main language.
