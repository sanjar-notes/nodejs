# 138. Comparing SQL and NoSQL databases
Created Tuesday 21 March 2023 at 10:05 pm

## Two ways of scaling
Two useful ways of approaches to scaling are:
1. Horizontal scaling - increase the number of devices, of the same type/power. Of course, we need software and processes to keep the whole data coherent. This is difficult to manage, but can be used indefinitely.
2. Vertical scaling - make the existing device(s) stronger, individually. This is very easy to do, but cannot be scaled indefinitely, due to fundamental physical constraints of hardware.

![](/assets/138_Comparison_overview-image-1.png)


## Comparison overview
| SQL                                                                     | NoSQL                                             |
|-------------------------------------------------------------------------|---------------------------------------------------|
| Data uses schemas                                                       | Schema-less                                       |
| Relations                                                               | No (or very few) relations                        |
| Data is kept in multiple tables                                         | Data is merged/nested in a few collections        |
| Horizontal scaling is difficult/impossible.Vertical scaling is possible | Both horizontal and vertical scaling are possible |
| Cannot handle large reads/writes per second                           | Easily handles a lot of reads/writes per second   |

NoSQL may look like the clear winner here. But the choice of database depends on a lot of things:
1. Amount of structure needed in the data?
2. High throughput app?
3. How frequently does the data change?
4. Are there parts of the app that have different characteristics - maybe use different types of databases for different parts/services of the app?


We'll learn to use both types of databases in this course.
