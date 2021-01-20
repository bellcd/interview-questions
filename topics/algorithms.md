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
         1. We commonly refer to the size of the input as **n**
      2. There are 3 time complexities for every algorithm
         1. best case
         2. average case
         3. worst case
   2. When people in industry ask for the time complexity of an algorithm / Big O, which one are they probably asking for?
      1. worst case
   3. Worst case time complexity is often - but not always - if a list is exactly reverse sorted.
5. Selection Sort
   1. Summarize
      1. Repeatedly finding the smallest number from the ever shrinking portion of the list that is still unsorted.
   2. List and explain the worst, average, and best case time complexities for Selection Sort?
      1. Worst O(n^2), average O(n^2), best O(n^2)
      2. As you increment through the list, you still have to look at every other yet-to-be-sorted value. The size of this yet-to-be-sorted portion of the list decreases by 1 with every iteration. So initially the yet-to-be-sorted portion of the list starts at position 0 and continues through the last index. So for this iteration you're doing (n - 1) comparisons. Next iteration, start at position 1, so length of the yet-to-be-sorted portion has decreased by 1, so you do (n - 2) comparisons. This continues until you're at the penultimate position, at which point the length of the yet-to-be-sorted portion is 2, which leaves 1 comparison left. So each of these iterations does of (yet-to-be-sorted portion of the list).length - 1 number of comparisons. So the number of comparisons in Selection Sort is (n - 1) + (n - 2) + (n - 3) ... 1. This expression simplifies to (n(n - 1)) / 2, which is a Big O of O(n^2).
   3. Why are the worst, average, & best case time complexities for Selection Sort the same?
      1. Regardless of what the list initially looks like, for every position except the penultimate, the algorithm still needs to look at every other position in the yet-to-be-sorted portion of the list. So the time complexities are the same for worst, average, & best cases.
   4. Memory
      1. Selection Sort is an in place sort. You can swap any two elements in the list as you come across them. No need for a copy of the whole list.
   5. Stability
      1. Selection sort is unstable, although it can be made stable depending on the implementation.