---
layout: post
title:  "Merge file from another branch."
date:   2018-05-08 17:21:29 +0200
categories: git
---

2 branches in a repo :

```bash
~> git branch
*  master
*  branch1
*  branch2
```

I want to merge a version of a file from branch2 in branch 1

```bash
~> git checkout branch1
~> tree
.
├── gpl-3.0.txt
├── lib
│   ├── file1.rb
│   ├── file2.rb
│   ├── file3.rb
.   ├── file4.rb
.
~> git checkout branch2 lib/file3.rb
```
