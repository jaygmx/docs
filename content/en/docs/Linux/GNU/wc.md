---
title:  "wc"
linkTitle::  "wc"
weight: 100
description: >-
     wc
---

# ‘wc’: Print newline, word, and byte counts

‘wc’ counts the number of bytes, characters, whitespace-separated words,
and newlines in each given FILE, or standard input if none are given or
for a FILE of ‘-’.
Synopsis:

```bash
 wc [OPTION]... [FILE]...
```

‘wc’ prints one line of counts for each file, and if the file was given
as an argument, it prints the file name following the counts. If more
than one FILE is given, ‘wc’ prints a final line containing the
cumulative counts, with the file name ‘total’. The counts are printed in
this order: newlines, words, characters, bytes, maximum line length.
Each count is printed right-justified in a field with at least one space
between fields so that the numbers and file names normally line up
nicely in columns. The width of the count fields varies depending on the
inputs, so you should not depend on a particular field width. However,
as a GNU extension, if only one count is printed, it is guaranteed to be
printed without leading spaces.

By default, ‘wc’ prints three counts: the newline, words, and byte
counts. Options can specify that only certain counts be printed. Options
do not undo others previously given, so

```bash
 wc --bytes --words
```

prints both the byte counts and the word counts.

With the ‘--max-line-length’ option, ‘wc’ prints the length of the
longest line per file, and if there is more than one file it prints the
maximum (not the sum) of those lengths. The line lengths here are
measured in screen columns, according to the current locale and assuming
tab positions in every 8th column.

The program accepts the following options. Also see \*note Common
options::.

‘-c’ ‘--bytes’ Print only the byte counts.

‘-m’ ‘--chars’ Print only the character counts.

‘-w’ ‘--words’ Print only the word counts.

‘-l’ ‘--lines’ Print only the newline counts.

‘-L’ ‘--max-line-length’ Print only the maximum display widths. Tabs are
set at every 8th column. Display widths of wide characters are
considered. Non-printable characters are given 0 width.

‘--files0-from=FILE’ Disallow processing files named on the command
line, and instead process those named in file FILE; each name being
terminated by a zero byte (ASCII NUL). This is useful when the list of
file names is so long that it may exceed a command line length
limitation. In such cases, running ‘wc’ via ‘xargs’ is undesirable
because it splits the list into pieces and makes ‘wc’ print a total for
each sublist rather than for the entire list. One way to produce a list
of ASCII NUL terminated file names is with GNU ‘find’, using its
‘-print0’ predicate. If FILE is ‘-’ then the ASCII NUL terminated file
names are read from standard input.

```bash
 For example, to find the length of the longest line in any ‘.c’ or
 ‘.h’ file in the current hierarchy, do this:

      find . -name '*.[ch]' -print0 |
        wc -L --files0-from=- | tail -n1
```

An exit status of zero indicates success, and a nonzero value indicates
failure.
