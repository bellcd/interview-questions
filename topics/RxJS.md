# RxJS
// TODO: add links

1. What is RxJS?
   1. The JavaScript version of the ReactiveX programming library
2. What problem does it solve?
   1. TODO: finish
3. What are the tradeoffs in using it?
   1. Pros
      1. Excels at handling the complexity of modern apps (ie, modern UIs with many interlocking events and state changes)
      2. Does so in a way that is:
         2. Readable
            1. declarative (instead of imperative) using pure functions, so less prone to bugs
         3. Extensible
            1. RxJS includes many, many operators specifically designed to allow enormous flexibility
   2. Cons
      1. Initial learning curve can be quite steep, official documentation can be confusing for those not familiar with the terminology.
      2. Requires learning a different way of thinking about programming.
5. What is an Observable?
   1. An observable represents a sequence of items arriving over time. The items could be basically anything (mouse / keyboard interactions, network request responses, data in memory, etc...)
6. What is an Observer?
   1. An observer is something that listens - observes - to an observable, invoking callbacks that you specify when certain conditions are met:
      1. item was emitted (next)
      2. error occurred (error)
      3. observable completed (complete)
7. Is RxJS a push or pull based approach?
   1. push - RxJS allows you to register callbacks that will run when your observable has data that is ready to be pushed. The observable - the data producer - is in control of when the data starts to flow through your stream, as oppossed to the observer.
8. Why is the term stream sometimes used?
   1. A common analogy for RxJS is a stream (river) with things flowing down it
9. Are observables synchronous or asynchronous?
   1.  Trick question. Observables can handle data that arrives synchronously or asynchronously, and there are many operators to make controlling this easier.
10. What's the difference between unicast & multicast in the context of RxJS?
    1.  unicasting
        1.  meaning each subscriber creates an individual execution path between the observable & the observer 
        2.  each subscription to the observable creates a new execution path, a separate producer, ie - the relationship between observers / subscribers & execution paths will always be 1:1
        3.  this is the default behavior in RxJS
        4.  completing one observable (one execution path) has no impact on any other
    2.  multicasting
        1.  subject
            1.  Subjects in RxJS are a mix between an observable & an observer, so they have  `pipe` & `subscribe` methods like observables, but also `next`, `error`, & `complete` methods like observers.
            4.  Subscribers of subjects are registered to, and share an execution to, an observable. Subjects are used to deliver a single notification to multiple subscribers.
11. What are some common use cases for multicasting in RxJS?
    1.  Sharing messages or state with multiple layers in your application (ie, broadcasting the same thing to any observer who cares to listen, similar to how EventEmitters work)
    2.  You don't want or need to create a new resource on every new subscription
    3.  You want to share part of an execution path between multiple observers
    4.  If there's an expensive operation / network request that we don't want to repeat on new subscribers
12. What's the purpose of the `asObservable` method?
    1.  TODO: finish
13. What is a ConnectableObservable? What's its purpose?
    1.  TODO: finish
14. What's the difference between `multicast()`, `refcount()`, & `share()`
    1.  TODO: finish
15. What's a Scheduler?
    1.  TODO: finish
16. What's the difference between hot & cold observables?
    1.  TODO: finish
17. How do you test RxJS? Pros & Cons?
    1.  Marble testing, which uses marble diagrams, represented in ASCII, to confirm the behavior of your streams
        1.  Pros
            1.  You can test that both the value & timing of notifications is as expected
            2.  Relatively easy to create & visualize streams
        2.  Cons
            1.  Involved setup
            2.  Required knowledge of testing helpers & marble syntax
    2.  Subscribe & Assert pattern, which involves you verifying results in the subscribe function
        1.  Pros
            1.  Much less setup involved (ie, typical testing APIs & patterns)
        2.  Cons
            1.  Must manually manage async test completion
                1.  careful planning is required to make sure your tests don't actually wait for the async things to happen
            2.  Extra boilerplate involved for making assertions
                1.  ie, VS marble testing, where much of this boilerplate is handled for you by the helper functions
            3.  Difficult to test timing of patterns
18. Marble Testing
    1.  What characters are used in marble testing? What do they mean?
        1.  `-` for 1 frame of virtual time
        2.  `[a-z0-9]` (alphanumerics) for emitted values
        3.  `#` for errors
        4.  `()` for groupings of synchronous values
        5.  `|` for complete notification
        6.  `^` for subscription point
        7.  `!` for unsubscribe point
    2.  What does the testScheduler do?
        1.  Exposes helpers to parse & compare ASCII diagrams
        2.  Contains functions that will allow us to run tests on async operators synchronously
        3.  Any async operators that appear inside the `testScheduler.run` callback automatically use the testScheduler so we can write synchronous test against previous async code. They will simulate the passing of time with virtual time instead. There is a time progression syntax for when many dashes become impractical.
            1.  Generally, all logic for your test should be placed inside the `run` function
            2.  Useful methods on the helper object passed to `run` include:
                1.  `cold` - lets us create a cold observable from a marble string. Cold observable subscriptions will start when the test begins.
                2.  `expectObservable` - accepts an observable & lets you compare the output of it to an expected marble diagram
                    1.  When you pass an observable to the `expectObservable` method, it converts this observable into an array of objects. These objects represent each emission, containing details like the notification type & frame. `toBe` does the same thing for the string you pass it. The function you provided to the TestScheduler on creation is then invoked with both arrays, and any assertions are run with the actual & expected output.
    3.  How do you test that your observables emitted values that don't fit in the ASCII diagram?
        1.  `cold`, `hot`, & `toBe` methods accept a second argument, a mapping of the values in ASCII string representations to another - arbitrary - value
    4.  How do you test that intermediate observable subscription / unsubscription happened correctly?
        1.  You can test that the observables contained in combined streams are subscribed to & unsubscribed from at the appropriate times
    5.  How would you verify how emissions that happened before subscription would impact your streams?
        1.  The `hot` helper method lets you create a hot observable who's subscription point you can identify using a `^`
    6.  What does a frame represent in marble diagrams? How do you interact with them?
        1.  TODO: finish
    7.  How do you model synchronous emissions for testing?
        1.  You surround the emitted values with parenthesis in your expected diagram. If the observable completes after emitting its final next notification, this complete notifaction must also be inside the expected diagram parenthesis.
    8.  When using time progression syntax, each emitted value advances a frame
        1.  TODO: finish, is this a common source of off-by-1 errors?
    9.  How do you test long running observables with no guaranteed completion?
        1.  TODO: finish
        2.  `expectObservable` accepts a second argument indicating when to unsubscribe manually from the observable under test
19. Subscribe and Assert Testing
    1.  How do you generate expected values?
        1. One option is to create an array of expected values, then assert against the value at each index in the subscribe function
        2. If you only need to test the final, emitted values - on completion - then you can use the `toArray` operator
    2.  What's a common gotcha when testing with Jest in this pattern?
        1.  Make sure to call `done` on complete notification, otherwise your assertions in the subscribe function will not run