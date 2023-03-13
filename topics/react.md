# React

1. Is React a framework or a library?
   1. Library. React is a JavaScript library for rendering user interfaces (UI)
2. React is declarative. Describe what that means
   1. Declarative programming means describing the UI for each visual state rather than micromanaging the UI through imperative programming
3. Describe how client-side routing is handled in React?
   1. TODO: finish
4. Describe how state works in React, and in React with a Flux pattern (ie, Redux)
   1. TODO: finish
5. Could you describe the React component lifecycle? When in the lifecycle would you bind to events?
   1. TODO: finish
6. When do you prefer to use the Ref attribute?
   - When you need access to the underlying DOM node (filePicker, media playback, certain animations, working with certain mapping libraries like Leaflet)
7. What is a pure component? why is that useful?
   1. doesn't mutate arguments or anything declared outside of the function
   2. returns same output for same input
   3. React assumes that every component you write is a pure function
   4. React's rendering process must always be pure
   5. Rendering can happen at any time, so components should not depend on each others' rendering sequence
   6. advantages
      1. components can be run in different environments, for example on the server
      2. allows for performance improvements by skipping rendering in some cases, like when a component's inputs haven't changed
      3. If data changes in the middle of rendering a deep component tree, React can restart rendering without wasting time to finish the outdated render. Purity makes it safe to stop calculating at any time
