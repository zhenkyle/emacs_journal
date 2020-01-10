+++
title = "Change Color"
date = 2020-01-10
+++

Followed this interesting video blog: [Switching to GNU Emacs][1], I changed my Emacs's color to [Dracula theme][2], my Emacs looks more like a morden text editor now.

# What is Dracula theme
Dracula theme is A dark theme for Emacs.

# Install
Install `dracula-theme` from MELPA

## Using Customize to change theme
Goto menubar: `Options` - `Customize Emacs` - `Customize Theme`, select `dracula` theme ,then click `Save Theme Settings`.

This will add the following line to you `init.el`.
```
;; under (custom-set-variables
 '(custom-enabled-themes (quote (dracula)))
```

## Another way to change theme
Another way to change theme is manually add the following line to your `init.el`:
```
(load-theme 'dracula t)
```

# Tweak Emacs
As I learned from [Switching to GNU Emacs][1], I can further tweak Emacs to have a more professional look.
## Add Relative Line numbers
Goto menubar: `Options` - `Show/Hide` - `Line Number for All Lines`, check `Relative Line Numbers`.

## Hide menubar

## Hide toolbar
## Hide scorllbar
TODO

# TODO: tweak fonts
After apply `Dracula theme`, The fonts in my setting is not exactly like the screenshot in `Dracula theme`'s home page. How to change fonts? Are there any recommendations?

[1]: https://www.youtube.com/watch?v=Y8koAgkBEnM
[2]: https://draculatheme.com/emacs/
