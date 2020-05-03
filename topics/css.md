# CSS

1. What does CSS stand for?
   1. Cascading Style Sheets
2. What's the difference between
    1. inline and inline-block?
       1. [inline-block can assign a height property](https://stackoverflow.com/questions/8969381/what-is-the-difference-between-display-inline-and-display-inline-block)
    2. CSS3 variables & SASS variables?
       1. TODO: finish this
3. Explain:
   1. selectors
      1. TODO: finish
   2. specificity
      1. TODO: finish
   3. BEM
      1. [BEM (Block, Element, Modifier)](https://en.bem.info/methodology/quick-start/)
   4. What's the point of using something like BEM?
      1. Having a consistent naming convention around classes and how they are used helps with readability, maintainability, & makes the codebase easier to reason about & change, especially as it grows & with lots of developers
   5. Pros & cons of the BEM naming convention to only have 1 element in the name
      1. Only having one (1) element listed in the name, rather than having the whole breadcrumb path (ie, the DOM node hierarchy) of every other element that's above it, keeps the codebase more concise, & allows you to adjust the DOM structure (ie, which elements are nested inside which other elements) **WITHOUT having to edit a bunch of CSS class names - the element names - to reflect the new DOM hierarchy you just changed.**
      2. As a tradeoff, you don't see that DOM hierarchy in the CSS class names
   6. Why would you namespace with prefixes?
      1. [Improves code readability](https://csswizardry.com/2015/03/more-transparent-ui-code-with-namespaces/)
4. What CSS would you use to turn a span into a button?
    - TODO: finish
5. Describe the cascading part of CSS
    - TODO: finish
6. What HTML & CSS would you use to make a horizontal nav bar?
   1. TODO: finish
7. What is a float?
   1. A floated element moves to the left or right of its container, allowing text & inline elements to flow around it
8. What values of the CSS display property can you remember offhand?
   1. [docs](https://developer.mozilla.org/en-US/docs/Web/CSS/display)
9. What would you do to make a website responsive?
   1. TODO: finish
10. I say to you make a website, do you choose vanilla JavaScript, React, Angular, Vue, jQuery, or something else? Why?
    1. TODO: finish