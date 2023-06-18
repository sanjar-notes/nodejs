# 79. Sharing Data across Requests and Users

[Initial code](https://github.com/exemplar-codes/templating-engines-w-express-js/commit/591b2acf09cb6d83fd434e20bc367f65136e5463)

## Storing data between requests, and users
Let's store (ingest) data inside JavaScript variables themselves, i.e. data is available in RAM, until the server is stopped.

This "temporary" storage can easily be used by other routers, files, by exporting the storage variable, and since the storage variable (array or object) is a reference type, it's no duplicated/reset when imported/used by other parts of the server.

So, data is persisted across requests, assuming the server keeps running.
   
Doubt: we'll not get circular dependency issues here, since the exporting file is run once and cached, by default in Node.js.


## This is not good (in general)
This kind of storage is:
1. Not secure - atleast for our implementation here, since every user can read/write all data.
2. Very unreliable - servers auto-restart if an error occurs, code is updated, power goes out etc
3. Very inefficient - RAM is for immediate working memory
4. Difficult to manage, track

This is very unrealistic so will almost never be used in a backend app.

Note: we can and will share data across requests, but not across users, in this module. This would still be unrealistic for a backend app, however.

## But, good enough for learning
But, for this module, we'll use this method to explore use of templating engines, without the overhead of database code.