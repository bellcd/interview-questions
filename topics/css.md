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
      1. These are the things you use to target the elements you want to apply CSS to
      2. Several selectors include
         1. id, class, type, & descendent
      3. You can combine several selectors
      4. [docs](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors)
   2. ruleset (or simply rule)
      1. [the whole structure that people typically think of when describing CSS](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/CSS_basics)
      2. contains one or more selectors and one or more declarations
         1. each declaration consists of a property & a property value
   3. specificity
      1. This is a value that is computed for every CSS selector. It solves the following problem:
      2. When there are two or more selectors that target the same element with mutually exclusive styles, whose styles get applied? (ie, `color: red` & `color: blue`)
      3. The selector with the higher specificity gets applied
      4. useful resources
         1. [spec](https://www.w3.org/TR/selectors/#specificity)
         2. [visualization](https://dev.to/emmabostian/css-specificity-1kca)
         3. [interactive tool](https://specificity.keegan.st/)
         4. [docs](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity)
         5. [funny thing that will help you remember specificity](https://specifishity.com/)
   4. BEM
      1. [BEM (Block, Element, Modifier)](https://en.bem.info/methodology/quick-start/) is a naming convention around classes and how they are used
   5. What's the point of using something like BEM?
      1. Enforcing a consistent approach like this (even if it's not specifically BEM!) helps with readability, maintainability, & makes the codebase easier to reason about & change, especially as it grows & with lots of developers
   6. Pros & cons of the BEM naming convention to only have 1 element in the name
      1. Only having one (1) element listed in the name, rather than having the whole breadcrumb path (ie, the DOM node hierarchy) of every other element that's above it, keeps the codebase more concise, & allows you to adjust the DOM structure (ie, which elements are nested inside which other elements) **WITHOUT having to edit a bunch of CSS class names - the element names - to reflect the new DOM hierarchy you just changed.**
      2. As a tradeoff, you don't see that DOM hierarchy in the CSS class names
   7. Why would you namespace with prefixes?
      1. [Improves code readability](https://csswizardry.com/2015/03/more-transparent-ui-code-with-namespaces/)
   8. CSS Flexbox
      1. TODO: finish
   9.  CSS Grid
      2. TODO: finish
4. What's the difference between Flexbox & Grid? Why would you use one over the other?
   1. TODO: finish
5. What CSS would you use to turn a span into a button?
    - This is possible with things like `border-radius`, `box-shadow`, `background-color`, `border`, etc ... But you would want to avoid this if possible for many reasons (ie, [by default buttons can be tabbed into & are hooked up to event handlers](https://developer.mozilla.org/en-US/docs/Learn/Accessibility/HTML)). It would probably be better to take the default functionality of a button and adjust its styling to what you need.
6. Describe the cascading part of CSS
   1. CSS rules can override each other, and [the cascade of CSS determines what actually gets displayed](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Cascade_and_inheritance) when more than one property value applies to the same property of the same element.
   2. In general, the order is:
      1. Importance
      2. Specificity
      3. Source order
7. What HTML & CSS would you use to make a horizontal nav bar?
   1. One approach is to [use a flexbox](https://codepen.io/bellcd/pen/VwvQrdx).
8. What is a float? and the `clear` property?
   1. A floated element moves to the left or right of its container, allowing text & inline elements to flow around it. Floated elements are removed from normal document flow.
9.  What values of the CSS display property can you remember offhand?
   2. [docs](https://developer.mozilla.org/en-US/docs/Web/CSS/display)
10. What would you do to make a website responsive?
   3. Make sure you're layout will adapt for every screen size and shape you're targeting (ie, mobile / tablet / desktop / etc ...), using things like [flexible grids & media queries](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Responsive_Design)
11. I say to you make a website, do you choose vanilla JavaScript, React, Angular, Vue, jQuery, or something else? Why?
    1. Depends on a number of things including [features, size, budget, timeframe, & technical skill level of the maintainers.](https://stackoverflow.blog/2020/02/03/is-it-time-for-a-front-end-framework/)
12. What are CSS Preprocessors / CSS extension languages (SASS / LESS / etc... )? Pros / Cons?
      1. CSS Preprocessors ([like SASS](https://sass-lang.com/)) compile what you've written in their specific syntax into standards compliant CSS.
      2. Pros
         1. Generally far easier for developers to work with, especially in larger codebases
         2. Includes extra features that can make your code DRYer or more performant (ie, nesting / @mixins / @use). NOTE: sometimes features introduced in preprocessors end up as spec in later versions of CSS (ie, variables)
      3. Cons
         1. Another learning curve
13. What are styled components & how do they work?
    1. TODO: finish
14. How would theme-ing work with styled components?
    1. TODO: finish
15. Difference between `display: none` & `visibility: hidden`?
    1.  `display: none` **removes the element from the DOM**. So if something needs the element there (accessibility is a big reason, perhaps layout also), the element will not be there
    2.  `visibility: hidden` hides the element, but it's still in the DOM. Screen readers can still find it, and it still takes up space in the layout
16. How would you scale an image responsively? Are there drawbacks to doing this?
    1.  TODO: finish
17. Describe the CSS box model
    1.  Every element the browser renders is represented as a box, described by [the CSS box model](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model). You can think of the CSS box model as being made up of 4 smaller boxes, Russian nesting doll style. Every one of these 4 boxes can have a width / height of 0 or greater. From the outside going in, the order is:
        1.  margin
        2.  border
        3.  padding
        4.  content - this is where the actual content is (text, image, video player, etc...)