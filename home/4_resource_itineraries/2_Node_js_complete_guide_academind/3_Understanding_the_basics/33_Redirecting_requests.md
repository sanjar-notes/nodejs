# 33. Redirecting requests
Created Tuesday 14 February 2023 at 03:39 pm


## Situation (why we need redirects)
1. Temporary redirects during site maintenance or downtime
2. Permanent redirects to preserver existing links (especially bookmarks) to resources whose location has updated.
3. Enforce HTTPS by redirecting
4. Federated login. See [chatgpt-redirections-&-IDP-login](../../../../assets/chatgpt-redirections-and-IDP-login.pdf).


## About (history, spec)
- Read [Redirections in HTTP - MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Redirections)
- HTTP has a special kind of response (aka "HTTP redirect" or just "redirect") that cause the browser to load a new URL (contained in the "redirect" response).
- There are 3 ways to redirect a client (in order of priority):
	1. Server redirect. This should be preferred.
	2. HTML redirect - using the `<meta>` tag
	3. JavaScript redirect - set the URL on page load or some other condition.
- There are 3 types of redirections (with status codes):
	1. Permanent - 301. Others - 308
	2. Temporary - 302. Others - 303, 307
	3. Special - 304 (not modified - use local cache). Others - 300.


## How (to do a server redirect)
For HTTP (i.e. server redirect), do two things:
1. Set status code to a redirect friendly one (3xx).
2. Set "Location" header, with value as the location.

Example:
```js
(req, res) = {
	res.statusCode = 301;
	res.setHeade("Location", "/about"); // same domain
	res.setHeader("Location", "https://github.com"); // external domain
}
```
[Code example](https://github.com/exemplar-codes/nodejs-server-academind/commit/0418ad5b9b0c026c442178672050e1d6b0bf078b)