+++
title = "Projectile"
date = 2020-01-16T15:00:00Z
+++

[Projectile][1] is a popular project interaction library for Emacs. Here is official [documentation][2].

# Overview

Project means a groups of files together, especially code, accroding to the [EmacsWiki CategoryProject][3] page. Different project management libraries have different views of projects. As far as I know, a project will always have a root directory in which contains all project files.
There are many Projectile alternatives,including CEDET, which seem like came out earlier and more advanced, I haven't tried it yet. EmacsWiki recommends it is probably not useful to use more both of them at the same time, for the same project. So I decided to try Projectile first.

My basic understanding of project management came from Sublime text. The feature I wanted most is the ability to goto anything in a project very quickly and search anything very quickly. The following post recorded how I do it in Projectile' way.

# Install

Install `projectile` package from MELPA. Add the following lines to your `init.el` is good enough to go.
```
(projectile-mode +1)
(define-key projectile-mode-map (kbd "s-p") 'projectile-command-map)
(define-key projectile-mode-map (kbd "C-c p") 'projectile-command-map)
(setq projectile-completion-system 'helm)
```
Note:
1. the first line enables projectile mode, it is the same as `projectile-global-mode` but the latter is deprecated.
2. The second line defines `Super - p` as projectile keymap prefixes, but I can't use Super key in Emacs on Gnome Desktop, which seems like blocked by Gnome. So I can only use `C-c p` defined in the third line.
3. the last line change projectile's completion system from the default `ido` to `helm`, of course `helm` package also need to be insalled.
4. There is another [`helm-projectile` package][4] writen by the same author offering some more intergration with `helm`, but I decided not to install it right now, course it seems like less maintained and offers no new features. [Here][5] is an indepth post explained how `helm-projectile` works, it is recommended to read before you try.


# Basic Usage

You can use `C-c p ?` or `C-c p C-h` to show Projectile keys or use `M-x` following `projectile` to see all Projectile commands.

## Project

Projectile automatic detect projects -- a collections of files within a root directory, with out any configuration. If this failed, you can also add a `.projectile` as a project marker in the root directory to force it to be detected as a project.

* Add a project to project list
    visit any file or directory, projectile can detect project automaticly, or you can make a project by the `.projectile` project marker.
* Delete project in project list
    `M-x projectile-remove-known-project` can clear a selected project
	`M-x projectile-clear-known-projects` can clear the project list
* Switch project
    `C-c p p` Switch project
* Show projects in project list
    `C-c p p` Switch project, use this to see projects in project list

## TODO: File

## TODO: Grep


[1]: https://github.com/bbatsov/projectile
[2]: https://www.projectile.mx/
[3]: https://www.emacswiki.org/emacs/CategoryProject
[4]: https://github.com/bbatsov/helm-projectile
[5]: https://tuhdo.github.io/helm-projectile.html