# Security

1. What happens when the username & password reach the server? How does the server verify if the password is correct?
   - The server has to be on & listening at the correct api endpoint & port, and have code set up to handle the type of incoming request - POST, in our case. The server code then reads the body of the POST request, parses the JSON, and continues processing the request with other server code.
   - For your password to be sercurely stored in the company's database (to a reasonable degree) the actual thing - the text - that the company stores in their database is NOT your password, as you remember it.
     - For example, when you enter your email awesomeMegan@gmail.com & password @myFluffyDog42 into the login form and submit them, those bits of text eventually arrive on the web server. There, the server code will ask the database for the stored password it has for awesomeMegan@gmail.com. Assuming you've registered before, the database will send the stored password it has back to the server code. Now the server code can compare the password you typed in - @myFluffyDog42 - with what it received from the database, something like 0E6A48F765D0FFFFF6247FA80D748E615F91DD0C7431E4D9. They're different because what's stored in the database is something called a hashed password. Hashing is a ONE-WAY operation, in that it takes your input string - @myFluffyDog42 - runs it through a function (called a hashing function), and outputs something - in this case the string 0E6A48F765D0FFFFF6247FA80D748E615F91DD0C7431E4D9. This works for passwords / security because hashing functions:
       - Always return the same output for the same input
       - It's not possible to go backwards (ie, take a hash and create the plain text password), even if you know the details of the particular hashing function used.
       - Every input maps to one output (not technically true at the margins, but for all practicality)
     - Some company systems also use a salt
   - So the server code runs your password - @myFluffyDog42 - (combined with your salt from the database, if they use them) through their hashing function, and compares the hashed password that was just generated with the hashed password retrieved from the database. If they match, the user is then authenticated.
2. How can a user stay logged in, so they don't need to & password?
   - The web app / website can set a cookie on the end user's web browser. Cookies are:
     - small pieces of data
     - in key:value format
     - domain specific
     - sent with every request
   - So, for example, when you sucessfully login to a website / web app, they could generate & save a unique string on your browser as a cookie. Then, later, when that same browser visits the webpage, the cookie gets sent to the web server, (which has code set up to recognize the unique string that it set earlier). This uniquely identifies you to the server, and so it may not ask you to log in again.
3. Can the company retrieve your password for you?
   - Not if they're following security best practices
   - Because hashing is a ONE-WAY transformation, and the company only stores your hashed password, it is NOT possible for the company to send you your password. The best they can do is validate that it is in fact you, then offer to rest your password.
4. What is SQL injection? How do you prevent it?
   - When a web page or web app executes user input directly in an SQL query
   - Don't directly execute uer input. ie, every piece of user input needs to pass input validation before that user input even gets to the part of your system that interacts with the database.
5. Architect a scaled down Facebook app, with a feed display, and a posts display, many users, many posts. FOLLOWUP: How do you make it so anyone can get to it?
6. When you have lots of traffic and the website is slow, how do you determine where the bottleneck is, and how would you fix it? FOLLOWUP: If the bottleneck if the server, how would you fix it?
7. How do you securely transmit data?
8. How do you get your React / Angular / Vue / etc... app onto the server?
9. Tell me about a time you missed a deadline, what happened, and how did you fix it?
10. Tell me about a time you've worked harder than you should've, and why you did it?
11. What browser do you use to develop and why?
    1. Chrome, dev tools features
12. Explain
    1. JSON Web Tokens
       1. JSON objects encoded as a string
       2. specifies a secure approach for two parties to make claims (ie, the client claiming this person is already logged in, and they have role: user), and verify that those claims are accurate
       3. [details](https://jwt.io/)
    2. Hashing
       1. ONE WAY operation that changes something (ie, your plain text password) into something else (ie, a hashed password). Even if you know the particular hashing algorithm used & the hashed value, you cannot recover the original value.
    3. Salt
       1. A random string (some common ones are combinations of date, IP address, type of web browser, etc...), and combine that with your user supplied password, to create the hashed password. This approach is more secure because then you need something the end user has (password) + something the company has (salt) to generate the correct hashed password.
13. What's the difference between?
    1. Authentication VS Authorization
       1. Authentication is the process of verifying that a given user is who they say they are. ie, signing in to a system with a username and password is authentication
       2. Authorization is the decision making process that determines whether a given user should be able to perform a particular operation. ie, once you're signed in, should you be able to modify a particular resource?
    2. 401 VS 403 error codes
       1. 401 is an Authentication error - ie, "I don't know who you are yet" - so please try again
       2. 403 is an Authorization error - ie, "You're not allowed here"
       3. [details](https://stackoverflow.com/questions/3297048/403-forbidden-vs-401-unauthorized-http-responses)
14. Where is an appropriate place to store secrets (ie, private keys) about your application?
    1. environment variables
    2. Secrets like this should NEVER be included in the codebase (and should be excluded from source control, like git / github)
15. Should authorization be implemented on every route in your API? why / not? how?
    1. no - certain routes might be public by design
    2. setting up the authorization as middleware
16. Can you safely store JSON Web Tokens in a database? how?
    1. TODO: finish