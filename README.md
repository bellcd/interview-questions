# interview-questions

A collection of interview questions I've been asked, to help you better prepare for software development interviews.

### Real Interview Questions

1. What interests you about this job in particular?
   - ...
2. How much experience in _____ do you have?
   - My-Awesome-Bootcamp / Training covers in ____months what junior & even some mid level developers cover in ____months / years
3. Have you ever worked as a web developer before? / Have you ever been paid to write software?
   - If they’re looking for someone with “developer” in several previous job titles, that’s not me
   - If they’re most concerned with simply getting the job done, that’s me
4. What are the most important qualities in a developer? / What makes a good developer?
   - base level of knowledge (HTML, CSS, JavaScript, DOM, how the internet works, front end frameworks / view libraries)
   - clear technical communication
   - open-mindedness
   - teamwork
   - persistence
   - how you react to being confused
   - managing the scribe VS conjurer tension
5. What are the 3 most important things to you in a job?
   - The ability to work in in demand, marketable technologies
   - mentorship from lead developers and management
   - quantitative impact on projects with move-the-needle type business outcomes
   - A team & management that set realistic goals
   - competitive compensation package
6. Tell me about yourself? / Who are you as a software engineer / Why do you do this? What do you like about development?
   - personal narrative ...
7. What do you dislike about development?
   - Being roadblocked w/deadlines. Teamwork aspect of web development is very important here.
8. What do you think is the largest problem with the UI/UX that if solved, would increase our conversion rate from visitor to paying user?
   - ...

#### React
1. Could you describe the React component lifecycle? When in the lifecycle would you bind to events?
   - ...
2. When do you prefer to use the Ref attribute?
   - When you need access to the underlying DOM node (filePicker, media playback, certain animations, working with certain mapping libraries like Leaflet)
3. How do you decide between using a functional VS a class component?
   - Two big reasons to use Class Components are
     - you need state
     - you need to use lifecycle methods, like componentDidMount() or componentDidUpdate()
4. What's the difference between a pure component and a regular component?
   - TODO: complete
5. What sort of patterns do you employ when developing forms in React?
   - Normally controlled components, sometimes uncontrolled (with refs) if I need to customize the validity messages and want to use the DOM api for that.
6. What happens when I enter my username & password into a form & hit login? Describe at as low a level as you can.
   - Assuming we're sending the data as JSON & following best practices. The front end encodes the username & password into a JSON object, then sends them in the body of a POST request to the relevant api endpoint of the server.

#### Security

1. What happens when the username & password reach the server? How does the server verify if the password is correct?
   - The server has to be on & listening at the correct api endpoint & port, and have code set up to handle the type of incoming request - POST, in our case. The server code then reads the body of the POST request, parses the JSON, and continues processing the request with other server code.
   - For your password to be sercurely stored in the company's database (to a reasonable degree) the actual thing - the text - that the company stores in their database is NOT your password, as you remember it.
     - For example, when you enter your email awesomeMegan@gmail.com & password @myFluffyDog42 into the login form and submit them, those bits of text eventually arrive on the web server. There, the server code will ask the database for the stored password it has for awesomeMegan@gmail.com. Assuming you've registered before, the database will send the stored password it has back to the server code. Now the server code can compare the password you typed in - @myFluffyDog42 - with what it received from the database, something like 0E6A48F765D0FFFFF6247FA80D748E615F91DD0C7431E4D9. They're different because what's stored in the database is something called a hashed password. Hashing is a ONE-WAY operation, in that it takes your input string - @myFluffyDog42 - runs it through a function (called a hashing function), and outputs something - in this case the string 0E6A48F765D0FFFFF6247FA80D748E615F91DD0C7431E4D9. This works for passwords / security because hashing functions:
       - Always return the same output for the same input
       - It's not possible to go backwards (ie, take a hash and create the plain text password), even if you know the details of the particular hashing function used.
       - Every input maps to one output (not technically true at the margins, but for all practicality)
     - Some company systems also use a salt, which is a random string (some common ones are combinations of date, IP address, type of web browser, etc...), and combine that with your user supplied password, to create the hashed password. This approach is more secure because then you need something the end user has (password) + something the company has (salt) to generate the correct hashed password.
   - So the server code runs your password - @myFluffyDog42 - (combined with your salt from the database, if they user them) through their hashing function, and compares the hashed password that was just generated with the hashed password retrieved from the database. If they match, the user is then authenticated.
