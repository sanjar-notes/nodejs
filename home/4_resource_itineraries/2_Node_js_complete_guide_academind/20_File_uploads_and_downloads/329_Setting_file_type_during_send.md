# 329. Setting file type during send
Created Thursday 31 August 2023

The 
1. file type
2. file name (including extension)
3. mode - whether to preview or download file 

can all be done using 2 headers. Here:
```js
// 1. type
res.setHeader('content-type', 'application/pdf');


// 2. filename and preview/download mode
res.setHeader('content-disposition', 'inline; filename=yourFile.pdf');

// 2.1 download instead of preview
res.setHeader('content-disposition', 'attachment; filename=yourFile.pdf');
```
Code (commit) - https://github.com/exemplar-codes/online-shop-nodejs-branches/commit/61789ec6fbd14d47d8d820cb134fcb53138b82d3