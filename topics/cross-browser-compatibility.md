# Cross-Browser Compatibility

1. Why is it important?
   1. to make sure your code runs correctly on many different browsers
   2. fail gracefully
      1. ie, without JavaScript / CSS, there's still a basic UX there
   3. more efficient workflow - save time
      1. [validating your code](https://validator.w3.org/) can help prevent issues before they come up
2. Should you target all modern browsers for every app you build?
   1. no, design for the browsers your audience uses
3. What are some useful considerations?
   1. frameworks can generally preempt a lot of cross browser issues
      1. this was a big selling feature of jQuery (and now things like Angular / React / Vue)
   2. Some fancy features might not be necessary
   3. Test difficult browsers first (IE 6)
   4. feature detection / polyfills if needed
   5. Use automated tools like Selenium to make this process easier