# 57. Module introduction
Created Sunday 19 February 2023 at 05:37 pm

## Situation
- Using the http module, fs module for reading/writing files, streams etc is OK. But it's inefficient (from a DX POV), and therefore impractical for making apps. Reasons:
	- Repetition of standard stuff - extracting the body of a request, creating JSON strings
	- Too fine grained
	- Too much code and scope of errors
	- No clear structure for files, functions - this need to be taught/communicated/maintained separately.
- More tangible reasons why this (vanilla Node.js server app) is impractical:
	- Routing
	- Handling status codes, response headers
	- Reacting differently based on request headers


## A solution
Express.js is a web app (server side) framework that solves many of the aforementioned problems and provides many utility functions.

- Express.js helps us focus more on the business, instead of the code.


## In this section
1. What is Express.js?
2. Using middlewares - an important feature of Express
3. Working with requests and responses, elegantly!
4. Routing - more structured, compared to explicit if-else blocks.
5. Returning files.