Writing a chat application with popular web applications stacks like LAMP (PHP) has normally been very hard. It involves polling the server for changes, keeping track of timestamps, and it’s a lot slower than it should be.

Sockets have traditionally been the solution around which most real-time chat systems are architected, providing a bi-directional communication channel between a client and a server.

This means that the server can push messages to clients. Whenever you write a chat message, the idea is that the server will get it and push it to all other connected clients.

The web framework
The first goal is to set up a simple HTML webpage that serves out a form and a list of messages. We’re going to use the Node.JS web framework express to this end. Make sure Node.JS is installed.

First let’s create a package.json manifest file that describes our project. I recommend you place it in a dedicated empty directory (I’ll call mine chat-example).

{
  "name": "socket-chat-example",
  "version": "0.0.1",
  "description": "my first socket.io app",
  "dependencies": {}
}
CAUTION
The "name" property must be unique, you cannot use a value like "socket.io" or "express", because npm will complain when installing the dependency.

Now, in order to easily populate the dependencies property with the things we need, we’ll use npm install:

npm install express@4
Once it's installed we can create an index.js file that will set up our application.

const express = require('express');
const app = express();
const http = require('http');
const server = http.createServer(app);

app.get('/', (req, res) => {
  res.send('<h1>Hello world</h1>');
});

server.listen(3000, () => {
  console.log('listening on *:3000');
});
This means that:

Express initializes app to be a function handler that you can supply to an HTTP server (as seen in line 4).
We define a route handler / that gets called when we hit our website home.
We make the http server listen on port 3000.
If you run node index.js you should see the following:

