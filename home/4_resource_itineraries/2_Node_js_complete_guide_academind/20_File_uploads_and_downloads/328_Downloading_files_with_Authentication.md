# 328. Downloading files with Authentication
Created Thursday 31 August 2023

Suppose we saved invoices for orders. These files if saved in `multer-uploads` or any such 'statically' served folder is a very bad idea. Reason: anybody can access the invoice of any other person.

So we need to serve the file only if the invoice belongs to the user whose requesting. When some user 'X' requests for invoice 'iY'. There are three parts:

1. **Make these files aren't blindly served** - save the sensitive stuff in their own folder `/invoices` here. `express.static` won't touch this folder.
2. **Check if resource belongs to the user** - the logic of `doesInvoiceBelongToUser(invoiceId, userId)` needs to be decided before hand, a simple approach here is to save the invoices as files whose name is the same as the `orderId`, since we can easily check if `orderId` belongs to `user`.
3. **Send the file** - we dedicate a route `'/invoices/:orderId'` and use `res.sendFile()`/`res.download`


[Code (commit)](https://github.com/exemplar-codes/online-shop-nodejs-branches/commit/976d678572cd94fc3d39a9f9f634ff9193aaf646)