2. How can a user stay logged in, so they don't need to & password?
   - The web app / website can set a cookie on the end user's web browser. Cookies are:
     - small pieces of data
     - in key:value format
     - domain specific
     - sent with every request
   - So, for example, when you sucessfully login to a website / web app, they could generate & save a unique string on your browser as a cookie. Then, later, when that same browser visits the webpage, the cookie gets sent to the web server, (which has code set up to recognize the unique string that it set earlier). This uniquely identifies you to the server, and so it may not ask you to log in again.
3. Can the company retrieve your password for you?
   - Not if they're following security best practices
   - Because hashing is a ONE-WAY transformation, and the company only stores your hashed password, it is NOT possible for the company to send you your password. The best they can do is validate that it is in fact you, then offer to rest your password.
4. What is SQL injection? How do you prevent it?
   - When a web page or web app executes user input directly in an SQL query
   - Don't directly execute uer input. ie, every piece of user input needs to pass input validation before that user input even gets to the part of your system that interacts with the database.
5. Architect a scaled down Facebook app, with a feed display, and a posts display, many users, many posts. FOLLOWUP: How do you make it so anyone can get to it?
   - ...
6. When you have lots of traffic and the website is slow, how do you determine where the bottleneck is, and how would you fix it? FOLLOWUP: If the bottleneck if the server, how would you fix it?
   - ...
7. How do you securely transmit data?
   - ...
8. How do you get your React / Angular / Vue / etc... app onto the server?
   - ...
9. Tell me about a time you missed a deadline, what happened, and how did you fix it?
   - ...
10. Tell me about a time you've worked harder than you should've, and why you did it?
    -  ...
11. What browser do you use to develop and why?
   - Chrome, dev tools features

#### Page Load Speed

