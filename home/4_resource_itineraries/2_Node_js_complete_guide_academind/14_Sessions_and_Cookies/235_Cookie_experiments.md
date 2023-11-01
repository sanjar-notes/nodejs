# 235. Cookie experiments
Created Sun Oct 22, 2023 at 12:56 AM


- Code + observations, https://github.com/exemplar-codes/cookies-experiments
- [Live table at Notion](https://www.notion.so/Experiments-with-cookies-9bfd4f4d46494084b14af6fb36cc072a?pvs=4)
- This is good: https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies

---
Only sameSite strict is the **only one** that can offer CSRF protection, and even that's not complete protection. External links (PDF, README) still cause cookies to be sent. It's best to use a CSRF token.

Weird/crazy things in Express noted in repo at relevant places