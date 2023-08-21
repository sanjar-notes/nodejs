# 294. Custom validators
Created Tuesday 22 August 2023

We have isEmail and other built in "validators". But we can create our own very easily too.

1. Just chain `.custom(myCallbackNeedToSpecify)` 
2. the callback structure is simple - first param is the value, and the second is an object containing location, params, href and req itself (basically all we need to decide an error or not).
	```js
	check('adhocEmail')
    /**
     * @param value             Value to be validated (if present) | undefined
     * @param {Object} req      Express request object
     * @param {String} path     'address.country'
     * @param {String} location 'body' | 'param' | 'header' | 'query'
     *
     * @returns truthy if no error | ( throw new Error('') | falsy )
     */
	.custom((value, { path, location, req }) => {
	  const hasAnError = ...// some logic;
	  
	  if(hasAnError) {
	    // throw an error or return falsy
	    // prefer throwing since it allows to pass pass an error message
	    throw new Error('some specific error occured');
	    return false;
	  }

	   // return truthy to indicate not error
	  return true;
	})
	```
3. Signaling valid/invalid in the callback - if the data is valid, return `true`. Else throw an error `throw new Error('somemessage')`. That's it.

Of course to validate multiple fields, just add multiple `.custom`

Code - https://github.com/exemplar-codes/online-shop-nodejs-branches/commit/29797550b7b633fbf6241732a52de103e3afa6f8