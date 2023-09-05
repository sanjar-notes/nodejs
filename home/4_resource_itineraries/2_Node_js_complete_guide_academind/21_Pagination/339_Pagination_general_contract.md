# Pagination general contract (contract)
Created Monday 4 September 2023

Pagination is meant for lists only. 
There are a few standard params involved. 
I'm assuming the client is an SPA (hardest case).

## Request params
1. Page size - number of data items to be sent.
2. Page number - which ('nth') chunk (of page size) to be sent.
3. Offset - items to ignore at the beginning of list.
4. Query parameters - helps in filtering, sorting the list.

## Response
1. data: array of 'page size'
2. pageNumber: sent since page number and size input could be incoherent.
3. pageSize: sent since page number and size input could be incoherent.
4. total: list size had pagination not been there.
   
Optional
1. hasMore - this can be used to disable the 'next' page event/UI at client. This is *optional*, since it's calculable from 'page number', 'page size' and 'total'.
2. isLastPage, for determining how many pills to make.

## Process
Essentially, the code on BE does this:
1. getAll('/resource')
2. filterAndSort(queryParams || null)
3. ignoreTill(offset || 0)
4. divideIntoChunks(pageSize || DEFAULT_PAGE_SIZE)
5. chunks\[pageNumber || 1]

## Edge cases
The input may be anything, but the response should always be coherent.

- If page and page size are not coherent. The server assumes relevant values. It does this in such a way that the response params are coherent. This behavior varies acc to app requirements of course.
	1. If page size is too large or zero, the server ignores the input (and assumes its max limit). The response contains this assumed limit.
	2. If page number is too large, the server assumes the last possible page number. The response contains this assumed page number.

## URI
Example: `/videos?page=1&pageSize=20&sort=asc&sortBy=name&offset=10`