# Trivia

1. Do `[] == 0` & `[] === 0` return the same value? why? what value(s)?
   ```JavaScript
   [] == 0 // true, because [] >>> "" >>> 0, then compared with 0
   [] === 0 // false, because no coercion takes place, so [] compared with 0
   ```
   1. JavaScript type coercion can have complicated rules / sequences that are not always immediately intuitive, so be careful!
   2. [high level overview](https://www.freecodecamp.org/news/js-type-coercion-explained-27ba3d9a2839/)
   3. [stackoverflow example](https://stackoverflow.com/questions/5491605/empty-arrays-seem-to-equal-true-and-false-at-the-same-time)
   4. [visual reference](https://dorey.github.io/JavaScript-Equality-Table/)
   5. [spec](https://www.ecma-international.org/ecma-262/5.1/#sec-11.9.3)