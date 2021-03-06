---
title:  "comm"
linkTitle::  "comm"
weight: 100
description: >-
     comm
---

# ‘comm’: Compare two sorted files line by line

‘comm’ writes to standard output lines that are common, and lines that
are unique, to two input files; a file name of ‘-’ means standard input.
Synopsis:

``` 
 comm [OPTION]... FILE1 FILE2
```

Before ‘comm’ can be used, the input files must be sorted using the
collating sequence specified by the ‘LC\_COLLATE’ locale. If an input
file ends in a non-newline character, a newline is silently appended.
The ‘sort’ command with no options always outputs a file that is
suitable input to ‘comm’.

With no options, ‘comm’ produces three-column output. Column one
contains lines unique to FILE1, column two contains lines unique to
FILE2, and column three contains lines common to both files. Columns are
separated by a single TAB character.

The options ‘-1’, ‘-2’, and ‘-3’ suppress printing of the corresponding
columns (and separators). Also see \*note Common options::.

Unlike some other comparison utilities, ‘comm’ has an exit status that
does not depend on the result of the comparison. Upon normal completion
‘comm’ produces an exit code of zero. If there is an error it exits
with nonzero status.

If the ‘--check-order’ option is given, unsorted inputs will cause a
fatal error message. If the option ‘--nocheck-order’ is given, unsorted
inputs will never cause an error message. If neither of these options is
given, wrongly sorted inputs are diagnosed only if an input file is
found to contain unpairable lines. If an input file is diagnosed as
being unsorted, the ‘comm’ command will exit with a nonzero status (and
the output should not be used).

Forcing ‘comm’ to process wrongly sorted input files containing
unpairable lines by specifying ‘--nocheck-order’ is not guaranteed to
produce any particular output. The output will probably not correspond
with whatever you hoped it would be.

‘--check-order’ Fail with an error message if either input file is
wrongly ordered.

‘--nocheck-order’ Do not check that both input files are in sorted
order.

``` 
 Other options are:
```

‘--output-delimiter=STR’ Print STR between adjacent output columns,
rather than the default of a single TAB character.

``` 
 The delimiter STR may not be empty.
```

‘--total’ Output a summary at the end.

``` 
 Similar to the regular output, column one contains the total number
 of lines unique to FILE1, column two contains the total number of
 lines unique to FILE2, and column three contains the total number
 of lines common to both files, followed by the word ‘total’ in the
 additional column four.

 In the following example, ‘comm’ omits the regular output (‘-123’),
 thus just printing the summary:

      $ printf '%s\n' a b c d e     > file1
      $ printf '%s\n'   b c d e f g > file2
      $ comm --total -123 file1 file2
      1       2       4       total

 This option is a GNU extension.  Portable scripts should use ‘wc’
 to get the totals, e.g.  for the above example files:

      $ comm -23 file1 file2 | wc -l    # number of lines only in file1
      1
      $ comm -13 file1 file2 | wc -l    # number of lines only in file2
      2
      $ comm -12 file1 file2 | wc -l    # number of lines common to both files
      4
```

‘-z’ ‘--zero-terminated’ Delimit items with a zero byte rather than a
newline (ASCII LF). I.e., treat input as items separated by ASCII NUL
and terminate output items with ASCII NUL. This option can be useful in
conjunction with ‘perl -0’ or ‘find -print0’ and ‘xargs -0’ which do the
same in order to reliably handle arbitrary file names (even those
containing blanks or other special characters).
