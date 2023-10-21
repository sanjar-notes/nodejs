# 233. Cookie code
Created Wednesday 9 August 2023 at 02:41 am

## Server
Requirements - *Needs the `cookie-parser` package installed and added as middleware.*

1. Create (set). There are two ways, both work without extra packages.
	1. `res.setHeader('set-cookie', 'cookieKey=cookieVal; confK=confV;')`
	2. `res.cookie('cookieName', 'cookieValue', config?)` [docs](https://expressjs.com/en/4x/api.html#res.cookie)
2. Read. Two ways to do it. Second one is parsed (but needs a package).
	1. `res.headers.cookie` - key value string, need to add parse logic.
	2. `res.cookies` object and `res.cookies['cookieName']`. *Needs the ['cookie-parser'](https://www.npmjs.com/package/cookie-parser) package installed and added as middleware.* [docs](https://expressjs.com/en/4x/api.html#req.cookies)
3. Update - same as set.
4. Delete - set with `max-age:0`
	1. `res.setHeader('set-cookie', 'cookieKey=cookieVal; max-age=0;')`
	2. `res.clearCookie('cookieName', config?)` [docs](https://expressjs.com/en/4x/api.html#res.clearCookie)

Note: 
- only reading cookies requires a package `cookie-parser`, writing `res.cookie` is supported by Express by default. Strange but ok.
- There's no one liner to delete all cookies. Loop through received cookies and call `res.clearCookie(key)` for each.


## In browser JS console
- Read/write is quite simple. Use `document.cookie`.
- But there's no parser, one needs to be cognizant of string logic.
- Cookies with config 'HttpOnly' cannot be edited by JS. They can still be edited manually (using browser UI - the Application tab in DevTools).
```js
document.cookies = 'key1=value1; key2=value2;'
```

## Trying out the code
1. Set simple cookies (no config and check if they're set or not).
