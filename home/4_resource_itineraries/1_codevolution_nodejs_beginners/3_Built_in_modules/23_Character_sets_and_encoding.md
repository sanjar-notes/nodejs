# 23 Character Sets and encoding
Created Saturday 28 January 2023 at 02:08 pm

This is a detour from learning about modules.

Good to know: Character <--> ASCII equivalent number in JS
```js
// string to number
"V".charCodeAt(); // 86
"⚡️".charCodeAt(); // 9889

'ABC'.charCodeAt(2); // 67. multi size string supported. 
// Also, that means default param is 0.
```

```js
// number to string
String.fromCharCode(65); // 'A'

String.fromCharCode(65, 66, 67); // 'ABC', comma separated supported
```


## Character sets (number <--> character mapping)
Character sets are number <--> character mapping.
1. ASCII
2. Unicode

Character sets, by nature, are arbitary.


## Character encoding (character number <--> binary mapping)
Character encoding are character number <--> binary mapping.

It's needed because of the following situation: we have a number for a given character. How do we convert it into binary?
1. Use 2's complement?
2. What about endianness?
3. How many bits to use?

All this logic for (number for a character <--> binary) is called character encoding.

Some popular character encodings:
1. UTF-8: 2's complement, little-endian, 8 bits.

Similarly, there are "encodings" for video, audio, pictures, etc.
