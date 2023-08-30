## 332. PDFKit - runtime PDF generation
Created Thursday 31 August 2023

## Pre-generating files is impractical
1. Invoices and other 'reports' usually get updated very frequently.
2. Generating files for all possible users/requests is a waste of resources.


## App flow for document/large-data download
Instead of pre-generating, frequently changing documents should either be:
1. Generated at request time
2. Or deferred with a notification - *"We'll send you the document via email when it's ready! ETA: x minutes"*


## Generating documents
For generating PDFs, the [pdfkit](https://pdfkit.org/) package is very helpful. It provides both low-level, high-level constructs as well as support for complex and multi-page PDFs. It runs on the server (Node.js) as well in the browser.

```js
const PDFDocument = require('pdfkit');

app.use((req, res, next) => {
  const pdfDoc = new PDFDocument();
	
  pdfDoc.pipe(res); // pdfDoc --> streams into res --> streams to user

  // optional: create a file too (if it's needed)
  pdfDoc.pipe(require('fs').createWriteStream('path-to-file'));

  pdfDoc.fillColor("black").text("Zeroth line of text");

  pdfDoc
    .fontSize(20)
    .fillColor("red")
    .text("First line of text", { underline: true });

  pdfDoc.fillColor("black").text("Second line of text");

  pdfDoc.end(); // pdfDoc ends --> res ends.
});
```
