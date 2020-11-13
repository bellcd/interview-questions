# SVG

1. What is SVG?
   1. [Scalable Vector Graphics](https://developer.mozilla.org/en-US/docs/Web/SVG) - it's an open source web standard for describing two dimensional vector graphics
2. Pros / Cons of using SVGs?
   1. Pros
      1. One asset that can scale to any size (ie, instead of having to load multiple raster images of different sizes)
      2. Less HTTP requests to handle (potentially 0 if you put the SVG asset inline)
      3. Possible (with proper design) to have very small filesizes
      4. Easy to animate, already has a navigable DOM (ie, as opposed to a raster image, where you would need to create a navigable DOM for that image)
      5. Easy to make accessible (for example, data visualizations would find this quite useful)
   2. Cons
      1. TODO: finish
3. Is SVG widely supported?
   1. SVG support used to be an issue, [this is no longer the case](https://caniuse.com/?search=svg)
4. Explain how position & scaling work in SVG, and how that relates to the viewport, viewBox, viewport coordinate system, & user coordinate system.
   1. One analogy you'll hear is to think of SVG as a piece of graph paper, "SVG is kind of like looking at a piece of graph paper that's infinite in all directions" - Sarah Dresner. In this analogy, the piece of graph paper is the SVG canvas - all the code that's inside your `<svg>`
   2. viewport
      1. SVG is a document, in a similar way to HTML being a document. When you add an `<svg>` element, you have added an `<svg>` document. All the content inside of that document - on the SVG canvas - is mapped onto a FINITE area of the page (we'll assume it's an HTML page), called the viewport, or SVG viewport. The size of this finite area is what you're setting when you do `<svg width="100px" height="100px">`.
      2. Continuing the analogy, the viewport is almost like a window that you're looking through to see your infinite piece of graph paper.
   3. viewBox
      1. The viewbox is an attribute of `<svg>` that accepts 4 values, in this order (which occurs quite a lot in web standards) `x y width height`. The default starting values for `x y` are `0 0`, (ie, the top left corner). 
      2. The viewBox allows you to specify a particular piece / section of your SVG canvas that will get mapped to the FINITE area of the SVG viewport
   4. viewport coordinate system & user coordinate system
      1. These are two coordinate systems, that give SVGs much of their flexibility, and allow them to scale without loss of quality
      2. **the user coordinate system is mapped to the viewport coordinate system**
   5. These [Sara Soueidan](https://www.sarasoueidan.com/blog/svg-coordinate-systems/) & [CSS Tricks](https://css-tricks.com/scale-svg/) articles are the best explanations I've seen of SVG positioning & scaling.
   6. [MDN SVG positions](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Positions) 
5. What shapes are available in SVG?
   1. [basic shapes](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Basic_Shapes), including squares, circles, stars, lines, polygons, polylines, etc...
   2. [paths](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Paths), from which you can create basically anything, including curves
6. How does the `<svg>` element interact with responsive design?
   1. The SVG will expand to its container if you remove the `width` & `height` attributes
   2. TODO: finish
7. What is `<g>`?
   1. This is a group, meant for grouping other objects. Analogous to a `div`, useful for removing redundency. 
8. What does `z` on the end of a `<path>` mean?
   1. It means the path closes back to the beginning point of the path
9. What's the main attribute you use in `<path>`?
    1.  `d=""`, which stands for drawing
10. What's the difference between the capital letters & lowercase letters in the `d` attribute of a `<path>` element?
    1.  lowercase letters are relative units, ie 5 units from the last position
    2.  uppercase letters are absolute units, ie go to this exact position
11. What's a decent start to making SVGs reasonably accessible?
    1.  Use `<svg aria-labelledby="">`, and include [`<title id="" lang="">` as the first element in the SVG](https://developer.mozilla.org/en-US/docs/Web/SVG/Element/title) to provide an short, accessible, text description.
    2.  Use `<svg role="presentation">`, to indicate that screen readers should not read out everything in the SVG DOM
    3.  [CSS-tricks](https://css-tricks.com/accessible-svgs/) & [Paciello Group report](https://developer.paciellogroup.com/blog/2013/12/using-aria-enhance-svg-accessibility/) on SVG a11y