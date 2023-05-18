## Relations in NoSQL (MongoDB)
Created Friday 19 May 2023 at 12:50 am

- Partial duplication is allowed, here. This means we store and fetch the data is almost exactly the form our app needs and don't need to do joins at request time. This makes reads/writes very fast.
- Even though duplication is allowed, and is popular, MongoDB does provide ways to have relations:
	1. Nested/embedded documents - preferable if scope of duplication is low
	2. References - preferable if scope of duplication is high