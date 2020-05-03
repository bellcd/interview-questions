# Testing

1. Explain:
   1. TDD
      1. TODO: finish
   2. AAA
      1. AAA a pattern for organizing your test code
         1. Arrange - setup for that particular test
         2. Act - triggering event necessary for the test
         3. Assert - making your assertions on what conditions should exist
2. What's the difference between:
   1. BDD & TDD
      1. TODO: finish
   2. Unit VS Integration VS End to End
      1. Unit
         1. the smallest type of testing, ideally (but not always!) a self contained function
         2. Majority of your tests are likely to be unit tests
         3. doesn't rely on the existence / uptime of other systems for the test to run (ie, not actually calling an API / database)
            1. so it's necessary to use spies, stubs, mocks
      2. Integration
         1. testing how two or more systems interact (ie, integrate)
         2. does actually involve calling APIS / databases
         3. by necessity, will be slower to run & more fragile than unit tests
      3. End to End
         1. testing how an entire system operates, ie running a sample user session that interacts with many parts of your system with a specialized library like Puppeteer
         2. The idea is to replicate how a user is likely to interact with your system
   3. Spies VS Stubs VS Mocks
      1. CAVEAT: These words can mean different things to different people in relation to different languages. [I know them to mean](https://codepen.io/bellcd/full/RwPaGmP):
         1. Spies
            1. Your function still does its thing, as normal
            2. You want extra information about how / how many times the function was called, its arguments, `this` context, return values, etc...
         2. Stubs
            1. You get all the extra information (like a Spy)
            2. You define special behavior for this function, this Stub
         3. Mock
            1. Everything a Stub does
            2. You also define expectations (ie, what you expect to happen)
3. How many conditions should you test?
   1. bare minimum - happy path (ie, what the function is supposed to handle)
   2. good - several unhappy paths (ie, typos / malicious input / etc... )
   3. excellent - many more unhappy paths
   4. ideal - as many tests as are reasonable
      1. what's "reasonable" is highly debated & personal
4. What are several options for where your testing date can live?
   1. hardcoded in the tests themselves
      1. Pros - easier & faster to see what's going on & debug
      2. Cons - managing the test data for many tests can get unwieldy as the codebase grows
   2. test data files
      1. Pros - single source of truth for the test data, easier to manage as the codebase grows
      2. Cons - not as easy / fast to debug
5. Is it always better to test implementation OR behavior?
   1. Both have their place, but in general you probably want to lean more towards testing behavior (even in unit tests!) rather than implementation. This leads to more resilient tests (ie, they're less likely to break after every tiny refactor)
   2. Testing implementation can become necessary when there is complex logic / many conditionals / etc...