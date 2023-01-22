# 2. ECMAScript
Created Sunday 22 January 2023 at 06:28 pm

## Interactivity, scripting languages and browser wars
One of the first popular web browsers was Netscape Navigator (released in 1994). There were some problems with this browser:
1. It lacked dynamic behavior
2. Supported static web pages only
3. There was no interactivity after a page was loaded.

To address these problems, Netscape (the company behind Netscape Navigator) created a new *scripting* language called "JavaScript". The name was purely for marketing purpose since Java was the *"hot new language"*.

Note: Java and JavaScript have nothing in common by design, except the C-like syntax.

During the same time, **Microsoft** debuted their web browser - Internet Explorer (aka IE). This led to a browser war between Netscape and Microsoft. Microsoft realized that JavaScript fundamentally changed the browsing experience of the web, so, they wanted to have a similar *"scripting"* language for IE.

Since Microsoft had no specification to follow, they reverse engineered Netscape Navigator's interpreter to create their own language called "JScript".


## Compatibility, developer experience
Since there was no standard, Netscape's "JavaScript" and Microsoft's "JScript" had very different implementations.

This became a big problem for developers, because they now had write each feature twice - for the two platforms. 

Many companies could not afford this double work - so tags like "Best viewed in IE" and "Best viewed in Netscape" came up.


## Standardization and ECMA international
To resolve these issues, Netscape submitted JavaScript to Ecma International in 1996.

Ecma International is an industry association dedicated to standardization of information and communication systems.

Netscape wanted a standard specification that all browser vendors could conform to as it would help keep other implementations consistent across browsers.

For each new specification, Ecma provides a standard specification and a committee.

In case of JavaScript, the standard is called ECMA-262 and the committee that works on this is called Technical Committee-39 (TC-39).

## ECMAScript
Ecma used "ECMAScript" to talk about the resulting official language, because "JavaScript" is a trademark owned by Oracle.

So, ECMAScript refers to the standard language whereas JavaScript is the language we use in practice that is built on top of ECMAScript.

ES2015+ is called modern JavaScript.

In practice, JavaScript and ECMAScript are used interchangeably.