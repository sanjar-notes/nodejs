# 67. Requests
Created Wednesday 22 February 2023 at 11:01 pm

[Code - demo and experiments](https://github.com/exemplar-codes/express-app-academind/commit/b28b5db7ae4e71a73524d82c1803d0d892718a96)

## Situation
In `node:http`, the request data is available as a stream that can be piped, listened to. This is not very helpful as most app server typically deal with small and almost scalar data (i.e. objects of a fixed and low size).

Express provides some constructs to deal with these "scalar" values easily. Of course, very granular control is still possible since Express mostly uses (and exposes API of) `http` under the hood.

## 1. Method
`req.method`

## 2. Path
- `req.originalUrl` - original request URL. Stays the same in routers too.
- `req.baseUrl` - URL for routers, middlewares i.e. value after prefix trimming has been applied.
- `req.url` - inherited from `node:http` module. Can be edited for internal routing. Not used very often.

### 2.1 Query string params (i.e. ?q=)
- `req.query` - an object constructed from query string, with query string keys as keys.
- Supports complex query strings too - duplicate keys, arrays, nested objects (atleast since Node v16).
	- Duplicate keys are are made into arrays. `?name=Sanjar&name=Nemo` will become `name: ['Sanjar', 'Nemo']`.
	- Both direct and explicit array notations are supported, i.e. `?name=Sanjar&name=Nemo` and `?name[]=Sanjar&name[]=Nemo` are equivalent.

Note: For convenience functions, use `qs`, a 3rd party module.

### 2.2 Path params (i.e. `/:name`)
`req.params` - object containing path params. Default value is `{}`.

Example: definition `user/:name` with instance `/user/23` will result in `{name: "23"}`.

Note: supports regex and capture groups, if they're used for param definition.

## 3. Headers
- `req.get(headerKey)` - returns header value.
- `req.headers` property - object containing all headers.
- `req.is(contentTypeValue)` returns argument (`string`) as is if match, else returns `false`. Returns `null` if there's no body. Example - `req.is("application/json")`, `req.is("urlencoded")`. Accepts partial input too.
- `req.accepts(acceptHeaderValue)` returns bool. Example - `req.accepts("application/json")`. Accepts partial input too.

Note:
- `req.header()` is an alias of `req.get()`
- `req.get()` is case insensitive.
- The `Referrer` and `Referer` header fields are treated as the same.

## 4. Body
- `req.body` property - request's body. Is `undefined` by default. Some interpretation input is needed before use.
- The interpretation input is usually done by built-in middlewares. Common ones:
	- `express.text()` - text
	- `express.json()` - JSON
	- `express.raw()` - raw binary data
	- `express.urlencoded` - for form data. Query strings don't need this, they're `urlencoded` by default. FIXME: `extended` is for query params, but `urlencoded` is not needed anymore, why is there still a a warning if this is omitted - `express.urlencoded({ extended: false })`. Should I keep it as false, since it's not needed anymore.
- `req.body` is a readable stream and is pipable, whenever this is applicable.

```js
app.use(express.json());

app.post('/', (req, res, next) => {
	req.body; // is an object
});
```

## 5. HTTP version
- `req.httpVersion` - a string. Example `"1.1"`. Is mostly enough.
- `req.httpVersionMajor` - a number. Example - `1` for `"1.1"`
- `req.httpVersionMinor` - a number. Example - `2` for `"1.2"`


## Convenience properties and functions
1. `req.is(contentTypeValue)`- Get `"Content-Type"` of the request.
	- Argument - `String`. Accepts partial arguments too, `req.is("json")` will return `"application/json"`.
	- Returns a `String`. Returns false if type is absent. Returns `null` if there's no body.
2. `req.cookies` property - cookies as an object
3. `req.route` returns skeleton of the path as is. Useful is path params are used.
4. `req.secure` - returns a boolean if HTTPS is being used.

## Extras
1. `req.ip` - IP address of the request client. Assumes trust proxy setting is not false.
2. `req.subdomain` - array of subdomains (in ancestor order, of course). Note - default offset is 2, i.e. ignores the last two. Example - `"tobi.ferrets.example.com"` will result in `['ferrets', 'tobi']`
3. `req.xhr` property - boolean. `true` if request made using `XMLHttpRequest` or `fetch`. **Not useful**, unless the `X-Requested-With` header has a value of `XMLHttpRequest`.