---
layout: post
title: "Tracking time spent on tasks with an Org-mode table"
author: "Cristina Elep"
tags: [org-mode, emacs, spacemacs]
---

Org-mode has a lot of nice project-planning features, including a system for [clocking time spent on various activities][org-clocking-docs]; so far I've found a [comprehensive post][org-clocking-article] about it with detailed examples by Lee Hinman, and likely there are others out there who've gone over these features in depth. I haven't used the clocking features myself, instead opting for simple spreadsheets using Org tables.

I started by looking up how to calculate the sum of a column; the answers and comments to [this question on StackOverflow][so-column-sum] provide a number of examples. One option is to press `C-c +` in the cell where you want the sum of the column to appear, then paste it in with `C-y`:

```
| Tasks | Minutes |
|-------|---------|
| Read  |      30 |
| Blog  |      45 |
|-------|---------|
| Total |         | <-- C-c + then C-y here to paste in the sum (75)
```

You have to do this every time you want to compute the sum, though, which can be tedious. Another option is to specify a formula for the cell by pressing `C-c =` while the cursor's in it then entering the formula at the prompt. In this case, you can use a formula that sums up the values in between the first and second horizontal lines:

```
| Tasks | Minutes |
|-------|---------|
| Read  |      30 |
| Blog  |      45 |
|-------|---------|
| Total |      75 |
#+TBLFM: @>$2=vsum(@I..@II)
```

`@>$2` refers to the cell in the last row (`@>`) and the second column (`$2`), and `@I..@II` refers to the range between the first and second horizontal lines. The result of the formula can be recalculated by pressing `C-c C-c` while the cursor is on it. Org's documentation goes into more detail about [field and range formulas][org-field-range-formulas] and [column formulas][org-column-formulas]; there's also a [tutorial][org-spreadsheet-tutorial] about using Org for spreadsheets.

I'd thought that this was already enough, but it turns out that Org can also calculate time values (because of course it can); you can specify them using `HH:MM[:SS]` notation (the seconds are optional):

```
|  Read | Blog |
|-------|------|
|  0:30 | 0:45 |
|  0:15 | 0:21 |
|-------|------|
| 00:45 | 1.10 |
#+TBLFM: @>$1=vsum(@I..@II);U::@>$2=vsum(@I..@II);t
```

This example includes two out of three ways to format the results (all of them are documented [here][org-time-values]). The first uses the `U` flag to specify the `HH:MM` format; the second uses the `t` flag, whose format depends on the value of the `org-table-duration-custom-format` variable. In this case, the variable is set to `hours`, which tells Org to compute the hours and minutes as a decimal value. You can check the value of `org-table-duration-custom-format` using `M-x find-variable`.

This is enough for my simple calculations, though I might try out Org's time clocking features someday.

[so-column-sum]: https://stackoverflow.com/questions/6688075/permanently-summing-a-column-in-an-org-mode-table
[org-field-range-formulas]: https://orgmode.org/manual/Field-and-range-formulas.html#Field-and-range-formulas
[org-column-formulas]: https://orgmode.org/manual/Column-formulas.html#Column-formulas
[org-time-values]: https://orgmode.org/manual/Durations-and-time-values.html#Durations-and-time-values
[org-spreadsheet-tutorial]: https://orgmode.org/worg/org-tutorials/org-spreadsheet-intro.html
[org-clocking-article]: https://writequit.org/denver-emacs/presentations/2017-04-11-time-clocking-with-org.html
[org-clocking-docs]: https://orgmode.org/manual/Clocking-work-time.html