8. What are side effects?
   1. things that don't happen as part of rendering, updating the screen, starting an animation, changing the data, etc...
   2. in React, side effects usually belong inside event handlers (event handlers don't need to be pure) or in a useEffect
9.  What can happen if you nest React component function definitions?
   1. a **new** component is created for each render of the parent component, which, even if the child component is rendered in the same position, that's then still a **different** component in the same position, so React resets all state below, which can lead to bugs and performance problems.
10. What sort of patterns do you employ when developing forms in React?
    1. Normally controlled components, sometimes uncontrolled (with refs) if I need to customize the validity messages and want to use the DOM api for that.
11. Describe conditional rendering in React
    1. Since a component must return something, you can return `null` to tell React to return nothing
    2. conditionally include or exclude the component in the parent components JSX, commonly using one or more of: `? :`, `&&`
12. React considers `false` as a "hole" in the JSX tree, just like `null` or `undefined`, and doesn't render anything in its place
13. Why is mutating state a problem in React?
    1.  The mutation modifies the value **from the previous render**
    2.  Without using the state setter function, React has no idea that the object has changed
    3.  local mutation is fine
    4.  benefits
        1.  easier debugging, `console.log`s will be consistent
        2.  common optimizations rely on reference equality, deep equality isn't required only if state is never mutated
        3.  new React features require it
        4.  easier to implement certain features (undo / redo, history of changes, resetting forms)
        5.  simpler implementation for React (no Proxies, etc...)
14. How does React's state update batching work?
    1.  React waits until all code in the event handlers has run before processing your state updates. This lets you update multiple state variables - even from multiple components - without triggering too many re-renders. This is called batching
        1.  makes your React app run much faster
        2.  avoids dealing with "half-finished" renders where only some state variables have been updated
    2.  **React does not batch across multiple intentional events like clicks** - each click is handled separately
15. How can you update the same state variable multiple times before the next render?
    1.  pass an updater function to the state setter. React queues both values and updater functions passed to the state setter, and processes them during the next render
17. What is derived state? Why can it be problematic? Is it ever OK?
    1.  storing React state in a child from received props. Because prop updates are not reflected in the child component's state
    2.  OK if that's what you want, ie you only want to set the initial state based on props, and want to ignore (or manually handle) all future updates for that state when that prop changes
18. How do you [store information from previous renders](https://beta.reactjs.org/reference/react/useState#storing-information-from-previous-renders)?
    1.  A rare approach is to keep it in state, and then call a `set` function as your component is rendering to update it.
    3.  You use a `set` function in the main function component body, and then after the `return` statement React immediately throws away that component's returned JSX (you could even `return` early as long as it's after all hook calls) and re-renders that component - before rendering its children. This approach eliminates the duplicate render of the children as compared to using an Effect to do this.
        1.  To avoid infinite loops, the `set` call must be inside a condition
        2.  Updating any other state besides the *currently rendering component* is an error, and React will crash.
19. What is `useSyncExternalStore()`?
    1.  TODO
20. What's the difference between:
   1. A React component & A React element
      1. React Elements
         1. plain JavaScript objects. You can think of them as descriptions of what you want to see on the screen. JSX tags `<i_an_an_html_tag>` OR `<I_Am_A_Component>` transpile to function calls that return React elements. (used to always be `React.createElement()`, but might be `jsx` now) when transpiled through Babel. React reads these objects and uses them to keep the DOM up to date. See [React official blog post](https://reactjs.org/blog/2020/09/22/introducing-the-new-jsx-transform.html#whats-a-jsx-transform) for details
         2. React elements are immutable. Once created, you cannot change an element's attributes of children (ie, its props)
      2. React Components
         1. A React components is a JavaScript function that you can sprinkle with markup. It accepts a mostly arbitrary input object (called props) & returns what the UI should look like given that input and any state or context it has access to. If it's a React element, it's ONE (1) React Element.
         2. A big use case for React Components is if they return a React Element, that element can be customized based on the props that component receives. This vastly improves the reusability & modularity of the code.
   2. state and props in React
      1. state
         1. In React, state is data that changes over time
         2. React stores state outside of your component
         3. When you call `useState`, React gives you a snapshot of the state **for that render**
         4. private
         5. fully controlled by the component
         6. expected to change
         7. a state variable's value never changes within a render, even if its event handler's code is asynchronous. The event handler has a closure over that particular render of the component's local state value
      2. the component can choose to pass some of its state to components BELOW it in the tree, as props
      3. props
         1. props reflect a component's data at any point in time. Every render receives a new version of props
         2. immutable (props are read-only)
         3. When you nest content inside a JSX tag, the parent component will receive that content in a prop called `children`
   3. controlled VS uncontrolled components
      1. important component functionality is **mostly** driven by props (controlled) or local state (uncontrolled)
21. Why does React mix markup and rendering logic using JSX?
    1.  As the web became more interactive, logic increasingly determined content, so keeping an element's rendering logic and markup together ensures that they stay in sync with each other on every edit, as well as making changes to that element's logic and markup less likely to break unrelated elements.
22. How do you make a React app faster?
    1.  Memoize expensive calculations during component render with `useMemo()`
    2.  Memoize the component itself (ie, skip rendering that component) with `React.memo()`
23. Explain:
    1. Virtual DOM
       1. TODO: finish
    2. `React.Fragment`
       1. Formally, React Fragments allow you to return a list of children from a component without adding extra nodes to the DOM
       2. ie, you can still return only one thing from a component (as React requires), in cases where if that one thing was a `<div>`, it would cause invalid / excessive HTML
    3. Strict mode in React
       1. TODO: finish
       2. React calls each component twice during development, in order to help find bugs caused by impure components
    4. JSX. Can you have JavaScript inside JSX? If so, how?
       1. TODO: finish
    5. Event propagation in React
       1. All events propagate in React except onScroll, which only works on the JSX tag you attach it to
       2. If you need to capture all events on child elements, even if they stopped propagation, (maybe for routers or analytics) you can do this by adding `Capture` to the event handler name, ie `onClickCapture`. 
          1. Each event propagates in 3 phases
             1. it travels down, calling all `onClickCapture` handlers
             2. it runs the clicked element's `onClick` handler
             3. it travels upwards, calling all `onClick` handlers
    6. refs
       1. A ref is a plain JavaScript object with a `current` property you can read and modify. Refs are retained by React between re-renders. Changing a ref does not trigger a re-render.
       2. Typically, refs are used to communicate with external APIs (like browser APIs) or external objects for when you want to "remember" some information, but you don't want changes to that information to trigger a render
       3. In general, you don't want to read / write to a ref during rendering, as this can make your component's behavior difficult to predict. Use state instead.
       4. Refs and the DOM
          1. A big use case for refs is [certain types of direct DOM manipulation](https://beta.reactjs.org/learn/manipulating-the-dom-with-refs)
          2. use cases
             1. managing focus, text selection, media playback, scrolling, measuring DOM element size and position
             2. triggering imperative animation
             3. integrating with existing or already deployed third party DOM libraries
          3. You can pass a ref to a built in React component (like `<input />`) using the `ref` attribute
          4. If you try to modify the DOM manually using refs, you risk conflicting with the changes React is making. So avoid changing DOM nodes managed by React. However, you can safely modify parts of the DOM that React has no reason to update
    7. callback refs
       1. [callback refs are a a way to get more control over the ref](https://beta.reactjs.org/reference/react-dom/components/common#ref-callback)
       2. You set the ref attribute equal to a callback function. React calls the ref callback with the DOM node when it's time to set the ref, and with null when it's time to clear it.
       3. For example, if you need refs to an arbitrary number of DOM nodes, you can use callback refs to mutate a map (itself stored in a ref) of some IDs to DOM nodes.
    8. forwardingRefs
       1. forwarding refs are a way for [parent (or ancestor) components to have access to some inner portion of a child component.](https://beta.reactjs.org/learn/manipulating-the-dom-with-refs#accessing-another-components-dom-nodes). This pattern should be avoided if possible, as it breaks component encapsulation.
       2. By default (and intentionally) React does not let a component access the DOM nodes of other components
       3. A component can specify that it "forwards" its refs to one of its children, by using `forwardRef`
     9.  `useImperativeHandle()`
         1.  React hook, normally used to [restrict the functionality of a parent component that is accessing some descendant component's DOM node through a forward ref](https://beta.reactjs.org/learn/manipulating-the-dom-with-refs#exposing-a-subset-of-the-api-with-an-imperative-handle). `useImperativeHandle()`, called in the descendant component, instructs React to provide your own special object as the value of a ref to the ancestor component.
     10. When does React attach Refs?
         1.  [React sets ref.current during the commit phase](https://beta.reactjs.org/learn/manipulating-the-dom-with-refs#when-react-attaches-the-refs)
             1.  object refs
                 1.  Before updating the DOM, React sets the affected `ref.current` values to `null`
                 2.  After updating the DOM, React immediately sets them to the corresponding DOM nodes
             2.  [callback refs](https://beta.reactjs.org/reference/react-dom/components/common#ref-callback)
                 1.  When the DOM node is added to the screen, React will call your `ref` callback with the DOM node as the argument
                 2.  When the DOM node is removed, React will call your `ref` callback with `null`
                 3.  React will also call your `ref` callback whenever you pass a different `ref` callback. This is why, when the component re-renders, the previous function will be called with `null` as the argument, and the next function will be called with the DOM node.
     11. What is `flushSync()` used for?
         1.  [`flushSync()` forces React to update the DOM synchronously right after the code wrapped in `flushSync` executes](https://beta.reactjs.org/learn/manipulating-the-dom-with-refs#flushing-state-updates-synchronously-with-flush-sync)
         2.  Sometimes can be useful if you need to interact with DOM nodes through a ref, but the nodes are impacted by a state update that hasn't been flushed yet
    9.  Context in React
       1. Context in React lets the parent component make some information available to any component in the tree below it, no matter how deep, without explicitly passing it through props. The child asks the closest provider of a given context above it in the tree for the data.
       2. Easy to overuse. Consider passing props or component composition (ie, defining the component that needs the data in the component where the data lives as state, then passing that whole component as a prop)
       3. Common use cases for Context include theming, location, data cache, current account, routing
    10. the `key` prop. Why is it needed? what happens if you don't use it?
       1.  TODO: finish
       2.  keys must be unique among siblings
       3.  keys must not change, or it defeats the point of using them
24. What are React Hooks?
    1. [An approach to accessing many useful React features that formerly required classes](https://reactjs.org/docs/hooks-intro.html) (state, lifecycle methods, etc...)
    2. hooks are special functions that are only available while React is rendering, and they let you "hook into" different React features that used to require classes
25. What are the main problems that React Hooks aim to solve?
    1. Classes in JavaScript are potentially difficult for developers to work with & [allow coding certain patterns that prevent many performance optimizations](https://reactjs.org/docs/hooks-intro.html#classes-confuse-both-people-and-machines).
    2. Using lifecycle methods enforces splitting related logic based on when-that-logic-needs-to-run. [Hooks allow for other groupings of related logic](https://reactjs.org/docs/hooks-intro.html#complex-components-become-hard-to-understand).
    3. Hooks allow you to [share stateful logic between components](https://reactjs.org/docs/hooks-intro.html#its-hard-to-reuse-stateful-logic-between-components) (sharing the LOGIC, not the state. The state remains unique.)
26. What are the rules of using React Hooks?
    1.  only be called at the top level of your components or your own custom hooks
    2.  don't call hooks inside conditions, loops, or other nested functions
27. Do React Hooks have any naming conventions? why? / why not?
    1.  start with lowercase `use`. It's helpful for other developers to identify this as a hook
28. Why is state needed in React?
    1.  local variables don't persist between renders. React literally runs the function again. So changes to local variables won't trigger renders
29. What's needed in order to update a component with new data in React?
    1.  Retain the data between renders (the state variable returned from `useState`)
    2.  Trigger React to render the component with new data (re-rendering) (the state setter function returned from `useState`)
30. How would you create & update state?
    1. invoke the `useState()` method with the initial state you want to store
    2. Every time your component renders, `useState` will return an array containing:
       1. 1st element - the current value of that state
       2. 2nd element - function to update that state value and trigger React to re-render the component
       3. the convention is to use [array destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) to create the local variables that point to the actual state value & associated updater returned from `useState`. Naming these variables is up to the developer.
    3. You update that state by invoking the updater function with the new value
31. In a React component with multiple `useState` calls, how does React know which state to return?
    1.  Hooks rely on a stable call order on every render of the same component.
    2.  Internally, React holds an array of state pairs for every component. It also maintains the current pair index, which is set to 0 before rendering. Each time you call useState, React gives you the next state pair and increments the index. More details [here](https://beta.reactjs.org/learn/state-a-components-memory#how-does-react-know-which-state-to-return) and [here](https://medium.com/@ryardley/react-hooks-not-magic-just-arrays-cd4f1857236e).
32. How is React component state isolated?
    1.  State is local to a component instance on the screen. If you render the same component twice, each copy will have completely isolated state
    2.  State is not tied to a particular function call or a place in the code, but it's "local" to the specific place on the screen
    3.  State is fully private to the component declaring it
33. Describe at least two (2) approaches for storing multiple state values with `useState()`
    1. Store all the values in a wrapper object, and have that wrapper object be what gets passed to `useState`
    2. React supports multiple calls to `useState` in the same component, each referring to a different slice of state
34. How do you synchronize with external systems using React? How would you perform side effects in a React component?
    1. examples
       1. control a non-React component based on the React state
       2. set up a server connection, data fetching
       3. send an analytics log when a component appears on the screen
       4. setting up a subscription
       5. manipulating the DOM with the browser API
    2. Components can have rendering code (pure), and event handlers (side effects)
    3. Effects let you specify side effects that are caused by rendering itself, rather than by a particular event, so you run some code after rendering to synchronize your component with some system outside of React
    4. invoke the `useEffect()` hook
    5. [you pass `useEffect()` a function](https://beta.reactjs.org/learn/synchronizing-with-effects#how-to-write-an-effect) - by convention called an Effect - and by default **React guarantees that it will invoke this effect after every render, including the first one**.
    6. The Effect you pass utilizes closure to retain access to the function component's scope (ie, props / state / etc...)
    7.  How do you prevent Effects from running after every re-render?
        1. `useEffect` optionally takes a second argument, an array, that React will compare using reference equality with their current value(s), and [only run the Effect if those values differ](https://beta.reactjs.org/learn/synchronizing-with-effects#recap).
     8. Describe an approach for when your Effect requires cleanup?
       1. You can return a cleanup function from your Effect that is run each time before the Effect runs again, and one final time when the component unmounts (gets removed)
          1. Remember that Effects are unique to a particular render, so the cleanup function run is the one from the last render in which that particular Effect ran, even if there were re-renders in between in which that particular Effect didn't run
       2. In development React remounts every component once immediately after mount (state and DOM are preserved). This is intentional and helps to surface bugs around Effect cleanup. React also remounts Effects whenever you save a file in development.
    8. What's the typical first approach for data fetching with React?
       1.  `fetch` call inside an Effect
       2.  Problems with that approach?
           1.  Effects don't run on the server, so all data fetching happens client side - initial server rendered HTML will contain defaults. Can be somewhat inefficient, depending on how often the data changes.
           2.  Fetching directly in Effects makes it more likely to create "network waterfalls" (the start of each network request is delayed until *after* the relevant component renders, as opposed to sending all the network requests at once at the beginning). Undesirable when all of the data is required immediately
           3.  Fetching directly in Effects usually means you don't preload or cache data
           4.  usually `fetch` manually requires considerable boilerplate code (especially handling race conditions)
       3.  Solutions?
           1.  use frameworks (Next.js, Gatsby, Remix, Razzle, etc...) with built-in data fetching
           2.  Use a client-side cache (React Query, useSWR, React Router 6.4+) - deduplicating requests, caching responses, avoiding network waterfalls (by preloading data or hoisting data requirements to routes)
35. Describe React's render and commit phases
    1. Triggering a render
       1. It's the component's initial render
       2. the component's (or one of its ancestors') state has been updated. Updating your component's state automatically queues a render
       3. CHRISTIAN
          1. context it uses has been updated
          2. the component's props have changed
    2. Rendering the component
       1. after you trigger a render, React calls your components to figure out what to display on screen.
       2. "Rendering" is React calling your components
          1. on initial render, React will call the root component
          2. for subsequent renders, React will call the function component whose state update triggered the render, ie to figure out what has changed
          3. this process is recursive, ie if the updated component returns another component, that component will be called, and so on
    3. Committing to the DOM
       1. For the initial render, React will use the appendChild() DOM API
       2. for re-renders, React applies the minimal necessary operations (which are calculated while rendering) to make the DOM match the latest rendering output
       3. **React only changes the DOM nodes if there's a difference between renders.**
    4. Browser paint
       1. After rendering is done and React has updated the DOM, the browser will repaint the screen
       2. technically called "browser rendering", React devs call it painting for clarity
36. List some examples of side effects in React that don't require cleanup?
    1. manually manipulating the DOM
    2. network requests
    3. logging
37. How is `useEffect()` different from class component lifecycle methods?
    1. TODO: finish
    2. TODO: finish effects don't block the browser from updating
38. Are effects reused? why? why not?
    1. TODO: finish
39. Does using multiple `useState()` / `this.setState()` calls in the same event handler (or lifecycle method) increase the number of re-renders? Why(not)?
    1. Trick question. It does if your `useState()` / `this.setState()` calls are [wrapped in async code](https://stackoverflow.com/questions/33613728/what-happens-when-using-this-setstate-multiple-times-in-react-component#:~:text=2%20Answers&text=React%20batches%20state%20updates%20that,to%20finish%20before%20re%2Drendering.&text=State%20updates%20are%20not%20batched,setTimeout%20event%20handlers%2C%20for%20example.) (ie, `setTimeout` / `setInterval` / AJAX calls / etc). Otherwise, no, React's [batching behavior for state updates](https://reactjs.org/docs/state-and-lifecycle.html#state-updates-may-be-asynchronous) may combine those updates into a single render.
40. Class based React 
    1. How do you decide between using a functional VS a class component?
       1. Two big reasons to use Class Components are
          1. you need state
       2. you need to use lifecycle methods, like componentDidMount() or componentDidUpdate()
   1. state updates
         1. done through `setState()` - NOT directly
         2. merged into existing state
         3. may be asynchronous
    2. 23. How is `useState()` different from `this.setState()`?
       1. TODO: finish
    3. Values returned from `useState` - the state & its associated updater function are LOCAL to the component, so they can be passed to event handlers, for instance, without any fuss (ie, no `bind()` calls necessary)
    4.  Can you use React Hooks inside classes? why? / why not?
        1. TODO: finish
     5. Context in class components:
          1. You assign `MyClass.contextType` to the context object you created earlier
          2. This makes the value defined in the nearest ancestor Context Provider available in this class at `this.context`
    5. Refs can give you access to the instance of a class based component
       1. refs updates happen before `componentDidMount` / `componentDidUpdate`
       2. `React.createRef()` or callback refs are preferred, instead of string refs & `ReactDOM.findDOMNode()`
       3. refs can only be used on HTML elements & class components. You CANNOT use a ref on function component. (but you can use them inside function components)
       4. A callback ref receives either the DOM node or the component instance before `componentDidMount` / `componentDidUpdate` invokes, and `null` when the component unmounts
    6. Describe an approach for when your effect requires cleanup? What advantages does this approach have over classes?
       1. Optionally, you can return a function from your effect. React will invoke this function before the component unmounts (ie, when `componentWillUnmount` would run). React also invokes this function before each re-render, which [helps prevent common bugs.](https://reactjs.org/docs/hooks-effect.html#explanation-why-effects-run-on-each-update)
       2. This approach allows you to keep related code together (encapsulation), rather than forcing a split based on the React lifecycle