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
When we return a book the library should check for any fines. 

We have some requirements for returning a book (or other item)

- The book should have been borrowed by the member who is returning it. 
- The due date should be after today. Otherwise we fine the member. 












   [ITEM1]: https://github.com/codingSteve/library/issues/1
   [ITEM2]: https://github.com/codingSteve/library/issues/2
   [ITEM3]: https://github.com/codingSteve/library/issues/3
   [ITEM4]: https://github.com/codingSteve/library/issues/4







