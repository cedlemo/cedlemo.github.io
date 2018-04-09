---
layout: post
title:  "Debugging ruby gnome native extensions."
date:   2018-04-09 19:22:29 +0200
categories: debug C gdb
---



{% highlight bash %}
ruby extconf.rb --enable-debug-build
# for fedora
sudo dnf debuginfo-install ruby-2.4.3-87.fc27?x86_64
cd gtk3
gtk3 % gdb --args ruby test/run-test.rb -t /Assistant/
{% endhighlight %}
