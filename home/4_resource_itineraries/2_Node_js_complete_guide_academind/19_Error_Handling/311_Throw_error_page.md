# 311. Throw error page
Created Wednesday 23 August 2023

note: this is not the error sink. It's like a check where we construct the response on the spot.

It's just early response using a util middleware, that renders a page.

But I did this out of necessity, already:
- [util code](https://github.com/exemplar-codes/online-shop-nodejs-branches/commit/b9ec4d285b0619af355cb7c8cd9296b52abaa4c4)
- [usage](https://github.com/exemplar-codes/online-shop-nodejs-branches/commit/bd1baa1d9f788be7378f5848aacef7a06d75685e#diff-1b4e82f3315e11c27c617a1c90a00b21db3a3c22e312fef6d2e8cfcb042aaeeeR102)