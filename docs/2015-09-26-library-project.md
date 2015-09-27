---
layout: page
meta-title: Lambas in Java 8
title: A simple library 
slug: loaning-from-the-library
excerpt_separator: <!--more-->
tags:
 - java
 - library
 - Saturday project 
---


Based on the simple spec, we have four pieces of functionality to support:

- [borrow a book][ITEM1]
- [return a book][ITEM2]
- [view the available items][ITEM3]
- [view the overdue items][ITEM4]


Borrowing a book
----------------

In order to borrow a book from the library, we have some preconditions:

- we are a member of the library
- we have permission to borrow the book
- the book must be available in the library's stock



Returning a book
----------------
When we return a book the library should check for any [fines][FINES]. 

We have some requirements for returning a book (or other item)

- The book should have been borrowed by the member who is returning it. 
- The due date should be after today. Otherwise we fine the member. 







Further extensibility
----------------------

There are some specific actions and behaviours we expect to cover:
- a member will want to perform an action (or ask a question) about a specific item
-  member will want to ask about a set of items in the library
- the library will want an overview on various sets of items. 




   [ITEM1]: https://github.com/codingSteve/library/issues/1
   [ITEM2]: https://github.com/codingSteve/library/issues/2
   [ITEM3]: https://github.com/codingSteve/library/issues/3
   [ITEM4]: https://github.com/codingSteve/library/issues/4
   [FINES]: /docs/2015-09-26-fee-schedule






