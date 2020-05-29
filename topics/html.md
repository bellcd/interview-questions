# HTML

1. Difference between HTML, CSS, & JavaScript
   1. HTML is a markup language, which describes WHAT (ie, the [meaning & structure](https://developer.mozilla.org/en-US/docs/Web/HTML)). It can provide granularity to your content, describing which particular tags go with which particular parts of your content.
   2. CSS handles presentation
   3. JavaScript handles functionality
2. Explain
   1. tags - does every element need a closing tag?
      1. tags are used in HTML documents to provide meaning & structure to different sections of content
      2. they consist of an opening `<` and closing `>` angle brackets, with the element name in between
         1. ie, `<img />`
      3. Most elements require opening and closing tags, a few do not
         1. ie, `<img />`, `<br />`
3. Is there anything wrong with using `<div>`s every time you need a container for something?
   1. Yes, `<div>`s do not inherently have any semantic meaning. One of the points of HTML is that the tags describe the purpose of the content they're wrapping. So an `<img>` represents an image, a `<button>` represents a button. HTML5 introduced many new tags, several of which allow us to provide semantic meaning to sections of a layout, including:
      1. `<header>`
      2. `<footer>`
      3. `<section>`
      4. `<article>`
      5. `<aside>`