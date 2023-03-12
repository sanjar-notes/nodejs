# 97. What is MVC
Created Sunday 12 March 2023 at 05:44 pm

/rough-in the sense that I don't want to spend time on exact definition of MVC

- MVC (Model-View-Controller) is a way to organize (logical) server side code.
- MVC is a way to achieve separation of concerns.

MVC parts:
1. Views - usually HTML templates. But in general, this is code responsible for generating the responses (what the users see). It is decoupled from both data and the business logic.
2. Models - code representing and managing data, e.g. saving data, fetching data, querying data. Since saving data is a responsibility of Models, they also contain the business logic.
3. Controllers - code that glues together functionality of Models and Views. In fact, it is the controller that handles (and is aware) of the HTTP request (since both Model and Views are oblivious to the request or it's params).
Note: generally, there's something called 'Router' that runs first (in the request cycle) and triggers the relevant controller to be called (passing along request params, of course).

---
MVC in an Express app
Since the primary (and only) construct of Express is the middleware, controllers are split across middlewares.