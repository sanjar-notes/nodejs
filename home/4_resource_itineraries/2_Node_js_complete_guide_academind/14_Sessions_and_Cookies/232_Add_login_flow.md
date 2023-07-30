## 232. Add login flow
Created Monday 26 June 2023 at 01:44 am

For now, let's assume that credential lookup (email and password match) exists already.

We have done the following till now:
1. Learn how to set cookie (s) in Express - single cookie, plural cookies.
2. Learn how to read cookies - plain, or with `cookie-parser` package.
3. Learnt that cookies by default are 'Session cookies', i.e. they expire when the browser is closed (i.e. all windows of the browser).
4. Detail wise, we looked two variations.
	1. A boolean called 'loggedIn' as cookie. This works - but there's no way identify a user.
		- A userId cookie in addition to the boolean "loggedIn" cookie solves identification issue. But there's still a problem - impersonating is trivially easy.
	2. Generate a hash of credentials with a server salt (assume it's fixed and known only by the server). This solves impersonation. A problem - maintaining the server salt across server machines, and changing them regularly is still a problem.
		- Using credentials is not a must, we could just have stored the userId. All that matters is here is the salt + some piece of information (userId here). We generate a hash everytime a request comes in using the extra piece of info and our server salt, if it matches with the sent hash, we're good.
		- There's another small problem - it's a preference issue, not strictly a problem. If the server salt does not change, just setting cookies correctly will log the user in, in other words, the user can choose to not use the login page at all, even on completely new devices. They may just copy and paste the cookies on the new device, and it would log them in. This is inconvenient for most web apps - since they wish "track" the user, they want to know when the user logged in, and from what all devices did they do so.