# React

1. Is React a framework or a library?
   1. TODO: finish
2. Describe how client-side routing is handled in React?
   1. TODO: finish
3. Describe how state works in React, and in React with a Flux pattern (ie, Redux)
   1. TODO: finish
4. Could you describe the React component lifecycle? When in the lifecycle would you bind to events?
   1. TODO: finish
5. When do you prefer to use the Ref attribute?
   - When you need access to the underlying DOM node (filePicker, media playback, certain animations, working with certain mapping libraries like Leaflet)
6. How do you decide between using a functional VS a class component?
   - Two big reasons to use Class Components are
     - you need state
     - you need to use lifecycle methods, like componentDidMount() or componentDidUpdate()
7. What's the difference between a pure component and a regular component?
   - TODO: complete
8. What sort of patterns do you employ when developing forms in React?
   1. Normally controlled components, sometimes uncontrolled (with refs) if I need to customize the validity messages and want to use the DOM api for that.
9. What's the difference between:
   1. A React component & A React element
      1. React Elements
         1. plain JavaScript objects. You can think of them as descriptions of what you want to see on the screen. JSX tags `<i_an_an_html_tag>` OR `<I_Am_A_Component>` transpile to `React.createElement()` function calls when transpiled through Babel. React reads these objects and uses them to keep the DOM up to date.
         2. React elements are immutable. Once created, you cannot change an element's attributes of children (ie, its props)
      2. React Components
         1. In a similar way to how JavaScript functions accept input(s) & return output(s) based on that input, React components accept an arbitrary input object (called props) & return ONE (1) React Element.
         2. A big use case for React Components is the React Element they return can be customized based on the props that component receives. This vastly improves the reusability & modularity of the code.
   2. state and props in React
      1. state
         1. private
         2. fully controlled by the component
         3. expected to change
         4. state updates
            1. done through `setState()` - NOT directly
            2. merged into existing state
            3. may be asynchronous
      2. the component can choose to pass some of its state to components BELOW it in the tree, as props
      3. props
         1. immutable (props are read-only)
   3. controlled VS uncontrolled components
      1. controlled - the containing React conponent contains the state & defines the input element value
      2. uncontrolled - the input element (for browsers, the actual DOM node) contains its own internal state
10. Explain:
    1. Virtual DOM
       1. TODO: finish
    2. `React.Fragment`
       1. Formally, React Fragments allow you to return a list of children from a component without adding extra nodes to the DOM
       2. ie, you can still return only one thing from a component (as React requires), in cases where if that one thing was a `<div>`, it would cause invalid / excessive HTML
    3. Strict mode in React
       1. TODO: finish
    4. JSX. Can you have JavaScript inside JSX? If so, how?
       1. TODO: finish
    5. Event handlers in React
       1. TODO: finish
    6. refs
       1. refs are a way to get references to:
          1. the underlying DOM node (for browsers)
          2. mounted instance of the component
       2. refs are used when you need that direct reference (ex, for accessing state if it lives in the DOM node)
          1. don't user them if you can avoid it (React pattern of lifting state up & passing props is generally preferred)
          2. use cases:
             1. managing focus, text selection, or media playback
             2. triggering imperative animation
             3. integrating with existing or already deployed third party DOM libraries
          3. `React.createRef()` or callback refs are preferred, instead of string refs & `ReactDOM.findDOMNode()`
    7. forwardingRefs
       1. TODO: finish
    8. Context in React
       1. Context in React is way to pass data through the component tree, without having to explicitly pass that data at each level (ie, the component that needs the data could be 50 levels down from where the data lives, manually wiring that data through 50 intermediate components leads to very WET code)
       2. Before using Context, consider if using component composition might be simpler (ie, defining the component that needs the data in the component where the data lives as state, then passing that whole component as a prop - instead of passing each piece of data as a separate prop)
       3. Which solution is better depends heavily on the number of components, props, nesting, etc...
       4. Common use cases for Context (instead of component composition) are
          1. themes
          2. current locale
          3. data cache
       5. React Context is an object

         ```JavaScript
         const MyContext = React.createContext(defaultValue);
         // you wrap any components you want to be able to access context inside
         <MyContext.Provider value={the_value_components_will_be_able_to_access} />
         // descendent components are also able to acess that value
         ```

       6. In class components:
          1. You assign `MyClass.contextType` to the context object you created earlier
          2. This makes the value defined in the nearest ancestor Context Provider available in this class at `this.context`
       7. In function components:
          1. You use `<MyContext.Consumer>` with a child of a function that accepts the value from the Context. That function returns a React Element
       8. Using the API, you can only consume a single Context. To consume more than one, either next several `<MyContext.Provider>`s, or consider using Render Props.
