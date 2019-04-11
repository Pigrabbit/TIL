# What is Express?

Express is a powerful but flexible Javascript framework for creating web servers and APIs. 
It can be used for everything from simple static file servers to JSON APIs to full production servers.

## Starting a server

Express is a Node module, so in order to use it, we will need to import it into our program file. 
To create a server, the imported express function must be invoked.

``` javascript
// Import the express library
const express = require('express');
// Instantiate the application
const app = express();
```

The purpose of a server is to listen for requests, perform whatever action is required to satisfy the request, and then return a response. 
In order for our server to start responding, we have to tell the server where to listen for new requests by providing a port number argument to a method called app.listen().
The server will the listen on the specified port and respond to any requests that come into it.

``` javascript
const PORT = 80;
app.listen(PORT, () => {
  console.log(`Server is listening on port ${PORT}`);
});
```

On the code above, it will log `Server is listening on port 80` once the server is started.

## Writing Route

To tell our server how to deal with any given request, we register a series of routes. 
Routes define the control flow for requests based on the request’s path and HTTP verb.

For example, if your server receives a GET request at ‘/monsters’, we will use a route to define the appropriate functionality for that HTTP verb (GET) and path (/monsters).

1. GET
GET requests are used for retrieving resources from a server. 
Express uses `.get()` to register routes to match GET requests.
It allows two arguments, a path and a callback function to handle the request and send a response.

2. PUT
PUT requests are used for updating existing resources. 
We need to include a unique identifier as a route parameter to determine which specific resource to update.

**Using Queries**

PUT requests need information about how to update the specified data.
Query strings appear at the end of the path in URLs, and they are indicated with a question mark`?`.
Query Strings do not count as part of the route path.
Instead, Express server parses them into an object and attaches it to the request body as `req.query`.

3. POST

POST requests are used for creating new resources.
Since it create new data, their path do not end with a route parameter, but instead end with the type of resources to be created.
Express uses `.post()` as its method for POST requests. 
The HTTP status code for a newly-created resource is 201 Created.

4. DELETE

DELETE requests are used for deleting existing resources.
Since it delete currently existing data, their paths should usually end with a route parameter to indicate which resource to delete.
Express uses `.delete()` as its method for DELETE requests.
Servers often send a 204 No Content status code if deletion occurs without error.

## Sending a response

HTTP follows a one request-one response cycle. 
Each client expects exactly one response per request, and each server should only send a single response back to the client per request.

Express servers send responses using `.send()` method on the response object.
It will take any input and include it in the response body.

## Setting Status Codes

Express allows us to set the status code on responses before they are sent. 
Response codes provide information to clients about how their requests were handled. 

`res` object has a `.status()` method to allow us to set the status code.

```javascript
const sweetInventory = { Sneakers: 4, Haribo: 1, Kisses: 3, Reese: 2 };
app.get('/sweet-inventory/:name', (req, res, next) => {
  const sweetInventory = sweetInventory[req.params.name];
  if (sweetInventory) {
    res.send(sweetInventory);
  } else {
    res.status(404).send('Sweet not found');
  }
});
```

vim editor에서 한글로 쓰기란...후
