# Accessibility (A11y)

1. What are aria labels & why are they used?
2. Is there a "source-of-truth" for accessibillity in web development? If so, what is it?
   1. [Perhaps, there's a guiding document called with WCAG 2.0 AA](https://www.w3.org/TR/WCAG20/)
      1. [In courts in the US, ADA compliance for websites has generally meant that you meet the 38 succeess criteria outlined in WCAG 2.0 AA](https://medium.com/@krisrivenburgh/the-ada-checklist-website-compliance-guidelines-for-2019-in-plain-english-123c1d58fad9)
3. Why should web developers code for accessibility?
   1. better SEO
   2. displays good morals as a company, so better public image
   3. many accessibility practices will also make your site faster, soyou should be doing them anyway
   4. in many countries, it's the law (ADA in the US)
4. Who are the traditional target populations for accessibility?
   1. visual
   2. auditory
   3. motor
   4. cognitive
5. Does coding for accessibility take longer than coding while ignoring it?
   1. not necessarily
      1. if you're refactoring already written code for accessibility, then yes, it might add developer hours. If you're merging accessibility into the workflow, then any added developer time is likely negligible
      2. It's arguably easier to develop with, because it forces best practices, and so the code that's produced will be more performant
6. List some accessibility best practices related to HTML
   1. What is POSH?
      1. "Plain Old Semantic HTML", ie, using tags for what they're meant for
         1. NOT everything-is-a-div web apps, `<main>` / `<header>` / `<footer>` / `<section>` / `<article>` / `<aside>` / etc...
   2. `<button>` for interactivity, if at all possible
      1. because `<button>`s can be tabbed into for focus, and engaged with enter/return, by default
   3. Always use meaningful `<label>`s with `<input>`s
   4. `<img>` tags with alt & title attributes, OR aria-
   5. useful text descriptions in links
      1. ie, `<a href="..."><p>Learn more about corgis here</p></a>`
      2. NOT `<p>Learn more about corgis <a href="...">here</a></p>`
   6. use skip links
   7. Links to non-HTML resources
   8. Links that open a new tab or window should be marked as such
   9. be careful about messing with default link styling, consider contrast guidelines
   10. `<th>`s & `<caption>`s with `<table>`s
7. List some accessibility best practices related to CSS
    1. sufficient proximity between clickable elements (ie, touch targets should be at least 48 x 48px)
    2. match user expectations & conventions
        1. ie, don't make _____ not look like a _____ (with headers, emphasized text, abbreviations, links)
    3. Tables - headers, zebra striping help
    4. color contrast is compliant with WACG 2.0 AA
        1. tools like [https://webaim.org/resources/contrastchecker/](https://webaim.org/resources/contrastchecker/)
    5. Hiding things
        1. Exercise caution using:
           1. `visibility: hidden`
           2. `display: none`
    1. Accept that users can override styles
        1. ie, zooming the text to 200% shouldn't break the layout (use scrollbars)
8. List some accessibility best practices related to JavaScript
   1. Keep JavaScript unobtrusive
      1. ie, there should some version of the site accessible to a screen-reader, only using a keyboard
   2. Mouse-specific events (mousover, mouseout, etc...)
      1. include additional triggers for the event handlers - onfocus / onblur
9. Explain WAI-ARIA
   1. Adds additional semantics for screen readers through HTML attributes. There are four (4) main areas where this is useful.
       1. signposts / landmarks via roll
           1. ie, to replace / extend HTML semantics
       2. dynamic content updates via aria-live
           1. ie, AJAX requests
       3. enhancing keyboard accessibility
           1. using tabindex
       4. accessibility of non-semantic controls
           1. ie, complex UI features
   2. Some might say it's possible to go overboard with WAI-ARIA ... aim for balance