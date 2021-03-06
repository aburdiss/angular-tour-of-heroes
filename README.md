# Angular.io Tour of Heroes Training Notes

You will need to take a course on TypeScript to get more familiar with Angular in general.

Styles in CSS files are private per component, and will only be loaded in to that component, even if they're loaded onto a page with multiple components with the same classes/selectors. Component CSS files are truly private, similar to CSS modules.

HTML files are the templates, not just static display. HTML files are valid html, but contain different kinds of attributes and bindings that will only work inside the context of an angular framework. It is possible to render an angular HTML file outside of an angular project.

interpolation binding syntax - This is the syntax that angular uses to add variables to the HTML files.

`ngOnInit()` function is where you can put all component initialization logic. Anything that needs to be ran on component setup.

On an `<input>` component, if you use the ngModel prop, and pass to it the name of a piece of state, angular sets up a two-way bridge for the data with that.

`*ngFor` is angular’s repeater directive. It will repeat the element that it is attached to. You can also use interpolation binding syntax inside an `*ngFor`, for things like dynamic routes.

`*ngIf` is angular’s conditional rendering mechanism. If the variable passed to `*ngIf` is not defined, the whole section wrapped by this wrapper will not render. Inside the string that you pass to `*ngIf`, you can just write a standard JavaScript expression that evaluates to a boolean.

To conditionally render classes on an element, you use the `[class.whateverClassItIsYouWant]=“whatever condition evaluates to true to render your class”` syntax

Using brackets around an attribute to an HTML element is angular’s way of property binding. Using this way is a One Way property binding, of sending elements to a component without the need to listen for them to change. If you want the two way binding, you’ll have to use the `[(ngModel)]` attribute.

Services are a great way to share information among classes that don’t know each other.

There’s nothing special about how the angular CLI structures your application. You can move the components into whichever directory you want, and as long as the imports line up your application will work as expected.

For triggering component updates, angular uses observables, and the traditional observable pattern.

For business logic, it is best to put all of that code into a service. Keep components for displaying code, and services for doing the calculations.

This is a great tutorial on JavaScript decorators, which are used throughout Angular!
https://www.sitepoint.com/javascript-decorators-what-they-are/
These decorators accept as an argument an object with metadata about the class they are decorating.

The @Injectable decorator registers a services with the Injector, an object that is responsible for choosing which dependencies to inject with which components. You need this decorator for your component to work properly. The injector won’t actually inject your dependencies to your component if it isn’t specifically using it.

To declare to the injector that your component uses a dependency, you have to add it to the constructor of the component as an argument. This declares your component as an injection site.

The constructor for your Angular component classes shouldn’t do anything. It should have a minimal purpose, such as wiring constructor parameters to properties. Use the ngOnInit lifecycle hook to do things on the start of your component.

Angular uses RxJS for observables. It comes with the `ng new` command.

Services can be injected into other services. This is a practice called “service-in-service”

Angular only binds to public component properties. This is important when working with services, because you have to make them public fields on the components you will use for binding.

When you use a service in your component's HTML template, this binds the service that you imported into your TypeScript template as a constructor parameter.

Adding a colon to a path in a route indicates that that is the parameter for that route, and you can pass data into a component this way.

The Angular `ActivatedRoute` holds information about the current route of the page, and allows you to get things like parameters passed via routes to the components.

The Angular `Location` holds information about the current browser state, and allows you to do things like navigate back to where you were.

TypeScript has a "Non-Null assertion operator".
https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-0.html#non-null-assertion-operator
This tells TypeScript that something isn't or couldn't be null, when TypeScript thinks that it could be.

The Angular HTTPClient returns an RxJS Observable object. Using `HTTPClient.get()` returns what `fetch().then(resp => resp.json).then(data => /* Use the data */)` usually would, in a synchronous API without callbacks. If you want to catch errors, you can use `.pipe()` (from RxJS) on the after calling `HTTPClient.get()` to handle errors.

## IMPORTANT:

Although a component may delegate deleting or adding an element from the server, in Angular, that component is responsible for updating its own display as well.

Observables by default don't do any action unless somethign subscribes. If you are deleting data from a server, your component has to subscribe from your service's delete method, even though your class can't really do anything with the empty observable it returns. But if your class doesn't subscribe, the observable method will not run.

When iterating over an array of observables, it is convention to title the loop variable ending with a dollar sign. `*ngFor` cannot do anything with observables, so you need to pipe the variable to `async`

You can subscribe to a subject just as you would an observable.