11. What are React Hooks?
    1. [An approach to accessing many useful React features that formerly required classes](https://reactjs.org/docs/hooks-intro.html) (state, lifecycle methods, etc...)
12. What are the main problems that React Hooks aim to solve?
    1. Classes in JavaScript are potentially difficult for developers to work with & [allow coding certain patterns that prevent many performance optimizations](https://reactjs.org/docs/hooks-intro.html#classes-confuse-both-people-and-machines).
    2. Using lifecycle methods enforces splitting related logic based on when-that-logic-needs-to-run. [Hooks allow for other groupings of related logic](https://reactjs.org/docs/hooks-intro.html#complex-components-become-hard-to-understand).
    3. Hooks allow you to [share stateful logic between components](https://reactjs.org/docs/hooks-intro.html#its-hard-to-reuse-stateful-logic-between-components) (sharing the LOGIC, not the state. The state remains unique.)
13. What are the rules of using React Hooks?
    1. TODO: finish
14. Can you use React Hooks inside classes? why? / why not?
    1. TODO: finish
15. Do React Hooks have any naming conventions? why? / why not?
    1. TODO: finish
16. How would you create & update state with a React Hook?
    1. invoke the `useState()` method with the initial state you want to store
    2. it will return an array, with
       1. 1st element - the current value of that state
       2. 2nd element - function to update that state value
       3. the convention is to use [array destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) to create the local variables that point to the actual state value & associated updater returned from `useState`. Naming these variables is up to the developer.
    3. These values - the state & its associated updater function are LOCAL to the component, so they can be passed to event handlers, for instance, without any fuss (ie, no `bind()` calls necessary)
    4. Updating that state is as simple as invoking the updater function with the new value
17. Describe at least two (2) approaches for storing multiple state values with `useState()`
    1. Store all the values in a wrapper object, and have that wrapper object be what gets passed to `useState`
    2. React supports multiple calls to `useState` in the same component, each referring to a different slice of state
18. How is `useState()` different from `this.setState()`?
    1. TODO: finish
19. How would you perform side effects using React Hooks in a React component?
    1. invoke the `useEffect()` hook
    2. [you pass `useEffect()` a function](https://reactjs.org/docs/hooks-effect.html#example-using-hooks) - by convention called an effect - and by default **React guarantees that it will invoke this effect after every render, including the first one**. This is how you get logic to run AFTER React has updated the DOM.
    3. The effect you pass utilizes closure to retain access to the function component's scope (ie, props / state / etc...). Contrast this with how class components use a separate, React-specific API to interact with state
20. What are some common example of side effects in a component?
    1. data fetching
    2. setting up a subscription
    3. manipulating the DOM with the browser API
21. List some examples of side effects in React that don't require cleanup?
    1. manually manipulating the DOM
    2. network requests
    3. logging
22. How is `useEffect()` different from class component lifecycle methods?
    1. TODO: finish
    2. TODO: finish effects don't block the browser from updating
23. Are effects reused? why? why not?
    1. TODO: finish
24. Describe an approach for when your effect requires cleanup? What advantages does this approach have over classes?
    1. Optionally, you can return a function from your effect. React will invoke this function before the component unmounts (ie, when `componentWillUnmount` would run). React also invokes this function before each re-render, which [helps prevent common bugs.](https://reactjs.org/docs/hooks-effect.html#explanation-why-effects-run-on-each-update)
    2. This approach allows you to keep related code together (encapsulation), rather than forcing a split based on the React lifecycle
25. What's one way of preventing effects from running after every re-render?
    1. `useEffect` optionally takes a second argument, an array (values from props / state), that React will compare with their current value(s), and [only run the effect if those values differ](https://reactjs.org/docs/hooks-effect.html#tip-optimizing-performance-by-skipping-effects).