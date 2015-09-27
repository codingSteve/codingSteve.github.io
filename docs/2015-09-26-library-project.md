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

Building a simple library project
=================================

Our library members interact with the library via a FrontDesk object which hides some of the complexity of the main library implementation and also allows for a layer of [abstraction to be introduced][ITEM6]. An exercise in TDD, java 8 streams and simplicity of design. Based on a simple spec, we have four pieces of functionality to support:

- [borrow a book][ITEM1]
- [return a book][ITEM2]
- [view the available items][ITEM3]
- [view the overdue items][ITEM4]


<div id="social">
    <iframe id="gh-fork" src="http://ghbtns.com/github-btn.html?user=codingsteve&repo=library&type=fork" allowtransparency="true" frameborder="0" scrolling="0" width="55px" height="20px"></iframe>
    <a href="https://twitter.com/codingSteve" class="twitter-follow-button" data-show-count="false" data-lang="en">Follow @codingSteve</a>
    <a href="https://twitter.com/share" class="twitter-share-button" data-url="{{ post.url}}" data-via="codingSteve" data-lang="en">Tweet</a>
</div>



Borrowing a book
----------------

In order to borrow a book from the library, we have some preconditions:

- we are a member of the library
- we have permission to borrow the book
- the book must be available in the library's stock

{% highlight java linenos %}

	public boolean requestCheckout(final LibraryMember m, final Item i) {
		logger.info("About to check for availability for item {}", i);

		final boolean isAvailable = (0 < library.getStockAvailable(i));
		final boolean checkoutSuccessful = isAvailable && library.checkout(i, m);
		return checkoutSuccessful;
    }
{% endhighlight %}


Returning a book
----------------
When we return a book the library should check for any [fines][FINES]. 

We have some requirements for returning a book (or other item)

- The book should have been borrowed by the member who is returning it. 
- The due date should be after today. Otherwise we fine the member. 


Checking the inventory
----------------------

We need to check the total stock and review the current open loans. 

Members should only be aware of the items they'll be permitted to check out of the library, so we filter the library's catalogue on their allowed item types.

We build a picture of the current open loans then merge the two data structures and present back a unique list of available items.




Checking for overdue items
--------------------------

We can simply look at the open loans and check their expected return date against the current business date.

{% highlight java linenos %}
	public Collection<LoanRecord> getOverdueItems() {
		return getOverdueItemsStream().collect(Collectors.toList());
    }

    // build the initial stream of overdue items
    // ready for either returning to the client
    // or re-filtering by user.
    private Stream<LoanRecord> getOverdueItemsStream() {
		return loans.stream().filter(lr -> lr.expectedReturnDate.compareTo(businessDate) < 0);
    }

    //The streams data processing chain is not executed until we call a terminator
    private Stream<LoanRecord> getOverdueItemsStreamByMember(final LibraryMember m) {
		return getOverdueItemsStream().filter(lr -> lr.member.equals(m));
    }

	public Collection<LoanRecord> getOverdueItems(final LibraryMember m) {
		return getOverdueItemsStreamByMember(m).collect(Collectors.toList());
	}

{% endhighlight %}




Further extensibility
----------------------

There are some specific actions and behaviours we expect to cover:
- a member will want to perform an action (or ask a question) about a specific item
-  member will want to ask about a set of items in the library
- the library will want an overview on various sets of items. 

Grouping the actions under a small number of interfaces means that we can save on code in the core library class and move behaviour into "micro-service" implementations. Laying out the supported services in a config file and processing that during startup would mean we can add services without touching the main Library classes, limiting risk to the existing functionality and clients. 


   [ITEM1]: https://github.com/codingSteve/library/issues/1
   [ITEM2]: https://github.com/codingSteve/library/issues/2
   [ITEM3]: https://github.com/codingSteve/library/issues/3
   [ITEM4]: https://github.com/codingSteve/library/issues/4
   [ITEM6]: https://github.com/codingSteve/library/issues/6
   [FINES]: /docs/2015-09-26-fee-schedule






