---
layout: blog
title: Notes on Profiling
summary: My notes on profiling and using the output to find bottnecks in the application
---

### Using gprof

+ Add -pg flag to the compiler using CXXFLAGS or CFLAGS

+ Add debug information using -g flag to the compiler

+ The program must do an exit(), so that gprof can write its output to the gmon.out file. If the program does not already do this, add a signal handler to respond to SIGINT etc.

### Tools required to generate (beautiful)call graph


{% highlight bash %}
yum install graphviz
pip install gprof2dot
{% endhighlight %}

gprof2dot is also available from [this](https://github.com/jrfonseca/gprof2dot) link.

### Generate Call Graph


{% highlight bash %}
/path/to/your/executable arg1 arg2
gprof path/to/your/executable | gprof2dot.py | dot -Tpng -o output.png
{% endhighlight %}
