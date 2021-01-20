# Algorithms

1. What's the difference between an algorithm & a heuristic (in computer science)?
   1. An algorithm will always produce a correct answer, regardless of how long it would take.
   2. A heuristic usually produces an answer that's sufficient, but there's no guarantee the result will be correct 100% of the time (ie, for every set of inputs)
2. Why would you use a heuristic instead of an algorithm?
   1. If the algorithm is impractical (ie, takes too long to run or uses too much space)
3. What's the difference between?
   1. Out of place VS in place sorts:
      1. In place means that you leave the data structure intact, no copy is made. You simply shuffle things around.
      2. Out of place is when you need an equal amount of storage to the data structure you're sorting. ie, you're making a copy of the data structure
   2. Stable VS unstable sorting
      1. A stable sort means that the sort guarantees the ordering of duplicates will be unchanged from before and after the sort.
      2. An unstable sort means there is no guarantee duplicates will be in the same order before and after the sort.
4. Time Complexity
   1. Explain time complexity
      1. Time complexity is how quickly the runtime grows, relative to the input, as the input gets arbitrarily large.
      2. There are 3 time complexities for every algorithm
         1. best case
         2. average case
         3. worst case
   2. When people in industry ask for the time complexity of an algorithm / Big O, which one are they probably asking for?
      1. worst case
   3. Worst case time complexity is often - but not always - if a list is exactly reverse sorted.