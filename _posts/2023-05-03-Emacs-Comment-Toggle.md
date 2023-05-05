---
title: Emacs Comment Toggle!
date: 2023-05-04 07:19:00 -600
categories: [emacs, programming]
tags: [emacs, programming, doom]
---

## Emacs Comment Toggle

Comment toggling is one of my most heavily used features of a text editor. When I recently switched from vim to mainly doom emacs, I was disapointed to find that there was no built in keybinding for comment toggling single lines or blocks. After some googling, I found a system that works for me.

Add this to your config.el. I use doom emacs, but this could be pretty easily tweaked to work with vanilla emacs as well. 

Just press `<leader>` (in my case, space), `c`, then `;` to toggle a line or block of selected lines between commented / uncommented.

```lisp
;; Comments or uncomments a region or line
(defun comment-or-uncomment-region-or-line ()
  " Comment or uncomments the region or the current line if there is no active region."
  (interactive)
  (let (beg end)
    (if(region-active-p)
        (setq beg (region-beginning) end (region-end))
        (setq beg (line-beginning-position) end (line-end-position)))
    (comment-or-uncomment-region beg end)))

(map! :leader
      :desc "Comment or uncomment block or line"
      "c ;" #'comment-or-uncomment-region-or-line)
```
