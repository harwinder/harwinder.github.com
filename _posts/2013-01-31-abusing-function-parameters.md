---
layout: blog
title: Abusing Function Parameters
summary: How programmers abuse function parameters and how to avoid it
---

## Introduction

Functions are the building blocks for procedural programming. They are very useful constructs, which increases modularity of a program. Inputs to a function are usually specified as parameters and output is generally available from the function in the form of return value.

I am listing two cases here, where I think programmers abuse function parameters and write sloppy code, which can easily be avoided:

## Default Parameters

Default parameters serve a purpose, but only when you use them properly. Their only purpose is to provide a default value for a parameter. However problem arises, when the default value of the function is considered a special case inside the function. If this is being done for a single parameter, it is still acceptable. Complexities arise when you have more than one default parameter in a function and the function logic depends on a combination of these special values of function parameters. This is a very subtle trap and one should avoid falling into this trap.

As a rule of thumb, there should not be any special handling inside the function for the default function parameters. Deviating from this rule will generally land you into unmaintainable code.


## Function Overloading

A lot of programmers abuse function parameters when they should instead have used function overloading. For example, in a trading application you may get different types of data, like last trade price, order depth (best 5 bids/asks), index values etc. To update the market data, a programmer may write a function:

{% highlight cpp %}
bool MarketData::update(LastTradePrice* price,
                        OrderDepth* depth,
                        Index* index)
{% endhighlight %}

Such a function is often internally implemented as:

{% highlight cpp %}
if (price != 0)
    // logic for updating LTP
else if (depth != 0)
    // logic for updating order depth
else if (index != 0)
    // logic for updating index values
{% endhighlight %}

Now, when the LastTradePrice data arrives, the call to the update functions looks like:

{% highlight cpp %}
market->update(price, 0, 0);
{% endhighlight %}

In this example, instead of using function overloading to update inherently different kind of data in a market data widget, the programmer falls into a trap of using function arguments. You must avoid such spaghetti code. Function overloading is a very neat way to handle similar actions on inherently different type of data without polluting the namespace. So, you would have overloaded functions as:

{% highlight cpp %}
bool MarketData::update(const LastTradePrice& );
bool MarketData::update(const OrderDepth& );
bool MarketData::update(const Index& );
{% endhighlight %}

As an added benefit, you also avoid pointers here and can rather rely on strict type checking. However, in languages like C, where you cannot overload functions, you need to have different functions handling different data. For example:

{% highlight cpp %}
int updateLastTradePrice(LastTradePrice* price);
int updateOrderDepth(OrderDepth* depth);
int updateIndex(Index* index);
{% endhighlight %}

## Conclusion

These are the two subtle but fairly common mistakes I have observed in the code I have seen over the last year and a half. It is fairly simple to avoid these mistakes:

- Do not make your behaviour of your functions dependent on default function parameters.
- Create different functions (or overloads) for similar behaviour with different data, rather than adding function parameters.