1. What are things you can do to improve page load speed?
   - Run Google's Lightouse, it provides a laundry list of suggestions
   - Reduce size
     - [Images sized appropriately to display sizes](https://web.dev/uses-responsive-images/) (ie, no 2000 x 2000px images if you're displaying a thumbnail)
       - Responsive images (multiple sizes of raster images, serving the appropriate ones with media queries)
       - Using SVGs in some cases
     - [Lazy loading images](https://web.dev/use-lazysizes-to-lazyload-images/)
     - [Videos](https://web.dev/efficient-animated-content/)
       - Prefer MPEG4 over GIFs (especially lager GIFs) when possible
     - [Use modern image formats](https://web.dev/uses-webp-images/) (ie, JPEG 2000 / WebP for better compression algorithms)
     - [Avoid enormous network payloads](https://web.dev/total-byte-weight/)
       - Minify HTML / CSS / JavaScript
     - [Enable text compression](https://web.dev/uses-text-compression/
     - [Lower your time-to-interactive](https://web.dev/offscreen-images)
       - Defer offscreen images
     - Reduce the number of requests
       - Consider server side rendering
     - [Render Blocking](https://web.dev/render-blocking-resources/)
       - Eliminate render blocking resources
     - [Don't chain critical requests](https://web.dev/critical-request-chains/)
     - [Caching](https://web.dev/uses-long-cache-ttl/)
       - Use CDNs
       - Have an efficient cache policy

#### Workflow

1. What's the difference between a text editor & an IDE?
  - A text editor is for more general purpose text editing (ie, Microsoft Word is a text editor), whereas an Integrated Development Environment has many more features specifically targeted at developers to make their workflows more efficient (ie, syntax highlighting, code completion, integrated terminals, etc...)

#### Fundamentals

1. What's the difference between
    1.  TODO: finish
    2.  a variable & a function
    3.  an id and a class in CSS?
2. How does the internet work?
    - TODO: finish

#### CSS

1. What's the difference between
    1. inline and inline-block?
       - inline-block can assign a height property TODO: link to stackoverflow answer
2. What CSS would you use to turn a span into a button?
    - TODO: finish
3. Describe the cascading part of CSS
    - TODO: finish
4. What HTML & CSS would you use to make a horizontal nav bar?
    - TODO: finish
5. What is a float?
    - A floated element moves to the left or right of its container, allowing text & inline elements to flow around it

#### Project Management

1. Agile VS Waterfall
    - Waterfall
      - Linear, sequential process flow
      - Scope is know, determined right at the beginning
      - Cost / timeline / deliverables flow from scope
      - Changes to scope go through formal change control, almost certainly cause changes to cost / timeline / deliverables ... too many changes can cause it-would-be-better-to-do-a-new-project
      - well suited for tangible, long term things (ie, **when the scope isn't likely to change**)
    - Agile
      - Originally envisioned as a solution to the downsides of waterfall in software development
        - ie, there were better solutions from competitors coming out 0.5 / 1yr into SDLCs ...
      - Change is expected & embraced - don't pre plan too far out into the future
      - Simple project design that becomes more clear throughout the project
      - Uses short iterations (Sprints ~30 days or less) to produce deliverables with feedback (from customer / stakeholder) after each Sprint
      - Incremental process, with customer feedback at each step, instead of all-at-the-end (like in Waterfall)
      - **well suited for knowledge work**
      - Can be challenging for inexperience people to know if they're building the "right-thing-right"
        - ie, when you have to make Waterfall type decisions in an agile process, ex how to handle state, which front end framework, which database, etc ... Each have their own tradeoffs that depend heavily on what the client requirements are (scope) ... if scope changes, what's "best" would change ...

|   |Waterfall|Agile  |
|---|---------|-------|
|Scope (picture of final product)|Clear at the beginning|NOT clear at the beginning|
|Quality VS Speed|Quality|Speed|
|Changes|Formal process for changes|Changes expected|

2. How would you handle someone who approaches you with a project management triangle? (price, speed, cost)
    - TODO: finish
3. You're leading a team that's behind on a deliverable. How do you motivate them to get it done?
    - TODO: finish

#### Functional Programming

1. What is functional programming and what are its benefits?
   1. Style of programming - programming paradigm - where the focus is on each function & its inputs / outputs
      1. Clojure, Haskell, & Lisp are set up in this way. JavaScript is multi-paradigm

|Pros|Cons|
|----|----|
|Easier to reason about & test (because the functions are more self contained|Can be more complicated to write|
|Easier to debug|Can feel like you're jumping through a lot of hoops to maintain the functional paradigm|
|More concise||
|More scalable||
|More predictable (because the functions don't rely on external state)||

1. What are the common parts of functional programming?
   1. first class functions
      1. functions are treated the same as any other variable
   2. higher order functions
      1. functions that accept or return a function, or both (setTimeout, map, filter, reduce, etc...)
   3. Pure functions
      1. a pure function is one that when called with the same input returns the same output

|Pros|Cons|
|---|---|
|Easier to test|Not every task can be accomplished with pure functions|
|Easier to debug||
|More scalable||
|No surprises (ie, mutating the arguments / global state||
|self documenting||
|concurrency||
|cacheable||

  4. function composition
     - the concept of building more complex functions from smaller, more narrowly focused functions
     - piping (ie, sending the output of one function as the input of another function)
  5. currying
     - changing a function so that it returns a new function that solves a more specific version of that problem. Reduces the amount of arguments in the returned function's signature, because at least one of the used-to-be-a-parameter is now an internal variable to that returned function

```js
// not currying
function add(a, b) { return a + b; }

// currying
function makeAdder(x) {
  return function(y) {
    return x + y;
  }
}

add(5, 6); // 11

const add5 = makeAdder(5) // returns a FUNCTION that accepts one argument, and adds 5 to it
add5(6) // 11
```

   6. Immutability
      - Where a data structure is not changeable after creation. String are immutable in JavaScript. Objects & arrays are not.

|Pros|Cons|
|----|----|
|Predictability|Performance hit, because you're copying objects all the time (especially with many tens / hundreds of thousands of objects)|
|Faster change detection for UI frameworks like React. (It's less work to tell if some property has changed, because a whole new object will be created whenever a property changes, and so the framework can do a computationally cheap referential identity check to see it it needs to update the UI (instead of a computationally expensive recursive check)|Memory overhead (because of all the object copies|
|Concurrency - more scalable code, because you can run multiple functions in parallel (because they're not relying on external state to be a certain way, they're always creating NEW state||

There are libraries such as Immutable.js & Immer to make handling this easier in JavaScript
