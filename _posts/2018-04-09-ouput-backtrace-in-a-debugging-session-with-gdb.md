---
layout: post
title:  "Ouput backtrace in a debugging session with gdb."
date:   2018-04-09 19:22:29 +0200
categories: debug C gdb
---

# Output backtrace in a debugging session with gdb.

* source : https://stackoverflow.com/questions/5941158/gdb-print-to-file-instead-of-stdout

The output in a file instead of Stdout, can be done via the logging facilities
of gdb

## Commands

{% highlight bash %}
set logging on
set logging off
show logging
set logging file the_file_to_output.log # gdb.txt by default
set logging overwrite [on|off] # append mode by default
{% endhighlight %}
