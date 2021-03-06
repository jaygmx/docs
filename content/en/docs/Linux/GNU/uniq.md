---
title:  "uniq"
linkTitle::  "uniq"
weight: 100
description: >-
     uniq
---

# ‘uniq’: Uniquify files

‘uniq’ writes the unique lines in the given ‘input’, or standard input
if nothing is given or for an INPUT name of ‘-’.
Synopsis:

``` 
 uniq [OPTION]... [INPUT [OUTPUT]]
```

By default, ‘uniq’ prints its input lines, except that it discards all
but the first of adjacent repeated lines, so that no output lines are
repeated. Optionally, it can instead discard lines that are not
repeated, or all repeated lines.

The input need not be sorted, but repeated input lines are detected only
if they are adjacent. If you want to discard non-adjacent duplicate
lines, perhaps you want to use ‘sort -u’. \*Note sort invocation::.

Comparisons honor the rules specified by the ‘LC\_COLLATE’ locale
category.

If no OUTPUT file is specified, ‘uniq’ writes to standard output.

The program accepts the following options. Also see \*note Common
options::.

‘-f N’ ‘--skip-fields=N’ Skip N fields on each line before checking for
uniqueness. Use a null string for comparison if a line has fewer than N
fields. Fields are sequences of non-space non-tab characters that are
separated from each other by at least one space or tab.

``` 
 For compatibility ‘uniq’ supports a traditional option syntax ‘-N’.
 New scripts should use ‘-f N’ instead.
```

‘-s N’ ‘--skip-chars=N’ Skip N characters before checking for
uniqueness. Use a null string for comparison if a line has fewer than N
characters. If you use both the field and character skipping options,
fields are skipped over first.

``` 
 On systems not conforming to POSIX 1003.1-2001, ‘uniq’ supports a
 traditional option syntax ‘+N’.  Although this traditional behavior
 can be controlled with the ‘_POSIX2_VERSION’ environment variable
 (*note Standards conformance::), portable scripts should avoid
 commands whose behavior depends on this variable.  For example, use
 ‘uniq ./+10’ or ‘uniq -s 10’ rather than the ambiguous ‘uniq +10’.
```

‘-c’ ‘--count’ Print the number of times each line occurred along with
the line.

‘-i’ ‘--ignore-case’ Ignore differences in case when comparing lines.

‘-d’ ‘--repeated’ Discard lines that are not repeated. When used by
itself, this option causes ‘uniq’ to print the first copy of each
repeated line, and nothing else.

‘-D’ ‘--all-repeated\[=DELIMIT-METHOD\]’ Do not discard the second and
subsequent repeated input lines, but discard lines that are not
repeated. This option is useful mainly in conjunction with other options
e.g., to ignore case or to compare only selected fields. The optional
DELIMIT-METHOD, supported with the long form option, specifies how to
delimit groups of repeated lines, and must be one of the following:

``` 
 ‘none’
      Do not delimit groups of repeated lines.  This is equivalent
      to ‘--all-repeated’ (‘-D’).

 ‘prepend’
      Output a newline before each group of repeated lines.  With
      ‘--zero-terminated’ (‘-z’), use a zero byte (ASCII NUL)
      instead of a newline as the delimiter.

 ‘separate’
      Separate groups of repeated lines with a single newline.  This
      is the same as using ‘prepend’, except that no delimiter is
      inserted before the first group, and hence may be better
      suited for output direct to users.  With ‘--zero-terminated’
      (‘-z’), use a zero byte (ASCII NUL) instead of a newline as
      the delimiter.

 Note that when groups are delimited and the input stream contains
 blank lines, then the output is ambiguous.  To avoid that, filter
 the input through ‘tr -s '\n'’ to remove blank lines.

 This is a GNU extension.
```

‘--group\[=DELIMIT-METHOD\]’ Output all lines, and delimit each unique
group. With ‘--zero-terminated’ (‘-z’), use a zero byte (ASCII NUL)
instead of a newline as the delimiter. The optional DELIMIT-METHOD
specifies how to delimit groups, and must be one of the following:

``` 
 ‘separate’
      Separate unique groups with a single delimiter.  This is the
      default delimiting method if none is specified, and better
      suited for output direct to users.

 ‘prepend’
      Output a delimiter before each group of unique items.

 ‘append’
      Output a delimiter after each group of unique items.

 ‘both’
      Output a delimiter around each group of unique items.

 Note that when groups are delimited and the input stream contains
 blank lines, then the output is ambiguous.  To avoid that, filter
 the input through ‘tr -s '\n'’ to remove blank lines.

 This is a GNU extension.
```

‘-u’ ‘--unique’ Discard the last line that would be output for a
repeated input group. When used by itself, this option causes ‘uniq’ to
print unique lines, and nothing else.

‘-w N’ ‘--check-chars=N’ Compare at most N characters on each line
(after skipping any specified fields and characters). By default the
entire rest of the lines are compared.

‘-z’ ‘--zero-terminated’ Delimit items with a zero byte rather than a
newline (ASCII LF). I.e., treat input as items separated by ASCII NUL
and terminate output items with ASCII NUL. This option can be useful in
conjunction with ‘perl -0’ or ‘find -print0’ and ‘xargs -0’ which do the
same in order to reliably handle arbitrary file names (even those
containing blanks or other special characters). Note with ‘-z’ the
newline character is treated as a field separator.

An exit status of zero indicates success, and a nonzero value indicates
failure.
