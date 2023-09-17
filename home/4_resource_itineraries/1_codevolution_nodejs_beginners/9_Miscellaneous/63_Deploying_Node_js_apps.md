# 63. Deploying Node.js apps
Created Monday 13 February 2023 at 03:19 am

Let's learn how to deploy Node.js app.

Heroku used to be a good choice, but it's not free anymore. We'll be using [Render](render.com) here. There are many other platforms and ways to deploy a Node.js app - [Fly](fly.io), [AWS](aws.com) (some manual work needed).

Steps for render.com:
- Step 1: Let's write some code that we'll deploy. Make sure it's inside a GitHub repo [Code](https://github.com/exemplar-codes/codevolution-nodejs/commit/2d1581c0310e981473276bf18c1cec2c0e460544) and has a `package.json` file (even if no packages are used).
- Step 2: Signup, login to Render.
- Step 3: Create a new "Web Service" and connect the GitHub repository containing the app code.
- Step 4: Fill out details. Defaults are fine. In our case, we'll need to set the branch, build command to `npm install` and start command to `node index.js`. Let the free plan be.
- Step 5: Environment (very important), add this by clicking "Advanced":
	1. Variables (add `PORT` to be anything, but read it inside app.js)
	2. Files:
		1. `.env`
		2. `.npmrc`
- Step 6: Leave everything else as is.
- Step 7: Click create web service. Done.

The deployment takes a few minutes.

Notes:
- Render.com supports `pnpm` natively, use it.
- Render.com [does not](https://feedback.render.com/features/p/module-workspace-syntax-causes-error) accept module workspace notation in imports, i.e. use `require("http")` instead of `require("node:http")`.
- Pushing to the branch will automatically trigger a re-deployment.
	- Manual deployment URL (should be kept private) is available. This can be used as an npm script (accessing .env). [Code](https://github.com/exemplar-codes/posts-express-api-app/commit/1edb7b79d3a3e17a974e3b0389c6fa3594da2243)