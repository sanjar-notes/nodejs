# 161. Creating a User model
Created Sunday 16 April 2023 at 02:02 pm

Let's a new model, called User. A user can create products, and also buy products. Of course, a user will have their cart (i.e. "associated" cart). There are two parts to the User model
1. Base data- name and email.
2. Associations - the relations to cart, product etc.

We'll not worry about user authentication right now.

Let's work on the first part. [Code](https://github.com/exemplar-codes/online-shop-express-ejs-mvc/commit/83b849694089ad439d4a115d5227bc21fb4f30c4)