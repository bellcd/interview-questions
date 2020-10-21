# RxJS
// TODO: add links

1. What is RxJS?
   1. The JavaScript version of the ReactiveX programming library
2. What problem does it solve?
   1. Simplifies much of the callback hell that promises (in JavaScript) solve, but for multiple values - where promises resolve to a single value. The value of the benefits grows with the complexity of the app.
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