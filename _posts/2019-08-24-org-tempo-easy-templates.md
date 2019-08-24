---
layout: post
title: "Re-enabling Org-mode easy templates using Org Tempo"
author: "Cristina Elep"
tags: [org-mode, emacs, spacemacs]
---

After updating emacs to version 26, my Spacemacs config also needed an update; I last updated it a few years ago, and I've gotten way behind the latest stable version. So far I haven't had any problems, though I'm still running into changes here and there that I hadn't expected. One of these is the apparent disappearance of Org-mode's easy templates, which includes shortcuts like `< s TAB` for inserting source blocks (`#+BEGIN_SRC ... #+END_SRC`) and `< q TAB` for inserting quotation blocks (`#+BEGIN_QUOTE ... #+END_QUOTE`).

It took me a bit of googling to find the relevant [Spacemacs issue on Github][spacemacs-issue] describing this problem; it links to a section of the [Org-mode 9.2 changelog][org-changelog] that mentions a new template expansion mechanism introduced in 9.2. Source and quotation blocks can be inserted by invoking `org-insert-structure-template` with `C-c C-,` then entering the letter corresponding to the respective type (ie, `s` for source blocks and `q` for quotation blocks). A buffer containing the list of available types is displayed, though they only have partial overlap with the [list of easy templates][easy-templates] in the Org manual.

The Spacemacs issue thread contains a number of suggested workarounds to bring back the easy templates; the one that worked for me was the same one suggested by the Org-mode 9.2 changelog, which involves requiring the Org Tempo library. For my Spacemacs config, I followed the suggestion to add `(require 'org-tempo)` to the `dotspacemacs/user-config` section of my `.spacemacs`.

[easy-templates]: https://orgmode.org/manual/Easy-templates.html
[org-changelog]: https://orgmode.org/Changes.html#outline-container-org1b5e967
[spacemacs-issue]: https://github.com/syl20bnr/spacemacs/issues/11798
