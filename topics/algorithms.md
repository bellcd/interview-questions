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
         1. best case, the ideal input, Big Omega
         2. average case, Big Theta
         3. worst case, Big O
      3. What are the common time complexities, from fastest to slowest?
         1. O(1), constant
         2. O(log n), logarithmic
         3. O(n), linear
         4. O(n log n), super linear
         5. O(n^2), polynomial
         6. O(2^n), exponential
         7. O(n!), factorial
   2. When people in industry ask for the time complexity of an algorithm / Big-O, which one are they probably asking for?
      1. worst case
   3. Worst case time complexity is often - but not always - if a list is exactly reverse sorted.
5. Selection Sort
   1. Summarize
      1. Repeatedly finding the smallest number from the ever shrinking portion of the list that is still unsorted.
   2. List and explain the worst, average, and best case time complexities for Selection Sort.
      1. Worst O(n^2), average O(n^2), best O(n^2)
      2. As you increment through the list, you still have to look at every other yet-to-be-sorted value. The size of this yet-to-be-sorted portion of the list decreases by 1 with every iteration. So initially the yet-to-be-sorted portion of the list starts at position 0 and continues through the last index. So for this iteration you're doing (n - 1) comparisons. Next iteration, start at position 1, so length of the yet-to-be-sorted portion has decreased by 1, so you do (n - 2) comparisons. This continues until you're at the penultimate position, at which point the length of the yet-to-be-sorted portion is 2, which leaves 1 comparison left. So each of these iterations does of (yet-to-be-sorted portion of the list).length - 1 number of comparisons. So the number of comparisons in Selection Sort is (n - 1) + (n - 2) + (n - 3) ... 1. This expression simplifies to (n(n - 1)) / 2, which is a Big-O of O(n^2).
   3. Why are the worst, average, & best case time complexities for Selection Sort the same?
      1. Regardless of what the list initially looks like, for every position except the penultimate, the algorithm still needs to look at every other position in the yet-to-be-sorted portion of the list. So the time complexities are the same for worst, average, & best cases.
   4. Memory
      1. Selection Sort is an in place sort. You can swap any two elements in the list as you come across them. No need for a copy of the whole list.
   5. Stability
      1. Selection sort is unstable, although it can be made stable depending on the implementation.
   6. Typical use case
      1. None, there are generally better algorithms. Although Selection Sort is known for it's simplicity.
6. Insertion Sort
   1. Summarize
      1. Starting at the 2nd element, looping-backwards-through-part-of-the-list, comparing adjacent elements & swapping if necessary.
   2. List and explain the worst, average, and best case time complexities for Insertion Sort.
      1. Worst O(n^2), average O(n^2), best O(n)
      2. In the worst & average cases, the looping-backwards-through-part-of-the-list logic does a growing number of comparisons for outer loop iteration. Specifically, 1 + 2 + 3 + ... + (n - 1). This leads to (n(n -1 )) / 2 comparisons, or Big-O of O(n^2)
      3. In the best case (ie, when the list is already sorted), the looping-backwards-through-part-of-the-list logic only does 1 comparison - with the element right before it (ie, you don't have to re-sort things that are already sorted). That turns the looping-backwards-through-part-of-the-list portion of Insertion Sort into a O(1) operation. An outer loop with only O(1) operations inside it runs in O(n) time.
   3. Memory
      1. Insertion Sort is an in place.
   4. Stability
      1. Insertion Sort is stable.
   5. Typical use case
      1. Insertion Sort is only really used when you have an already sorted list, and you add - one, two, maybe a handful - of elements to it. In this close to best case scenario, the time complexity would approach O(n), because the looping-backwards-through-part-of-the-list logic is not O(1) only for the handful of elements that are not already sorted. An example of this would be in a database, when you're adding a key to a list of sorted keys.
7. Merge Sort
   1. Summarize
      1. Split your list in half until you have lists of 1 element. A list of 1 element is, by definition, sorted. Then merge your sorted lists of 1 element together.
   2. List and explain the worst, average, and best case time complexities for Merge Sort.
      1. Worst O(nlogn), average O(nlogn), best O(nlogn)
      2. Because you divide the list in half each time, you reduce the number of comparisons you have to do for every element in the list (ie, you avoid having the (n - 1) + (n - 2) ... + 1 number of comparisons that leads to O(n^2) complexity)
   3. Memory
      1. Merge Sort is out of place, because you need another array to hold all the elements in the list
   4. Stability
      1. Merge Sort is stable