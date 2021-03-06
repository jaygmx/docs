---
title:  "csplit"
linkTitle::  "csplit"
weight: 100
description: >-
     csplit
---

# ‘csplit’: Split a file into context-determined pieces

‘csplit’ creates zero or more output files containing sections of INPUT
(standard input if INPUT is ‘-’).
Synopsis:

``` 
 csplit [OPTION]... INPUT PATTERN...
```

The contents of the output files are determined by the PATTERN
arguments, as detailed below. An error occurs if a PATTERN argument
refers to a nonexistent line of the input file (e.g., if no remaining
line matches a given regular expression). After every PATTERN has been
matched, any remaining input is copied into one last output file.

By default, ‘csplit’ prints the number of bytes written to each output
file after it has been created.

The types of pattern arguments are:

‘N’ Create an output file containing the input up to but not including
line N (a positive integer). If followed by a repeat count, also create
an output file containing the next N lines of the input file once for
each repeat.

‘/REGEXP/\[OFFSET\]’ Create an output file containing the current line
up to (but not including) the next line of the input file that contains
a match for REGEXP. The optional OFFSET is an integer. If it is given,
the input up to (but not including) the matching line plus or minus
OFFSET is put into the output file, and the line after that begins the
next section of input.

‘%REGEXP%\[OFFSET\]’ Like the previous type, except that it does not
create an output file, so that section of the input file is effectively
ignored.

‘{REPEAT-COUNT}’ Repeat the previous pattern REPEAT-COUNT additional
times. The REPEAT-COUNT can either be a positive integer or an asterisk,
meaning repeat as many times as necessary until the input is exhausted.

The output files’ names consist of a prefix (‘xx’ by default) followed
by a suffix. By default, the suffix is an ascending sequence of
two-digit decimal numbers from ‘00’ to ‘99’. In any case, concatenating
the output files in sorted order by file name produces the original
input file.

By default, if ‘csplit’ encounters an error or receives a hangup,
interrupt, quit, or terminate signal, it removes any output files that
it has created so far before it exits.

The program accepts the following options. Also see \*note Common
options::.

‘-f PREFIX’ ‘--prefix=PREFIX’ Use PREFIX as the output file name prefix.

‘-b FORMAT’ ‘--suffix-format=FORMAT’ Use FORMAT as the output file name
suffix. When this option is specified, the suffix string must include
exactly one ‘printf(3)’-style conversion specification, possibly
including format specification flags, a field width, a precision
specifications, or all of these kinds of modifiers. The format letter
must convert a binary unsigned integer argument to readable form. The
format letters ‘d’ and ‘i’ are aliases for ‘u’, and the ‘u’, ‘o’, ‘x’,
and ‘X’ conversions are allowed. The entire FORMAT is given (with the
current output file number) to ‘sprintf(3)’ to form the file name
suffixes for each of the individual output files in turn. If this option
is used, the ‘--digits’ option is ignored.

‘-n DIGITS’ ‘--digits=DIGITS’ Use output file names containing numbers
that are DIGITS digits long instead of the default 2.

‘-k’ ‘--keep-files’ Do not remove output files when errors are
encountered.

‘--suppress-matched’ Do not output lines matching the specified PATTERN.
I.e., suppress the boundary line from the start of the second and
subsequent splits.

‘-z’ ‘--elide-empty-files’ Suppress the generation of zero-length output
files. (In cases where the section delimiters of the input file are
supposed to mark the first lines of each of the sections, the first
output file will generally be a zero-length file unless you use this
option.) The output file sequence numbers always run consecutively
starting from 0, even when this option is specified.

‘-s’ ‘-q’ ‘--silent’ ‘--quiet’ Do not print counts of output file sizes.

An exit status of zero indicates success, and a nonzero value indicates
failure.

Here is an example of its usage. First, create an empty directory for
the exercise, and cd into it:

``` 
 $ mkdir d && cd d
```

Now, split the sequence of 1..14 on lines that end with 0 or 5:

``` 
 $ seq 14 | csplit - '/[05]$/' '{*}'
 8
 10
 15
```

Each number printed above is the size of an output file that csplit has
just created. List the names of those output files:

``` 
 $ ls
 xx00  xx01  xx02
```

Use ‘head’ to show their contents:

``` 
 $ head xx*
 ==> xx00 <==
 1
 2
 3
 4

 ==> xx01 <==
 5
 6
 7
 8
 9

 ==> xx02 <==
 10
 11
 12
 13
 14
```

Example of splitting input by empty lines:

``` 
 $ csplit --suppress-matched INPUT.TXT '/^$/' '{*}'
```
