# Computer Science Fundamentals

1. Describe each data structure.
   1. Stacks
      1. Often visualized as a real world stack (ie, a stack of plates), whereby each new element is added to the top. Uses Last In First Out (LIFO) access order, which means the element added LAST is now the FIRST element that will get removed.
      2. Examples
         1. Call stacks
         2. Your browsing history, ie - what you access with the back button
      3. A JavaScript `array` works very nicely as a stack, with the `push` and `pop` methods.
   2. Queues
      1. Often visualized as a real world queue (ie, a checkout queue). Uses First In First Out (FIFO) access order, which means the elements are accessed in the order they were added.
      2. Examples
         1. Keyboard buffer
         2. Customer service ticketing systems
      3. In JavaScript, you would want to make a singly linked list, with `head` & `tail` references. Using an array, each `dequeue` operation is `O(n)`
2. Explain
   1. Factory & Singleton patterns
      1. TODO: finish
   2. two-way data binding and one-way data flow, and how they are different?
      1. TODO: finish
3. What does great code look like to you?
   1. Great code to me is code that fulfills its purpose as efficiently as possible. There are a few things to unpack in that statement:
      1. what is "its purpose"?
         1. be as fast as possible? - then it should probably be written in a language that's pretty 'close to the metal', ie not JavaScript
         2. able to be understood by people who aren't intimately familiar with it?
            1. then variable names like `a` & `b` wouldn't be appropriate, and perhaps something like `questionCountByTopicByPreference` is reasonable
      2. what is "as efficiently as possible"? efficient for what? or who?
         1. again - is execution speed the primary concern? memory used? What about likelihood of introducing future bugs with changes & new features? The development cost of finding & fixing those bugs? The priorities around all of these need to be considered.
         2. something like DRY - don't repeat yourself. It's something of a mantra to some developers. But in certain situations (ie, test suites, for instance), you could argue for a certain level of repetition - to make the code more explicit, and make bugs less likely / less difficult to find.
   2. Ideally, these types of priorities are decided at the team & business level, and wouldn't be constantly shifting.