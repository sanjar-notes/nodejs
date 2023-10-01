# 233. Cookie code
Created Wednesday 9 August 2023 at 02:41 am

1. Create (set) - both work with express (without package)
	1. `res.setHeader('set-cookie', 'cookieKey=cookieVal; confK=confV;')`
	2. `res.cookie('cookieName', 'cookieValue' | Object)`
2. Read
	1. `res.headers.cookie` - key value string, need to add parse logic.
	2. `res.cookies` object and `res.cookies['cookieName']`. *Needs the 'cookie-parser' package installed and added as middleware.*
3. Update - same as set.
4. Delete - set with `max-age:0`
	1. `res.setHeader('set-cookie', 'cookieKey=cookieVal; max-age=0;')`
	2. `res.clearCookie('cookieName')`

Note: only reading requires a package `cookie-parser`, other functionality is supported by Express by default.