# 29. Understanding Requests
Created Monday 13 February 2023 at 10:02 pm

The request param in `http`'s server callback contains a lot of data and functions - HTTP headers, browser ("user-agent"), acceptable mime types, etc.

Some important ones are:
- `url` - requested URL (with domain and string before it removed). A request for `example.com` will have the `url` /.
- `method` - HTTP verb. Example - GET, PUT, POST, DELETE, HEAD etc.