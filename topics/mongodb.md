# MongoDB

1. What is MongoDB?
2. Explain:
   1. clustering
      1. TODO: finish
   2. embedded document. Is there an alternative?
      1. TODO: finish
2. Give an example of when you would want to encapsulate logic in a Mongoose Model
   1. Your model is of the users in your application, and you want to specify what properties of any given user get added to a JSON web token. This logic would best be situated inside the Mongoose Model, where it has access to those properties.