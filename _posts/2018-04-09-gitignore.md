---
layout: post
title:  "gitignore"
date:   2018-04-09 19:22:29 +0200
categories: git
---

## Configuration
Git allows users to configure which files or directories they want
it to ignore. It can be done via multiple files :

* `$HOME/.config/git/ignore`
* `$HOME/.gitignore`
* `/project/path/.gitignore`

A lot of gitignore files can be found in [https://github.com/github/gitignore](https://github.com/github/gitignore).

## Modifying gitgnore.

When you modify a gitignore file, so that some files will be ignored, it happens that Git don't ignore them. In order to fix that:

{% highlight bash %}
git rm -r --cached .
git add .
git commit -m "fixed untracked files"
{% endhighlight %}

https://stackoverflow.com/questions/11451535/gitignore-is-not-working
