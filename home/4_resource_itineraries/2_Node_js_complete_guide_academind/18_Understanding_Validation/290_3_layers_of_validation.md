# 290. 3 layers of validation
Created Tuesday 15 August 2023

## The 3 layers overview
Validation can be done at multiple layers of an app - the intent and effect varies. The layers are:
1. Client side - purely a UX thing, isn't technically data validation.
2. Server side - this is the ideal place for validation, in most apps.
3. Database level - schema validations of the database being used.

- client side validation is recommended but optional
- atleast one of server side or database level is mandatory. 
- prefer server side.

## 1. Client-side validation
This is just a UX thing.

Client side (browser side) validation can be implemented in various ways:
1. `input.type` HTML attribute
2. Custom JavaScript - with or without an application lib like React/Vue.
   
It isn't data validation, technically, since the client can make API calls directly without a browser, or change the frontend code as per their needs (since HTML, CSS and JS are directly accessible - if not readable).
Or they could just use a API client like Postman to mock the request.

Client side validation is recommended to be there, but isn't enough. Of course, it is not mandatory (if dev resources are low).


## 2. Server-side validation
By server-side validation, I mean the request handler code - an Express, Rails, Django app. I don't mean the database.

This is thought to be the ideal place for validation, for most apps. Some reasons for it:
1. Database may be changed, without changing the server app logic
2. Easy to respond with messages, files etc.
3. Easy to do non-trivial validation - like validation that's based on external entities (e.g an external API) or a different part of the app - a database or message-queue etc.


## 3. Database level validation
By database level, I mean the validations allowed by the db engine - usually done via Schemas (e.g. Sequelize models, Mongoose schemas and models).

This is not preferred if the database may be changed in the future.
It is OK to do this if the app is small and requirements shall stay stable in the future.

It's not recommended. It's not required (assuming there's server side validation).


---

In this course, we'll focus on server-side validations only.