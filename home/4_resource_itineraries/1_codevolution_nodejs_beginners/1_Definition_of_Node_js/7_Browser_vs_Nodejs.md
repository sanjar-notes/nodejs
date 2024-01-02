# Browser vs Node.js
Created Monday 23 January 2023 at 02:26 am

## Available APIs
1. The browser is a platform to consume sites, whereas the other is a general purpose runtime. **Result**: browser gives us access to DOM API, Cookies, Storage API and other web platform APIs. Node.js is not a site consumption runtime, so it doesn't provide these APIs.
2. The Browser has tight security, so much so that one cannot interact with the file system - except downloading/uploading and some internal housekeeping the browser does. **Result**: the browser does not provide us access to filesystem modules, or other OS utilities, but Node.js does.
   

## Choosing JavaScript versions
With Node.js, we specify/control the code execution environment (including the JS engine).
So we can use all the new JavaScript versions like ES2015 or later, and also any custom features we define.

In the browser, we are at the mercy of users and browser vendors when it comes to running JavaScript. Reason being that we can execute only selected versions of JavaScript that the browser vendor has implemented for that browser. And users choose the browsers.


In the subsequent sections, we'll focus on the features of Node.js one at a time.