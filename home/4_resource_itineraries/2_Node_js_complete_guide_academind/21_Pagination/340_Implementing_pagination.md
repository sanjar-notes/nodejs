# 340. Implementing pagination
Created Sunday 10 September 2023

Changes:
1. Add [pagination buttons (frontend)](https://github.com/exemplar-codes/online-shop-nodejs-branches/commit/83a2fe1956a828c3354ac790a6d9481615fbf721)
2. [Creating pagination util](https://github.com/exemplar-codes/online-shop-nodejs-branches/commit/1d365365e4b8fda83dfb888aeae0cd233ff847f1), then [correct](https://github.com/exemplar-codes/online-shop-nodejs-branches/commit/f58912507114c3c2f0b362d3a3bb9978a322ed05) it to only do pagination as opposed to sort and filter (these are not relevant to pagination). The util is added as a middleware before listing routes.
3. Calculate db params - "skip" and "limit" (db params) from request pagination params - this involves a [virtual calculation](https://github.com/exemplar-codes/online-shop-nodejs-branches/commit/dbc2626b9b2dfe66f26ced0b8b4497fb3f424bf4). Mongoose's .skip and .limit methods were enough.
4. [Respect existing input](https://github.com/exemplar-codes/online-shop-nodejs-branches/commit/8550e848613bbf78842d12754efb01636e4b9cab) - page size and offset, in rendered buttons.
5. [Add helper buttons](https://github.com/exemplar-codes/online-shop-nodejs-branches/commit/20b5ce37c8e34085f1ba36ecc100c8611212fcc8) - previous, next, first and last helper buttons.

Deployed to render.com, see live https://ecomm-t-pagination.onrender.com/products