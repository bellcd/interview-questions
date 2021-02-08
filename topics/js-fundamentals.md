# JavaScript Fundamentals

1. Describe general pros & cons to using JavaScript
   1. TODO: finish
2. How was the `this` problem handled before ES6?
   1. TODO: finish
3. How can you add more methods to an already existing class?
   1. TODO: finish
5. Explain:
   1. scope
      1. The area of a running program where a lookup for a given variable can happen. Scopes can be nested inside each other, and inner scopes have access to variables defined in outer scopes (but not vice-versa) [docs](https://developer.mozilla.org/en-US/docs/Glossary/Scope)
   2. var VS const VS let
      1. three (3) ways of declaring variables in JavaScript
      2. var - uses function scope
      3. const & let
         1. Both use block scope
         2. const variables cannot be reassigned, let variables can
   3. the keyword `new`
      1. JavaScript is not an object oriented language (OOP), nor is it a functional programming language - JavaScript is a multi-paradigm language. JavaScript does has a `new` keyword that creates results that look like what the `new` keyword does in many OOP languages; however, the details of what actually happens are different.
         1. *JavaScript does NOT have "constructor" functions*. When `new` is used in front of a function invocation, the interpreter does several special things. (So you could say JavaScript has "construction invocations" of a function)
            1. Creates a new object in memory
            2. Assigns the `this` context of the construction invocation of that function to the new object
            3. If no explicit return is declared in the function, returns that newly created object
   4. prototype delegation
      1. Because JavaScript is multi-paradigm, it does not do classing in the same way that OOP languages handle classing (even with the ES6 `class` keyword!)
      2. Instead, JavaScript does something called prototype delegation.
         1. When you tell the interpreter to search for a property (or method, if it's a function) on an object (in JavaScript, arrays and functions are types of objects), the interpreter first looks directly on that object.
            1. If the lookup succeeds, it continues with your code
            2. Else, the interpreter delegates the lookup to the next higher object in the prototype chain
            3. This process repeats until
               1. the lookup is successful
               2. we get to the highest prototype object, which itself delegates lookups to the value `null`, at which point the interpreter returns `undefined`.
         2. Every object in JavaScript has a Prototype Chain to which it delegates failed property lookups.
            1. In many browsers (ie, Chrome) the prototype object of a given object is available in the console at the property `__proto__`
            2. Because Arrays and Functions are types of Objects, the object at the `__proto__` property of an Array, for example, will itself have an object at its `__proto__` property.
   5. hoisting. variable VS function hoisting differences?
      1. TODO: finish
   6. Creation VS Execution phase
      1. TODO: finish
   7. closure
      1. closure is a way for functions to access variables that would otherwise be outside their scope.
      ```js
      function myFuncY() {
         var a = 0;
         function myFuncX() {
            a += 1;
            return a;
         }
         return myFuncX;
      }

      var x1 = myFuncY();
      var result1 = x1();
      var result2 = x1();

      var x2 = myFuncY();
      var result3 = x2();
      var result4 = x2();
      ```
      1. For example, one way we could talk about the code above it to say that `x1` has a closure over `myFuncY`. We would also say that `x2` has a closure over `myFuncY` However, I find this verbiage incomplete, at best. If both `x1` & `x2` have a closure over `myFuncY`, what do you expect `result4` to be? 1? 4? It certainly looks like we're `myFuncX` a total of 4 times...
      2. *`result4` equals 2*
      3. Each time we invoke `myFuncY`, an execution context is created, with a local scope. When we declare `var a = 0`, we're declaring that *in local scope*, local to THIS INVOCATION of `myFuncY`. We then return a function, `myFuncX`, which has access to `a`, because `a` was declared in a parent scope to the scope of `myFuncX`. But because we're *returning* `myFuncX`, it needs some way to access variables it should have access to (ie, through normal lexical scope lookup) in whatever scope it ends up invoking in. Closure is what allows this to happen.
      4. So the function referenced by `x1` has access (through closure) to the variable `a` that was in scope at the time that `myFuncX` function declaration was made. `x1` invokes, and the function increments that variable `a` first to 1, then to 2.
         1. The variable `a` exists in an area that the interpreter creates - sometimes called a backpack. `x1` has access to this backpack.
      5. When we invoke `myFuncY` again, a different - *different* - execution context is created. We also create a variable `a`, *different from before*, and set this new variable `a` to 0. Likewise, we declare a totally new function, that happens to have the same name & be identical to `myFuncX` from before. We return this function, and set it equal to `x2`.
      6. So when we invoke `x2`, what is the value of `a` that that function increments? 0. *0*, not 2. The variable `a` that `x1` has access to and the variable `a` that `x2` have access to are *different variables* (that happen to have the same name), that live in *different backpacks*
      7. So `result4` equals 2, not 4.
   8. event delegation. Describe the performance tradeoffs.
      1. TODO: finish
   9.  object literal
      2. TODO: finish
   10. object & array destructuring
       1. TODO: finish
   11. Callbacks VS Promises VS async / await
       1.  TODO: finish
   12. Asynchronous programming, and why it is important in JavaScript?
       1.  JavaScript is a single threaded language. That means that your JavaScript code will execute sequentially / synchronously / as it's written, one line after the other. Except that the thing that provides the runtime environment to your JavaScript code (browser, Node.js, etc...), is written in languages that are NOT single threaded. Asynchronous programming in JavaScript refers to the fact that the environment in which your JavaScript code executes can provide APIs that allow the execution of portions of your JavaScript code to happen at later times (ie, `setTimeout` / `fetch` / Promises / `async / await`, etc... ). This allows JavaScript code to handle all sorts of situations where your JavaScript code is not in control of how long it needs to wait for something - network requests are a prime example of this. You provide code that triggers the network request, and does something with the response. But your code doesn't control how long that response takes to come back.
   13. How would you use promises right after each other?
       1.  TODO: finish
   14. How do you handle needing to wait for multiple promises to finish?
       1.  TODO: finish
   15. Immutability in JavaScript
       1. Are objects & arrays in JavaScript immutable?
       2. How do you make something immutable in JavaScript?
          1. TODO: finish
   16. Syntactic Sugar, and give at least 1 example
       1. When the language provides a different (also simpler / cleaner / easier to understand / shorter / "better" / etc...) syntax for **accomplishing the exact same task**
          1. `async` & `await`, so you don't have to work with `.then` blocks
          2. the `class` keyword in JavaScript
          3. the spread & rest operators
          4. object & array destructuring
   17. Worker (and when / why you would use one)
6. What's the difference between
    1. WET & DRY code?
       1. DRY - Don't Repeat Yourself - is the general idea of encouraging efficiency in the way you structure your code
       2. WET is the opposite - inefficient code
    2. a variable & a function
       1. TODO: finish
    3. an id and a class in CSS?
       1. TODO: finish
    4. double `==` & triple `===` equality
        1. double compares with type coercion on, triple with type coercion off
    5. arrow function & 'normal' function
       1. normal function
          1. declared with the `function` keyword
          2. creates a new `this` context
       2. arrow function
          1. declared with arrow function syntax `() => {}`
          2. uses the `this` context of its containing scope
    6. the functions `call`, `apply`, & `bind`. What are they used for?
        1. `call` accepts a list of arguments, whereas `apply` accepts one (1) array with potentially many arguments
        2. `call` & `apply` are used to invoke another function, optionally with:
           1. a different `this` context
           2. additional arguments
        3. `bind` is used to bind a function's `this` context to a particular `this` context. It returns a new function that will always invoke with the given `this` context, along with any additional arguments passed. A function like this is needed because of how `this` works in JavaScript (ie, the value of `this` is not known until runtime, instead of at author-time, like in other languages)
    7. `JSON.stringify()` & `toString()`
        1. `toString()`
            1. method on `Object.prototype`
            2. can return different (sometimes surprising!) results for different values (ie, for an obj returns `[object Object]`)
        2. `JSON.stringify()`
            1. method on `JSON`
            2. intended to serialize values into the JSON format for transmission or storage, so the results tend to be more predictable than `toString()`
               1. but doesn't serialize functions or undefined
    8. dot & bracket notation in JavaScript objects?
       1. both syntaxes instruct the interpreter to look for a property on that object with a particular sequence of characters
          1. dot notation looks for literally every character after the dot
          2. bracket notation causes what's inside the bracket to get evaluated, & **that evaluated expression is what's searched for**
    9. spread & rest operators
       1. TODO: finish
       2. can you use the spread operator to concatenate an array with another array?
    10. the JavaScript callstack & the JavaScript memory heap?
       3. TODO: finish
    11. Using the `delete` keyword & `splice` method to remove an element from an array?
        1. The `delete` keyword removes a property from an object, so in the case of an array, it will remove the *numeric* property. The length of the array remains unchanged.
           ```js
           let array = [0, 1, 2, 3, 4, 5];
           delete array[2];
           console.log(array) // Chrome would display this array as [0, 1, empty, 3, 4, 5]
           console.log(array.length) // 5
           console.log(array[2]) // undefined, because it's trying to access a property of an object (in JavaScript, arrays are objects!) that doesn't exist
           ```
        2. Using `splice` to remove that element removes the property, but it [also reindexes the array, so the array length will change](https://stackoverflow.com/questions/500606/deleting-array-elements-in-javascript-delete-vs-splice). (ie, the example above would be `[0, 1, 3, 4, 5]`, so the elements 3, 4, & 5 are at *different indices* than they were when using `delete`).
7. How does the internet work?
   1. TODO: finish
8. Describe the request / response cycle
   1. TODO: finish
9.  What's the difference between the head & body of a request / response?
   2.  TODO: finish
10. How do template strings work in ES6?
   3. TODO: finish
11. What are the 5 instantiation patterns in JavaScript? Describe pros / cons of each, and why / where you would use them.
   4.  TODO: finish
12. Explain the different ways to get asynchronously executing code in JavaScript
    1.  TODO: finish, ie - task queue VS microtask queue VS setAnimationFrame
13. Are there any downsides to using the microtask queue as your default for async work?
    1.  TODO: finish, ie - microtask queue is blocking to certain browser actions?