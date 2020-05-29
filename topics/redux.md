# Redux

1. What is Redux?
   1. Implementation of the Flux pattern, which is a state management solution

|Pros|Cons|
|----|----|
|Centralizes application's state in one place, where all UI components can access it|Complexity|
|Makes data flow transparent & predictable, ie predictable state changes|Verbosity|

2. When / why would you use redux?
   1. The same piece of application state needs to be mapped to multiple application components
      1. ie, session state`
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
7. Describe
   1. Middleware in Redux
      1. middleware in Redux is a function that wraps the store's dispatch method, performing some work
      2. Then, at some point later, the middleware calls the store's dispatch method, of the next middleware in the chain
      3. middleware functions can be chained
   2. The `redux-actions` package? What benefits does it provide?
      1. [`redux-actions`](https://redux-actions.js.org/) (or packages like it) provide a set of utility / wrapper functions that can make working with actions / action creators, and the reducers that handle those actions:
         1. less verbose
         2. more organized
         3. more standardized
   3. Reselect
      1. Provides a utility function that creates [memoized Redux selectors](https://github.com/reduxjs/reselect#creating-a-memoized-selector), given
         1. one or more input-selector functions
         2. a transform function, that actually returns the value in question from the store
      2. [These memoized selectors are composable](https://github.com/reduxjs/reselect#composing-selectors) (ie, they themselves can be input-selectors to the utility function that returns yet another memoized selector)
   4. Container VS Presentational components. Are there other names for these?
      1. In Redux (or Flux patterns more generally) it can be helpful (easier to read, reason about, maintain) to [split code that contains the business logic](https://redux.js.org/basics/usage-with-react) (event handlers, connecting to the store, etc...) from code that renders the actual DOM nodes. The way this has evolved is with two components, Container & Presentational
         1. Container Components
            1. have access to the store, its dispatch method, etc...
            2. contain the business logic
            3. render an associated presentational component
         2. Presentational Components (sometimes called dumb)
            1. Rely on the container components for all of their inputs (through props)
            2. render the actual DOM nodes
            3. do NOT have direct access to the the store
      2. The usefulness of splitting code like this scales with the size & complexity of the app, so it's better to carefully consider whether this pattern is appropriate, rather than automatically doing this every time.