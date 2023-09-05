# 338. Module Intro
Created Monday 4 September 2023

## Situation
When you search 'bulb' on Amazon, it's impractical for the site to load all items that match.
- Instead it loads a fixed number of items (say 30) the first time.
- There's an event - a click, or scroll to end (infinite scroll), that gets the next 30
- And so on.

This technique is called pagination. It reduces load on the server and is important to keep server side apps manageable.