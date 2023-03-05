# Flux architecture for ReactJs

**What is Flux?**

Flux is not a framework or library its just an architecture for managing data in unidirectional flow
Like facebook use flux over redux to manage application (react) state

OR

Flux is the application architecture that **Facebook** uses for building client-side web applications. It complements React's composable view components by utilizing a unidirectional data flow. It's more of a pattern rather than a formal framework, and you can start using Flux immediately without a lot of new code.

OR

Flux is an architecture that Facebook uses internally when working with React. It is not a framework or a library. It is simply a new kind of architecture that complements React and the concept of Unidirectional Data Flow.

That said, Facebook does provide a repo that includes a Dispatcher library. The dispatcher is a sort of global pub/sub handler that broadcasts payloads to registered callbacks.

A typical Flux architecture will leverage this Dispatcher library, along with NodeJS's EventEmitter module in order to set up an event system that helps manage an applications state.

Flux is probably better explained by explaining its individual components:

Actions - Helper methods that facilitate passing data to the Dispatcher
Dispatcher - Receives actions and broadcasts payloads to registered callbacks
Stores - Containers for application state & logic that have callbacks registered to the dispatcher
Controller Views - React Components that grab the state from Stores and pass it down via props to child components.

Ref :

https://scotch.io/tutorials/getting-to-know-flux-the-react-js-architecture#:~:text=Wrap%20Up-,
What%20is%20Flux%3F,that%20includes%20a%20Dispatcher%20library.

https://facebook.github.io/flux/docs/in-depth-overview/

https://github.com/facebook/flux

![image](./images/image1.png)

https://github.com/facebook/flux/tree/master/examples/flux-concepts

Clone sample repo of flux example/flux-todoMVC app

https://github.com/abdulmoizshaikh/flux.git

React and Flux:

https://survivejs.com/react/implementing-kanban/react-and-flux/
