# Redux

1. What is Redux?
   1. Implementation of the Flux pattern, which is a state management solution

|Pros|Cons|
|----|----|
|Centralizes application's state in one place, where all UI components can access it|Complexity|
|Makes data flow transparent & predictable, ie predictable state changes|Verbosity|

2. When / why would you use redux?
   1. The same piece of application state needs to be mapped to multiple application components
      1. ie, session state
   2. Global components that can be accessed from anywhere
      1. notifications, tooltips, modals, etc...
   3. Too many props are being passed through multiple levels of components
   4. state management using setState is bloating the component
   5. caching page state
      1. ie, search input values, expanded / collapsed accordians
   6. Keeping a history of actions, which allows:
      1. time travel debugging
      2. maintaining an undo history
      3. user actions & state snapshot for reproducing errors
      4. travel between the state history during development, for easier-to-reason-about TDD
3. When should you NOT use redux?
   1. Tight budget (it will take too long)
   2. small to medium size apps (probably overkill)
   3. Simple UI / data flow (probably overkill)
   4. Static data OR page is refreshed on every change
4. How would you respond to the argument that it's better to start with Redux because state management will get messy sooner or later, and it's better to have the right foundation for the project
   1. Redux is a tool that solves a certain set of problems, and if your project is never likely to encounter those problems, using Redux is unnecessary.
5. Describe Redux's architecture at a high level
   1. One store, which holds state for the whole app
      1. other Flux implementations may use multiple stores
   2. Changes to state are represented through redux actions - plain objects - which describe what happened & (optionally) contain some data
   3. Action creators are functions that return actions
   4. reducers are functions that handle some particular slice of the redux store's state
      1. pure functions
      2. arguments of state & action
      3. return new state
      4. multiple reducers can be composed together
      5. every reducer is invoked for every action
   5. There's often a mapping between redux & the presentational framework (like React)
      1. A common way to do this is to wrap React components in a component generated from the `connect()` function from the react-redux package
      2. react-redux provides a `<Provider>` component that makes the redux store available to any child component
6. Why is it important the reducers are pure functions, & do NOT mutate state?
   1. TODO: finish
7. Describe middleware in Redux
   1. middleware in redux is a function that wraps the store's dispatch method, performing some work
   2. Then, at some point later, the middleware calls the store's dispatch method, of the next middleware in the chain
   3. middleware functions can be chained