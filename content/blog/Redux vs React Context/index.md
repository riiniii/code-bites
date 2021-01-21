---
title: Redux vs React Context
description: "A code-bite on Redux vs React Context."
categories: [javascript, react]
comments: false
---

The ever-burning question of what really is the difference between Redux and React Context, and when should we use Redux or React Context...?

When we look at things from a very, very, very... very... high level, it may seem that they do the same things. Both are able to update values from one part of your React web application and have the updated values reflected in another. From a very high level this stands true. But when we zoom in there are, of course, differences.

Here are the differences in a nutshell:

### React Context

React Context is **not** a state management tool like Redux is, it's actually based on the dependency injection pattern. Thus, React Context through its dependency injection pattern supports abstractions, makes it easier to decompose program components, all with the wonderful feature of allowing props to be accessible through many levels of components without props drilling. React Context only supports passing down one value, though that value can be an object containing many values.

### Redux

Redux on the other hand is fully fledged application state manager that can be used across many different languages and frameworks (not just React!). Redux is good for large and complicated web applications, and is good for visualizing and understanding well how the changes were made over time.

Redux is good for when you want to add indirection to decouple things from "what happened" to "how things change" (parent to child components)(2).

Here's a comprehensive bullet point taken from (1):

- Wanting to write your state management logic completely separate from the UI layer
- Sharing state management logic between different UI layers (such as an application that is being migrated from AngularJS to React)
- Using the power of Redux middleware to add additional logic when actions are dispatched
- Being able to persist portions of the Redux state
- Enabling bug reports that can be replayed by developers
- Faster debugging of logic and UI while in development

### State Management

State management is how state changes over time. That means, we have to have these three functionalities: _store_ an initial value, _read_ the current value, _update_ a value (1). React Context by itself does not do that. Firstly, the value of React Context is decided by it's parent component. Secondly, React Context with useState or useReducer gives us the functionality to update the values in context. Together, it finally gives us the functionality of state management. By itself, React Context is not enough to be considered state management.

### Use What, When?

Use React Context for when you want values easily accessible to a part of your React component tree, without props drilling.

You can use React Context and useReducer together for state management of a particular portion of your React application.

Use Redux if you have a lot of application state needed to be managed throughout your app, or for any of the bullet point reasons mentioned under the Redux section.

Information gathered from the great blog posts written at "[Why React Context Is Not a State Management Tool and Why It Doesn't Replace Redux](https://blog.isquaredsoftware.com/2021/01/blogged-answers-why-react-context-is-not-a-state-management-tool-and-why-it-doesnt-replace-redux/),(1)" "[Redux, Not Dead Yet!](https://blog.isquaredsoftware.com/2018/03/redux-not-dead-yet/),(2)" "[When and When Not To Reach For Redux](https://changelog.com/posts/when-and-when-not-to-reach-for-redux)," and "[You Might Not Need Redux.](https://medium.com/@dan_abramov/you-might-not-need-redux-be46360cf367)"

For information on dependency injections, information was gathered from "[Dependency Injection in React](https://itnext.io/dependency-injection-in-react-6fcdbd2005e6)"
