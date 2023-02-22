# 64. Parsing Incoming Requests
Created Wednesday 22 February 2023 at 11:01 pm

## Situation
In `node:http`, the request data is available as a stream that can be piped, listened to. This is not very helpful as most app server typically deal with small and almost scalar data (i.e. objects of a fixed and low size).

Express provides some constructs to deal with these "scalar" values easily. Of course, very granular control is still possible since Express mostly uses (and exposes API of) `http` under the hood.

Let's make a simple form, i.e. we'll be receiving HTML form data.