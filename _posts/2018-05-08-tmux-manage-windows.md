---
layout: post
title:  "Tmux manage windows."
date:   2018-05-08 17:52:09 +0200
categories: tmux
---

* open a window in the same directory : `tmux neww`
* swap position of current window to tab 0 : `Ctrl+b :` et `swap-window -t 0`
* bindings in tmux.conf

```
unbind %
bind | split-window -h
bind - split-window -v
setw -g automatic-rename on

# keybindings to make resizing easier
bind -r C-h resize-pane -L
bind -r C-j resize-pane -D
bind -r C-k resize-pane -U
bind -r C-l resize-pane -R
```

** sources ** :
  - https://unix.stackexchange.com/questions/12032/create-new-window-with-current-directory-in-tmux
  - https://superuser.com/questions/343572/how-do-i-reorder-tmux-windows
