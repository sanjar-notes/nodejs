# Adding 404 page
Created Wednesday 1 March 2023 at 10:56 pm

Use `res.sendFile()` inside the last "unfiltered" middleware. This middleware runs only if none of the other middlewares match.

Note: We can check `res.headersSent` to avoid double responses, but it's fine without it too, since `next()` is usually never called after response.