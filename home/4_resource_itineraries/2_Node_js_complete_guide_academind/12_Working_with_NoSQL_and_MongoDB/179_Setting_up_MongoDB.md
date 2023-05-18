# Setting up MongoDB
Created Friday 19 May 2023 at 01:10 am

## Installing MongoDB (the database)
- We can install MongoDB locally.
- However, we'll use a cloud environment - from the official MongoDB website. This will be helpful if we wish to deploy our app. MongoDB has a good enough free tier, this is sufficient for the course.


## Cloud setup
- Sign in
- Create a user, and a cluster. Make sure the user has both read and write permissions.
- Check IP whitelist etc, and add your PC's IP address. We'll need to do this for exploring MongoDB in our Node.js apps locally.


## Local (project) setup
- Install the mongoDB driver, by running `npm install mongodb`