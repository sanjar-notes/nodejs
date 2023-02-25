# 32. Routing requests
Created Tuesday 14 February 2023 at 01:09 am

## Why
The USP of the internet is the hyperlink. Routing is backend feature that makes this possible.


## What
- Routing generally refers to the act responding differently for different request URLs.
- In the modern web however, routing is a general term for responding to requests based on metadata of the request - URL, locale, authentication, authorization etc.


## How (app implementation)
- Fundamentally, routing is done by a switch (or if else) of criteria and associated and action/response.
- It can get complex, since criteria can be based on nested routes, query strings, other request metadata or a combination of these.

Examples
- [Based on route](https://github.com/exemplar-codes/nodejs-server-academind/commit/eb4e6ef075fe3f401075c28c1c09f152682df67d)
- [Based on route and HTTP method](https://github.com/exemplar-codes/nodejs-server-academind/commit/e1e0ef52406ae8d6ab943f2e514e2eb33c2380eb)