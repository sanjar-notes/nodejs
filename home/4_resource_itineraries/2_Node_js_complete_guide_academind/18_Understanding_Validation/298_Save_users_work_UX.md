# 298. Save user's work (UX)
Created Tuesday 22 August 2023

## The idea (UX)
The idea is simple - upon validation error, the client should not have to fill up the values again. DON'T redirect, since they will have to fill the form again.

Instead we should just show the errors (for fields) and keep the filled values intact. So they may edit the form and submit again.


## SPA vs non-SPA
SPA vs notSPA changes things a little here.
- non SPA (ssr) - add conditional error CSS to form and the template engine can do the prefilling (with received form) as well as conditionally apply the CSS (based on validation errors).
	- or simply use a flashing library.
- SPA - since we make a AJAX call, the same thing happens except that we don't need to prefill (since the page never "really" redirects in an SPA). It's simple here - just show the errors based on error keys returned by the server, via a Toast/notification.


## RoR style actions help here
Suppose you do have a traditional app (server side rendering).

An observation: the 7 CRUD endpoints of RoR solve this issue very well, since they have new and edit actions which are supposed to take care of pre-filling and error. It's a good pattern (separated from create and update action).