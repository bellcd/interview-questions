# CSS

1. What does CSS stand for?
   1. Cascading Style Sheets
2. What is normal flow?
   1. Also called flow or block & inline layout, this is how the page is laid out by default
      1. Block level elements are laid out in the block direction (in English, displaying one after the other - vertically)
      2. Inline level elements are laid out in the inline direction - the direction a sentence goes in - (in English, horizontally)
3. How is the default behavior for block & inline boxes different?
   1. Block level elements will
      1. Take up all of the space in the inline direction
      2. Respect height, width, padding, & margin if provided
         1. If padding & margin are provided, it'll push things away from it (ie, make extra space)
   2. Inline level elements will
      1. Preserve 1 character (regardless of how many whitespace characters are in the HTML) of whitespace between each box in the inline level element
      2. Inline level elements can have padding & margins, but this will NOT push other elements away
         1. This is in contrast to how padding & margins affect block level elements (here, those things WILL push other elements away)
4. What is the default stylesheet in browsers for?
   1. Make the document readable (ie, so that we get a human readable document, and not a wall of text).
      1. Makes block level things have a value of `display: block`
      2. Headers bigger & bold
      3. Lists have bullets & are indented
      4. These changes are still accessible & responsive
5. What does `inline-block` do?
   1. inline-block elements only take up as much space in the inline direction as needed to fit their content
   2. Padding & margin are respected (as opposed to `inline` level elements which can have padding and margin, but in `inline` level elements these things will NOT push other elements away)
   3. [inline-block can assign a height property](https://stackoverflow.com/questions/8969381/what-is-the-difference-between-display-inline-and-display-inline-block)
6. What's the difference between
    1. CSS3 variables & SASS variables?
       1. TODO: finish this
    2. `flex-grow` & `flex-shrink`?
       1. `flex-grow` defines how fast a flex-item grows - along the main axis - compared to other items, while `flex-shrink` does the same thing for shrinking.
       2. These are typically defined in the `flex` property, which by default is `flex: 0 1 auto;`
    3. Setting flex-basis to `auto` VS `0` VS a fixed size (pixels, rems, etc...)
       1. `auto` is saying size the flex item based on the intrinsic size of the flex item's content
       2. `0` is saying that flex item does NOT have any intrinsic size
       3. A fixed size is saying that flex item has an intrinsic value of that-fixed-size
       4. This matters because `flex-grow` & `flex-shrink` can only use the amount of space that's available AFTER each item is laid out based on its `flex-basis`
    4. The explicit and implicit grid with CSS grid?
       1. The explicit grid is when you tell the browser to create a grid with this many tracks (ie, by defining `grid-template-rows` & `grid-template-columns` properties)
       2. The implicit grid is additional tracks that the browser creates because there are more items to add to the grid than you explicitly defined space for. (or if you place an item outside the bounds of the explicit grid).
       3. Tracks will be auto sized (ie, big enough to fit the content).
7. What are some common shorthands of `flex`?
   1. `flex: auto;`
      1. same as `flex: 1 1 auto;`
   2. `flex: initial;`
      1. `flex: 0 1 auto;`
   3. `flex: none;`
      1. `flex: 0 0 auto;`
   4. `flex: 1;`
      1. `flex: 1 0 0;`
   5. [docs](https://developer.mozilla.org/en-US/docs/Web/CSS/flex)
8. Explain:
   1. selectors
      1. These are the things you use to target the elements you want to apply CSS to
      2. Several selectors include
         1. id, class, type, & descendent
      3. You can combine several selectors
      4. [docs](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors)
   2. How does generated content work with the selectors `::before` & `::after`?
      1. The content is placed as the first / last child of the element you apply it to
      2. One technique is to use generated content, specifically `content: '';`, to be able to style grid items that otherwise have no content
   3. ruleset (or simply rule)
      1. [the whole structure that people typically think of when describing CSS](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/CSS_basics)
      2. contains one or more selectors and one or more declarations
         1. each declaration consists of a property & a property value
   4. specificity
      1. This is a value that is computed for every CSS selector. It solves the following problem:
      2. When there are two or more selectors that target the same element with mutually exclusive styles, whose styles get applied? (ie, `color: red` & `color: blue`)
      3. The selector with the higher specificity gets applied
      4. useful resources
         1. [spec](https://www.w3.org/TR/selectors/#specificity)
         2. [visualization](https://dev.to/emmabostian/css-specificity-1kca)
         3. [interactive tool](https://specificity.keegan.st/)
         4. [docs](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity)
         5. [funny thing that will help you remember specificity](https://specifishity.com/)
   5. BEM
      1. [BEM (Block, Element, Modifier)](https://en.bem.info/methodology/quick-start/) is a naming convention around classes and how they are used
   6. What's the point of using something like BEM?
      1. Enforcing a consistent approach like this (even if it's not specifically BEM!) helps with readability, maintainability, & makes the codebase easier to reason about & change, especially as it grows & with lots of developers
   7. Pros & cons of the BEM naming convention to only have 1 element in the name
      1. Only having one (1) element listed in the name, rather than having the whole breadcrumb path (ie, the DOM node hierarchy) of every other element that's above it, keeps the codebase more concise, & allows you to adjust the DOM structure (ie, which elements are nested inside which other elements) **WITHOUT having to edit a bunch of CSS class names - the element names - to reflect the new DOM hierarchy you just changed.**
      2. As a tradeoff, you don't see that DOM hierarchy in the CSS class names
   8. Why would you namespace with prefixes?
      1. [Improves code readability](https://csswizardry.com/2015/03/more-transparent-ui-code-with-namespaces/)
   9.  CSS Flexbox
      2. TODO: finish
   10. CSS Grid
       1. Lines
          1. These are the lines that make up your grid
          2. Specifying a gap increases the thickness of these lines
          3. The space between two lines is called a track - both column tracks & row tracks
       2. Cell
          1. The area between 4 grid lines
          2. Direct children in the grid container get auto placed into each cell
       3. Sizing keywords
          1. `auto` - Looks at the size of the content, and makes the track as big as needed. For columns, this will stretch to take up available space.
          2. `min-content` - Tracks will be the smallest the content can possibly be (ie, via soft-wrapping)
          3. `max-content` - Tracks will be as big as they can (may cause overflows of the grid container)
          4. `fit-content()` - You pass a value. It tries to go to max-content, but not beyond the value you pass. Then it wraps.
          5. `fr` - These represent proportions of the available space, after any gaps & fixed length tracks are accounted for. Only available to grid layouts.
             1. `fr` is is really `minmax(auto, 1fr)`. ie, distributing available space from a minimum size to fit the content.
          6. `minmax()` - Allows you to set a minimum and maximum value for the size of a track.
             1. Setting `minmax(0, 1fr)` is saying this thing has no minimum size. So start from 0, and distribute the space. (may cause overflows)
          7. `repeat()` - Allows you to repeat tracks, or groups of tracks
          8. `auto-fill` - You telling the browser to fit as many tracks of a particular size as you can
             1. Especially useful with `minmax()` for the size, as you could have each track expand when the browser can't fit another track of a given minimum size
          9. `auto-fit` - You'll only see the difference between `auto-fill` & `auto-fit` when there aren't enough elements to fill up the first row.
             1.  `auto-fill` Leaves the space for those tracks in the layout
             2.  `auto-fit` Collapses the space for those tracks. The tracks are still there, but they take up no space.
       4. Auto placement
          1. The browser will attempt to place any child elements into the grid, starting with the ones you have specified positions for.
          2. Auto placed items can span more than one track with `span`
       5. Alignment
          1. Grid is writing mode aware, so the block & inline axes for the grid can change depending on the writing mode. For English, the block axis is vertical & inline axis is horizontal.
          2. Properties that adjust the block axis start with the prefix `align`, (`align-content`, `align-items`, `align-self`).
          3. For the inline axis, you use properties that begin with `justify`, (`justify-content`, `justify-items`, `justify-self`).
          4. Properties that end with `-content` are for sharing out extra space. You'll have extra space if your grid tracks don't add up to the size of the grid container. The `-content` properties, `align-content` & `justify-content`, are only going to make a difference if you have spare space to distribute. ie, if you're using tracks defined with `fr`, there won't be any spare space, so these properties won't do anything! The default for the `-content` properties is `start` (so for English, top left).
          5. For the alignment of the content within each cell, you use the properties that end in `-items`, (`align-items` & `justify-items`). The default for these is `stretch`. (Except when you have a direct child with an instrinsic aspect ratio, ie an image. Then it's `start`).
          6. Properties that end in `-items` sets the values on the whole group - all of the items in the grid at once. To change these values on only 1 particular item at a time, use `-self` (`align-self` & `justify-self`). The `-self` properties go on the grid item (instead of the grid container).
9.  What's the difference between Flexbox & Grid? Why would you use one over the other?
   11. TODO: finish
10. What CSS would you use to turn a span into a button?
    - This is possible with things like `border-radius`, `box-shadow`, `background-color`, `border`, etc ... But you would want to avoid this if possible for many reasons (ie, [by default buttons can be tabbed into & are hooked up to event handlers](https://developer.mozilla.org/en-US/docs/Learn/Accessibility/HTML)). It would probably be better to take the default functionality of a button and adjust its styling to what you need.
11. Describe the cascading part of CSS
   12. CSS rules can override each other, and [the cascade of CSS determines what actually gets displayed](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Cascade_and_inheritance) when more than one property value applies to the same property of the same element.
   13. In general, the order is:
      1. Importance
      2. Specificity
      3. Source order
12. What HTML & CSS would you use to make a horizontal nav bar?
   14. One approach is to [use a flexbox](https://codepen.io/bellcd/pen/VwvQrdx).
13. What is a float? and the `clear` property?
   15. A floated element moves to the left or right of its container, allowing text & inline elements to flow around it. Floated elements are removed from normal document flow.
14. What values of the CSS display property can you remember offhand?
   16. [docs](https://developer.mozilla.org/en-US/docs/Web/CSS/display)
15. What's the difference between inner & outer values of `display`?
    1. The outer value sets how the element interacts in flow layout
    2. The inner value sets how the element's direct children behave
    3. [spec](https://www.w3.org/TR/css-display-3/#the-display-properties)
16. What would you do to make a website responsive?
   17. Make sure you're layout will adapt for every screen size and shape you're targeting (ie, mobile / tablet / desktop / etc ...), using things like [flexible grids & media queries](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Responsive_Design)
17. I say to you make a website, do you choose vanilla JavaScript, React, Angular, Vue, jQuery, or something else? Why?
    1. Depends on a number of things including [features, size, budget, timeframe, & technical skill level of the maintainers.](https://stackoverflow.blog/2020/02/03/is-it-time-for-a-front-end-framework/)
18. What are CSS Preprocessors / CSS extension languages (SASS / LESS / etc... )? Pros / Cons?
      1. CSS Preprocessors ([like SASS](https://sass-lang.com/)) compile what you've written in their specific syntax into standards compliant CSS.
      2. Pros
         1. Generally far easier for developers to work with, especially in larger codebases
         2. Includes extra features that can make your code DRYer or more performant (ie, nesting / @mixins / @use). NOTE: sometimes features introduced in preprocessors end up as spec in later versions of CSS (ie, variables)
      3. Cons
         1. Another learning curve
19. What are styled components & how do they work?
    1. TODO: finish
20. How would theme-ing work with styled components?
    1. TODO: finish
21. Difference between `display: none` & `visibility: hidden`?
    1.  `display: none` **removes the element from the DOM**. So if something needs the element there (accessibility is a big reason, perhaps layout also), the element will not be there
    2.  `visibility: hidden` hides the element, but it's still in the DOM. Screen readers can still find it, and it still takes up space in the layout
22. How would you scale an image responsively? Are there drawbacks to doing this?
    1.  TODO: finish
23. Describe the CSS box model
    1.  Every element the browser renders is represented as a box, described by [the CSS box model](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model). You can think of the CSS box model as being made up of 4 smaller boxes, Russian nesting doll style. Every one of these 4 boxes can have a width / height of 0 or greater. From the outside going in, the order is:
        1.  margin box
        2.  border box
        3.  padding box
        4.  content box - this is where the actual content is (text, image, video player, etc...)
24. What is `border-box`?
    1.  If you assign a width (or height), by default, that width is the size of the content box. Padding & border (& margin) will be ADDED to that.
        1.  This is defined through the `box-sizing` property, which is `content-box` by default
    2.  Changing to `border-box`, will make the value you assign to width INCLUSIVE of the padding & border. So the amount of available space for that box's content will shrink (by the amount taken up by padding & border).
    3.  [docs](https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing)
25. Describe the `writing-mode` property
    1.  Changes which direction inline content flows in & which direction block level elements stack in
    2.  English is `horizontal-tb`
    3.  [docs](https://developer.mozilla.org/en-US/docs/Web/CSS/writing-mode)
26. What are `inline-size` & `block-size`?
    1.  These are replacements for width & height. Width & height are fixed to physical dimensions, whereas `inline-size` & `block-size` will change directions appropriately if you use a different `writing-mode`.
    2.  [docs](https://developer.mozilla.org/en-US/docs/Web/CSS/inline-size)
    3.  There are appropriate alternate properties for [border, padding, & margin as well](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Logical_Properties/Basic_concepts)
27. How do you center an item?
    1.  You can use [flexbox with `justify-content` & `align-items`](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox)
28. What does setting a margin with a value of `auto` do?
    1.  It absorbs all of the available space in the direction that it's applied in, pushing it away from other items.
    2.  Useful for the common layout pattern for navigation bars of many elements on one side, and one or two pushed to the other side
29. What is `grid-template-areas`? When is it appropriate to use it?
    1. Defining your grid, ASCII art style, in a CSS property
    2. Every cell in the grid must be accounted for
    3. Most appropriate for:
       1. Smaller grids
       2. Grids with a definite amount of items (the amount of cells displayed is not going to change dynamically)
       3. It's much faster (and perhaps lower cognitive load) to adjust the layout of your grid items in the ASCII art, rather than adjusting the start & end lines for each item's CSS properties
30. Are there conventions for naming grid lines? Any benefits?
    1.  Yes, using `-start` & `-end` on lines you name matches a feature the CSS grid does. This allows you to, for example,
        1.  Place an item using a given name, without having to define that name in `grid-template-area` (ie, with `container-start` & `container-end` named lines outlining an area, you could use `grid-area: container` to place an item).
    2.  If you have an area `main` defined with `grid-template-areas`, CSS grid will generate `main-start` & `main-end` lines. You could then use those lines to place some other item, allowing for overlap.
31. Are the `align-` & `justify-` properties used with flexbox or grid?
    1.  Trick question, those properties are part of the Box Alignment specification. So although they started in flexbox, they are now used for both flexbox & grid (and perhaps others as well).
32. Does an element with a higher `z-index` always appear appear to be stacked 'on top of' an element with a lower `z-index`? Why?
    1. Not always. **Sibling** elements appear stacked from top to bottom, based on which has the higher `z-index`. If one of those siblings happens to have children (or descendants) that itself has a `z-index` that is higher than one of the other original siblings, the child element will still not appear stacked above the other sibling in question. [Useful example.](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context#the_example)