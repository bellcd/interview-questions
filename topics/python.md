# Python

1. What is Python?
   1. Python is a high level, object oriented, dynamically typed general purpose programming language.
2. Why is it useful?
   1. The syntax is particularly clean, easy to understand (it tends to read like English)
   2. Comes with many best practices built in (ie, comparison operators)
3. How do you make escape characters in Python?
   1. Use the `\` character in a string immediately before the character you want to escape
   2. What are some common escape sequences?
      1. `\"`
      2. `\'`
      3. `\\`
      4. `\n`
4. How do you do comments in Python?
   1. the `#` character
5. How do formatted strings work in Python?
   1. `f"{this-expression-will-be-evaluated-at-runtime} {this-one-too}"`
6. How do you represent numbers in different bases in Python?
   1. you use the appropriate prefix
      1. binary - 0b10 represents the binary value '10', ie 2
      2. hexadecimal - 0x14f represents the hexadecimal value '14f', ie 335
      3. to print numbers in non-decimal systems, you use the appropriate built-in function (ie, `bin()`, `hex()`, etc...)
7. What are some arithmetic operators in Python that don't exist in other programming languages
   1. `//` - floor division. ie, division, then go left on the number line to the next whole number
   2. `**` - exponents
8. Can you do `i++` in Python?
   1. No, Python doesn't have increment / decrement operators, but it does have augmented assignment operators for all of the arithmetic operators, ie `x *= 2`
9.  Can you set constants in Python?
   2. No, you only set variables with the `=` operator. By convention, variables set `IN_ALL_UPPERCASE` indicates to other variables that it is a constant, and should not be changed.
10. Where are the docs for Python
   3.  [docs.python.org](https://docs.python.org/3)
11. What happens if you run `print('1' + 1)` in Python?
    1.  You get a TypeError.
    2.  Python is a strongly typed language, in the sense that there is no implicit type conversion. So in situations like the above, Python chooses to error, instead of converting either the string to a number OR the number to a string, to go down either of those paths.
        1.  There are a number of built-in type conversion functions to address this:
            1.  `int()`
            2.  `float()`
            3.  `bool()`
            4.  `str()`
12. What does truthy & falsy mean in Python?
    1.  Certain values convert to `False` when used in a boolean context. Everything else will return `True`
        1.  Falsy values in Python are
            1.  `''`, empty string
            2.  `0`, the number zero
            3.  `[]`, empty list
            4.  `None`, the concept none, exactly the same as the concept null in C based languages
13. What are the comparison operators in Python?
    1.  `==`, equal
    2.  `!=`, not equal
    3.  `>=` / `<=`, greater than or equal to / less than or equal to
    4.  `>` / `<`, greater than / less than
14. How does indentation & braces (curly braces) work in Python?
    1. Instead of using braces `{}` to identify a code block, Python uses indentation. So an if conditional looks like this
    ```Python
      if price > 100:
        print('expensive')
      elif price > 50:
        print('normal')
      elif price > 0:
        pass
      else:
        print('free')
      print('finished')
    ```
15. What is the `pass` keyword for?
    1.  you can't have an empty block in Python. So there is a `pass` keyword when you want nothing to happen in that block.
16. What are the logical operators in Python?
    1.  `and`, `or`, & `not`
17. What is chaining comparison operators in Python?
    1.  A feature that allows you to write comparison operators the same way you write them in math.
        1.  `age >= 10 and age < 65` could be written as
        2.  `10 <= age < 65` <- using comparison operators
18. How do ternary operators work in Python?
    1.  `[true-condition] if [condition-to-test] else [false-condition]`
    ```Python
      happy = false
      greeting = 'Hello!' if happy == true else 'What do you want?'
    ```
19. Describe the two loops in Python and how they work.
    1.  `for` - can iterate over any iterable (strings, lists, ranges, etc...)
          ```Python
            for x in 'Python':
              print(x)
          ```
    2. `while` - iterates while the condition is true. They also have an optional `else` block - only executed if the while loop completes successfully without using a `break` statement.
20. Does the `range()` function return a list? What's a benefit of using `range()`?
    1.  No, it returns an instance of the range class.
    2.  Range objects don't store every valid value for them, so they take up much less space when dealing with huge values.
21. What does the `for...else` clause do in Python?
    1.  If the for loop iterates over every element in the iterable (ie, without triggering a `break` statement), the `else` clause gets executed. This is useful as a cleaner way of handling certain common situations that might otherwise require flags.
22. Talk about functions in Python
    1.  Defined using `def`
    2.  By default, functions return the `None` value
    3.  Python functions can return multiple values, with something called a tuple. Tuples in Python are ordered, immutable collections. They are written with parentheses, ie `my_tuple = (1, 3, 5, 7)`
    4.  Python can have keyword arguments, where you list the name of the argument(s) at the function invocation site, ie `add(num1=2, num2=4)`
    5.  you can have default arguments, similar to many other languages
    6.  Python functions can also use type annotation / type hinting
23. How would you pass a variable number of arguments to a function in Python?
    1.  Use the `*` character before the relevant parameter, and Python will package the remaining arguments into that variable as a tuple.
    2.  Or use the `**` characters in the same way, to have Python make a dictionary of the keyword arguments
24. How does scope work in Python
    1.  Local variables that have function scope
    2.  Global variables that have file scope
    3.  There's no block level scope in Python
    4.  If you attempt to reassign a global variable inside a function, the Python interpreter will instead create a new, local variable with the same name. This was done as a best practice. There is a way to change this behavior, using `global name-of-the-global-variable-you-want-to-reassign` in the function. This is generally considered a bad practice, as it easily leads to bugs.