# HTML

1. Difference between HTML, CSS, & JavaScript
   1. HTML is a markup language, which describes WHAT (ie, the [meaning & structure](https://developer.mozilla.org/en-US/docs/Web/HTML)). It can provide granularity to your content, describing which particular tags go with which particular parts of your content.
   2. CSS handles presentation
   3. JavaScript handles functionality
2. Explain
   1. elements
      1. HTML elements consist of an opening tag, the content, & a closing tag (most of the time)
   2. tags - does every element need a closing tag?
      1. tags consist of an opening `<` and closing `>` angle brackets, with the element name in between
         1. ie, `<img />`
      2. Most elements require opening and closing tags, a few do not
         1. ie, `<img />`, `<br />`
   3. attributes
      1. These add additional information about the element. Common ones include class, id, <input>s can have type, etc...
         1. where do attributes go?
            1. only in the opening / self-closing tags, not in closing tags
3. Is there anything wrong with using `<div>`s every time you need a container for something?
   1. Yes, `<div>`s do not inherently have any semantic meaning. One of the points of HTML is that the tags describe the purpose of the content they're wrapping. So an `<img>` represents an image, a `<button>` represents a button. HTML5 introduced many new tags, several of which allow us to provide semantic meaning to sections of a layout, including:
      1. `<header>`
      2. `<footer>`
      3. `<section>`
      4. `<article>`
      5. `<aside>`
4. Does whitespace matter in HTML?
   1. [HTML largely ignores whitespace, but not completely.](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Whitespace) Empty text nodes (representing the white space in your HTML document) DO indeed show up in the DOM in between other nodes.
   2. This enables more flexibility in formatting HTML documents
5. Describe how you can use the `<form>` element to submit data to some URL without any extra JavaScript
   1. `<form>` has two attributes that will be important here, [action & method](https://developer.mozilla.org/en-US/docs/Learn/Forms/Your_first_form)
      1. action is the URL where the form data will go
      2. method is the type of request (HTTP method) the browser will send to that URL
      3. You also need a `<button type="submit">` element - clicking this will send the form's data to the action URL
6. What's the general structure of an HTML document, and what is the purpose of each section (each tag)?
   ```html
   <!DOCTYPE html>
   <html>
      <head></head>
      <body></body>
   </html>
   ```
   1. `<!DOCTYPE html>` - tells the browser to expect an HTML document & what version
   2. `<html>` - all your HTML markup has to be inside this tag
   3. `<head>` - this is content for the browser to use, not directly visible on the page. `<title>`, `<meta>`, `<link>`, & `<script>` tags all go here (some can go elsewhere)
   4. `<body>` - this is all the content that's displayed in the browser
7. When would you use a `<div>` VS a `<span>`?
   1. `<div>` is a block level element, while `<span>` is an in-line element. So a `<div>` is going to require all the horizontal space (in left-to-right languages) for that line, while a `<span>` would sit next to any additional content that comes before or after it if there is room on that line.
   2. Because of this, `<span>`s are typically used to group smaller amounts of text within a line, while `<div>`s are used for larger groupings and layout.
8. Describe the basics of setting up a form on a webpage
   1. TODO: finish