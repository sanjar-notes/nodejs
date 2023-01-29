# 30. HTTP module
Created Sunday 29 January 2023 at 10:34 pm

// FIXME: rough 
Let's understand how the web works.

- Computers connected to the internet are called clients and servers (they can be both at the same time too).
- Clients have web accessing software available on them, the most common one being the browser. Example - laptops, phones, game consoles etc.
- Servers are computers that store web pages, sites, media and run applications.
- Client-Server model - the client sends a "request" to the server, and the server sends back a "response " containing a web page, media or just text responses.

Q: What is the format for the request, response? Also, what about other rules like failure, retries etc.
A: The HTTP (Hyper Text Transfer Protocol) defines the format and other rules.

Q: HTTP and Node
A: We can create a web server using Node.js. Node.js has access to OS level functionality like networking. Also, since Node.js has an asynchronous (and therefore non-blocking) nature, it is perfect for handling large volumes of requests.

Of course, the Node server we create should still respect the HTTP format.

The `http` module is used for creating web-servers that can transfer data over HTTP. In addition to creating servers (i.e. responding to requests), it also has functionality to make requests.