---
layout: blog
title: New feature in C++11 - "enum class"
summary: C++11 has several new features, which make C++ a much better language.
---

Recently, I stumbled upon a new feature in C++11, "enum class"es. A simple feature, but a much need relief. Stroustrup has described the feature briefly in his C++11 FAQ [here](http://www.stroustrup.com/C++11FAQ.html#enum).

Anyone who has worked with C or C++ knows about enumerations, which was really a half-baked feature in the language. The "old" enumerations had the following problems:

+ _Bad scoping rules_ - Enumerations had a global scope, which was not a great idea in the first place. So, if you had two enumerations with same enumerated value, you will need to adopt some sort of coding convention to avoid name collisions.

{% highlight cpp %}
enum BookColor { RED, BLUE, GREEN };
enum PenColor { RED }; // error, RED is already declared
{% endhighlight %}

* _Implicit conversion_ - Since the C days, enumerations are known to convert to integers at the drop of a hat. So, if you have

{% highlight cpp %}
enum BookColor { RED, BLUE, GREEN };
int color = BookColor::RED;   // color = 0 :(
if ( BookColor::RED < 5 )     // perfectly legal with implicit conversion
{% endhighlight %}

* _Inability to specify size of enumeration_ - Size of enumerations and even signed-ness is implementation defined, leading to all sort of confusions and portability problems. So, the above enumeration may be treated as a char on one machine/compiler and an integer on another machine.

### Enter C++11 "enum class"


+ Scoping problem is resolved. So, the enumeration names do not conflict with other enums. This reflects the strong type safety provided by these enum classes. Following is legal in C++11:

{% highlight cpp %}
enum class BookColor { RED, BLUE, GREEN };
enum class PenColor { RED }; // OK
{% endhighlight %}

+ No surprises with implicit conversions

{% highlight cpp %}
if ( BookColor::RED > 5 ) // error, not legal in C++11 with enum class
{% endhighlight %}

* You can specify the size of an enum now. Taking an example from the [proposal document](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2007/n2347.pdf):

{% highlight cpp %}
enum class E : unsigned long { E1 = 1, E2 = 2, Ebig = 0xFFFFFFF0U };
// ability to specify an unsigned type for unsigned enum value
{% endhighlight %}

### Much needed relief

The feature eliminates surprises for new users and ensure type safety, which was missing for so long in C and C++ languages. I guess, I should read the Stroustrup FAQ more often and try to blog everytime I find something new or maybe write something on every topic.