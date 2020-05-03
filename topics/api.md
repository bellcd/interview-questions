# API

1. Explain:
   1. What is an API?
      1. An Application Programming Interface, an API, in general is the contract between an application and something else it needs to talk to. For APIs on the web specifically, that generally means the contract between a web client & web server.
      2. A neat comparison is that APIs are a bit similar to function signatures
      3. On the web, an API will have:
         1. endpoints - the path part of the URL.
   2. What is REST?
      1. Representational State Transfer - REST - is a pattern, that came about to try to bring some standardization to how APIs would be set up
         1. The server will transfer to the client a representation of the state of the requested resource
         2. That pattern sets down 6 constraints about the how the API - the contract - behaves
            1. Uniform interface
               1. includes resource locator
               2. includes enough information so the client can modify the resource
               3. Each request includes all the info the server needs to perform the request, & reach response contains all the info the client needs to understand the response.
               4. Hypermedia as the engine of app state
                  1. Most web pages adhere to his, but most web APIs do not
            2. Client Server separation
            3. Stateless
            4. Layered system
            5. Cacheable
            6. Code-on-demand (optional)
      2. Commonly, this involves sending an HTTP request (ie, with an HTTP method) to a particular endpoint specified by the server
      3. The REST pattern is designed to imitate a file structure
      4. [More Details](https://medium.com/extend/what-is-rest-a-simple-explanation-for-beginners-part-1-introduction-b4a072f8740f)
2. Give an example of when you would want to encapsulate logic in a Mongoose Model
   1. Your model is of the users in your application, and you want to specify what properties of any given user get added to a JSON web token. This logic would best be situated inside the Mongoose Model, where it has access to those properties.