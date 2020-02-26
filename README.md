[![MELPA](http://melpa.org/packages/gerrit-badge.svg)](http://melpa.org/#/gerrit)
[![Build Status](https://travis-ci.org/thisch/gerrit.el.svg?branch=master)](https://travis-ci.org/thisch/gerrit.el)

gerrit.el
=========

This package is currently mainly an emacs interface for the `git-review` CLI
tool. It allows you to upload (`gerrit-upload`) and download
(`gerrit-download`) gerrit changes. In the latter case it is possible to
specify reviewer(s), topic name, WIP flag and custom (git-review)
parameters.

Both the upload and download interfaces are implemented using the great
[hydra](https://github.com/abo-abo/hydra) package.

This package also contains a minimalistic open-reviews status-section
(`gerrit-magit-insert-status`) for magit status buffers.

This code is tested using git-review=0.27 and gerrit=2.16.

## Installation

Make sure that [git-review](https://opendev.org/opendev/git-review) is
installed and that every cloned gerrit repo has a gerrit-specific pre-commit
hook configured (`git review -s`).

This emacs package is available on
[MELPA](http://melpa.org/#/gerrit).

Example `use-package` config

``` el
(use-package gerrit
  :ensure t
  :custom
  (gerrit-host "gerrit.my.domain")
  :config
  (progn
    (add-hook 'magit-status-sections-hook #'gerrit-magit-insert-status t)
    (global-set-key (kbd "C-x i") 'gerrit-upload)
    (global-set-key (kbd "C-x o") 'gerrit-download)))
```

In the case of the gerrit server `review.opendev.org`, the following
variables have to be set:

``` el
(setq gerrit-host "review.opendev.org") ;; runs gerrit-2.13
(setq gerrit-rest-endpoint-prefix "") ;; needed for older gerrit server versions
```

## Similar elisp packages

* [magit-gerrit](https://github.com/darcylee/magit-gerrit) Fork of
unmaintained https://github.com/terranpro/magit-gerrit. Uses the
[`ssh`](https://gerrit-review.googlesource.com/Documentation/cmd-index.html)
interface for performing gerrit requests.

* [gerrit-download](https://github.com/chmouel/gerrit-download.el) Downloads
  gerrit change and shows the diff in a diff buffer. Uses `git-review` under
  the hood.

* [gerrit-el](https://github.com/iartarisi/gerrit-el) reimplementation of
  the gerrit code review Web UI in emacs.
