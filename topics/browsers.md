# Browsers

1. Explain:
   1. Document Object Model VS CSS Object Model VS Render Tree VS Critical Render Path
      1. TODO: finish
2. What's the difference between:
   1. AJAX & page requests?
       1. AJAX (XMLHttp) requests
          1. made by JavaScript, & only JavaScript
          2. sent to the server AFTER the page has loaded
          3. is a request for **data**
       2. page requests
          1. initiated by the browser (in whatever code the browser is written in, probably C++)
          2. THIS is the request for the initial page (or a new / updated / different page)
          3. is a request for a document (in some format, like HTML)
   2. web & internet?
      1. web
         1. series of documents using a markup language (like HTML)
         2. with hyperlinks linking them together
         3. and a browser to read those documents (screen readers are also browsers)
      2. internet
         1. many other protocols / networks, including:
            1. email servers
            2. FTP
            3. 90s style internet chat rooms (AOL / Yahoo Mail / etc...)
            4. SSH
   3. local storage & cookies
      1. TODO: finish this
   4. TCP & UDP
      1. TCP specifies that the client tell the server info about the message (ie, what / how many packets, etc...) it's sending, so the server can be assured it received all the packets of a message.
         1. **TCP is slower than UDP**
      2. UDP simply sends packets, without metadata about those packets. Use case is really games, where performance (especially of the system as a whole) is much more critical than dropping ceratin packets.
   5. Parser Blocking VS Render Blocking
      1. TODO: finish
3. Does a 2xx status code always mean the request was completely successful?
   1. 200-something status codes do indeed mean success, but not necessarily complete & utter success.
      1. 206 status means partial success (for example, perhaps 14 of your 15 database queries were successful)
4. Do subdomains have unique IP addresses?
   1. yes
5. Are `<style>` tags parser blocking or render blocking?
   1. **`<style>` tags are render blocking** because the engine doesn't - and can't - know what the CSS object model, and thus the render tree, will look like until ALL the css stylesheets have been downloaded & parsed.
   2. **`<style>` tags are NOT parser blocking** because the engine will continue to download & parse other files.
6. How many unique requests can be outstanding to a given IP address?
   1. 20
      1. for example, a page can simultaneously have 20 open requests each to:
         1. blog.fb.com
         2. fb.com
         3. www.fb.com
         4. etc...
7. Is there a general ordering for script & link tags in the head of an HTML document? Why? Any exceptions?
   1. TODO: finish
8. Describe the browser's general approach to parsing HTML
   1. TODO: finish
9. What happens when I enter my username & password into a form & hit login? Describe at as low a level as you can.
   1. Assuming we're sending the data as JSON & following best practices. The front end encodes the username & password into a JSON object, then sends them in the body of a POST request to the relevant api endpoint of the server.