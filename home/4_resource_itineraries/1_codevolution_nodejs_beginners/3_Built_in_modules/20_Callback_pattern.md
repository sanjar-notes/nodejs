# 20. Callback pattern
Created Saturday 28 January 2023 at 11:44 am

## Jargon
1. "Callback" - A function being passed/consumed/returned is called a "callback". Also means an argument accepted by a piece of code (functio, object class), which will run the function with relevant parameters when some desired/undesired state is reached in that piece of code.
2. "Higher order function" - A function that accepts/works-with/returns "callback" functions.


## Types of callbacks (based on execution time)
1. Synchronous callback - a callback function that's executed immediately.
	- "Immediately" means as part of a synchronous chain. 
	- Examples - map, filter, reducer functions, custom functions.
2. Asynchronous callback - a callback function that's not executed immediately.
	- "Not immediately" means deferred execution based on time or event or on error, etc.
	- Examples - eventListeners ('click' event in the DOM), reading/writing to files, querying databases, making network requests.

Nothing new here.