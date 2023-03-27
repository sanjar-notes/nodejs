# 25. How the Web works
Created Monday 13 February 2023 at 12:25 pm

## Request-Response model of the web
The communication model used by the Internet is a request-response model based on HTTP (Hyper Text Transfer Protocol). Details:
- The flow is simple:
	1. Machine A send a request to some IP address.
	2. Machine B (with the IP address in \#1) sends back a "response".
- Machine A is called the client and Machine B is called the server. These terms are relative and may be temporary.
- The request is usually sent using a browser, but it could be sent otherwise too.
- The response is definitely not sent using a browser, since a browser cannot respond.
- Derived: Server to server communication is also possible via this request-response model. By server to server, I mean no browsers are involved.

![](/assets/25_How_the_Web_works-image-1.png)


## About HTTP and HTTPS
- HTTP is the protocol used to specify the format and general flow of request and responses.
- HTTPS is the same as HTTP, except with encryption (SSL) turned on. All data between the client and server is now encrypted.
- We'll use HTTP for all projects in this course, since our will be running locally. We'll learn how to turn on SSL (for HTTPS), at the end of the course when learning about deployment.
- HTTPS is a minimum requirement on the Internet today. Using HTTP for real apps is strongly discouraged.
