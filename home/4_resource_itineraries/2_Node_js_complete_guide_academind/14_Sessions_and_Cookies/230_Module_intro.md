# Module intro
Created Sunday 25 June 2023 at 07:57 pm

[height.app task link](https://height.app/OitGt6StRG/T-61)

We have looked at databases, which are stored on secondary storage for long term storage on the server.

Now, let's look at other important storage constructs - in the context of web apps.

We'll look at 3 things in this section:
1. What are Cookies?
2. What are Sessions?
3. Using Session and Cookies

https://github.com/sanjar-notes/backend/blob/d7878820f76ec345fdfd5aa0ff69b5f5f0305516/home/4_resource_itineraries/2_Cookies_Hussein_Nasser/1_HTTP_Cookies_Crash_Course.md - all about cookies.


Know that Cookies and sessions are unrelated principally, but they are used in conjunction.


---

note: I'm not trying to give a hard definition.

Suppose we have a web app which has user authentication (simple log in). The expected requirements of such an app include:
1. User shouldn't have to sign in each time they visit the app
2. User should be able to see that they are logged in or not.
3. User should be logged out after a certain event - generally a timeout. By "logged out", I mean requests fail and redirects to the login page.


## Cookie
1. Cookies are browser level storage that can be controllable by servers (i.e. the website).
![](../../../../assets/230_Module_intro-image-1-510c7988.png)
- Cookies can be used for many purposes, one of which is persistent authentication ("logged in state"). Cookies uses for this are also called "authentication cookies".
- Cookies can be manipulated by the user and front-end code too.
2. Another important aspect of a cookie is that it is included in every request that's made to the website.

## Sessions (not started)
A session is the server side counterpart of a cookie. It may be stored in a database or otherwise.

An "authentication session" is the counterpart of a "authentication cookie".