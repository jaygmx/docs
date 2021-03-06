---
title:  "sort"
linkTitle::  "sort"
weight: 100
description: >-
     sort
---

# ‘sort’: Sort text files

‘sort’ sorts, merges, or compares all the lines from the given files, or
standard input if none are given or for a FILE of ‘-’. By default,
‘sort’ writes the results to standard output.
Synopsis:

``` 
 sort [OPTION]... [FILE]...
```

Many options affect how ‘sort’ compares lines; if the results are
unexpected, try the ‘--debug’ option to see what happened. A pair of
lines is compared as follows: ‘sort’ compares each pair of fields (see
‘--key’), in the order specified on the command line, according to the
associated ordering options, until a difference is found or no fields
are left. If no key fields are specified, ‘sort’ uses a default key of
the entire line. Finally, as a last resort when all keys compare equal,
‘sort’ compares entire lines as if no ordering options other than
‘--reverse’ (‘-r’) were specified. The ‘--stable’ (‘-s’) option
disables this “last-resort comparison” so that lines in which all fields
compare equal are left in their original relative order. The ‘--unique’
(‘-u’) option also disables the last-resort comparison.

Unless otherwise specified, all comparisons use the character collating
sequence specified by the ‘LC\_COLLATE’ locale.(1) A line’s trailing
newline is not part of the line for comparison purposes. If the final
byte of an input file is not a newline, GNU ‘sort’ silently supplies
one. GNU ‘sort’ (as specified for all GNU utilities) has no limit on
input line length or restrictions on bytes allowed within lines.

‘sort’ has three modes of operation: sort (the default), merge, and
check for sortedness. The following options change the operation mode:

‘-c’ ‘--check’ ‘--check=diagnose-first’ Check whether the given file is
already sorted: if it is not all sorted, print a diagnostic containing
the first out-of-order line and exit with a status of 1. Otherwise, exit
successfully. At most one input file can be given.

‘-C’ ‘--check=quiet’ ‘--check=silent’ Exit successfully if the given
file is already sorted, and exit with status 1 otherwise. At most one
input file can be given. This is like ‘-c’, except it does not print a
diagnostic.

‘-m’ ‘--merge’ Merge the given files by sorting them as a group. Each
input file must always be individually sorted. It always works to sort
instead of merge; merging is provided because it is faster, in the case
where it works.

Exit status:

``` 
 0 if no error occurred
 1 if invoked with ‘-c’ or ‘-C’ and the input is not sorted
 2 if an error occurred
```

If the environment variable ‘TMPDIR’ is set, ‘sort’ uses its value as
the directory for temporary files instead of ‘/tmp’. The
‘--temporary-directory’ (‘-T’) option in turn overrides the
environment variable.

The following options affect the ordering of output lines. They may be
specified globally or as part of a specific key field. If no key fields
are specified, global options apply to comparison of entire lines;
otherwise the global options are inherited by key fields that do not
specify any special options of their own. In pre-POSIX versions of
‘sort’, global options affect only later key fields, so portable
shell scripts should specify global options first.

‘-b’ ‘--ignore-leading-blanks’ Ignore leading blanks when finding sort
keys in each line. By default a blank is a space or a tab, but the
‘LC\_CTYPE’ locale can change this. Note blanks may be ignored by your
locale’s collating rules, but without this option they will be
significant for character positions specified in keys with the ‘-k’
option.

‘-d’ ‘--dictionary-order’ Sort in “phone directory” order: ignore all
characters except letters, digits and blanks when sorting. By default
letters and digits are those of ASCII and a blank is a space or a tab,
but the ‘LC\_CTYPE’ locale can change this.

‘-f’ ‘--ignore-case’ Fold lowercase characters into the equivalent
uppercase characters when comparing so that, for example, ‘b’ and ‘B’
sort as equal. The ‘LC\_CTYPE’ locale determines character types. When
used with ‘--unique’ those lower case equivalent lines are thrown away.
(There is currently no way to throw away the upper case equivalent
instead. (Any ‘--reverse’ given would only affect the final result,
after the throwing away.))

‘-g’ ‘--general-numeric-sort’ ‘--sort=general-numeric’ Sort numerically,
converting a prefix of each line to a long double-precision floating
point number. \*Note Floating point::. Do not report overflow,
underflow, or conversion errors. Use the following collating sequence:

``` 
    • Lines that do not start with numbers (all considered to be
      equal).
    • NaNs (“Not a Number” values, in IEEE floating point
      arithmetic) in a consistent but machine-dependent order.
    • Minus infinity.
    • Finite numbers in ascending numeric order (with -0 and +0
      equal).
    • Plus infinity.

 Use this option only if there is no alternative; it is much slower
 than ‘--numeric-sort’ (‘-n’) and it can lose information when
 converting to floating point.
```

‘-h’ ‘--human-numeric-sort’ ‘--sort=human-numeric’ Sort numerically,
first by numeric sign (negative, zero, or positive); then by SI suffix
(either empty, or ‘k’ or ‘K’, or one of ‘MGTPEZY’, in that order; \*note
Block size::); and finally by numeric value. For example, ‘1023M’ sorts
before ‘1G’ because ‘M’ (mega) precedes ‘G’ (giga) as an SI suffix. This
option sorts values that are consistently scaled to the nearest suffix,
regardless of whether suffixes denote powers of 1000 or 1024, and it
therefore sorts the output of any single invocation of the ‘df’, ‘du’,
or ‘ls’ commands that are invoked with their ‘--human-readable’ or
‘--si’ options. The syntax for numbers is the same as for the
‘--numeric-sort’ option; the SI suffix must immediately follow the
number. Note also the ‘numfmt’ command, which can be used to reformat
numbers to human format *after* the sort, thus often allowing sort to
operate on more accurate numbers.

‘-i’ ‘--ignore-nonprinting’ Ignore nonprinting characters. The
‘LC\_CTYPE’ locale determines character types. This option has no
effect if the stronger ‘--dictionary-order’ (‘-d’) option is also given.

‘-M’ ‘--month-sort’ ‘--sort=month’ An initial string, consisting of any
amount of blanks, followed by a month name abbreviation, is folded to
UPPER case and compared in the order ‘JAN’ \< ‘FEB’ \< ... \< ‘DEC’.
Invalid names compare low to valid names. The ‘LC\_TIME’ locale category
determines the month spellings. By default a blank is a space or a tab,
but the ‘LC\_CTYPE’ locale can change this.

‘-n’ ‘--numeric-sort’ ‘--sort=numeric’ Sort numerically. The number
begins each line and consists of optional blanks, an optional ‘-’ sign,
and zero or more digits possibly separated by thousands separators,
optionally followed by a decimal-point character and zero or more
digits. An empty number is treated as ‘0’. The ‘LC\_NUMERIC’ locale
specifies the decimal-point character and thousands separator. By
default a blank is a space or a tab, but the ‘LC\_CTYPE’ locale can
change this.

``` 
 Comparison is exact; there is no rounding error.

 Neither a leading ‘+’ nor exponential notation is recognized.  To
 compare such strings numerically, use the ‘--general-numeric-sort’
 (‘-g’) option.
```

‘-V’ ‘--version-sort’ Sort by version name and number. It behaves like a
standard sort, except that each sequence of decimal digits is treated
numerically as an index/version number. (\*Note Details about version
sort::.)

‘-r’ ‘--reverse’ Reverse the result of comparison, so that lines with
greater key values appear earlier in the output instead of later.

‘-R’ ‘--random-sort’ ‘--sort=random’ Sort by hashing the input keys and
then sorting the hash values. Choose the hash function at random,
ensuring that it is free of collisions so that differing keys have
differing hash values. This is like a random permutation of the inputs
(\*note shuf invocation::), except that keys with the same value sort
together.

``` 
 If multiple random sort fields are specified, the same random hash
 function is used for all fields.  To use different random hash
 functions for different fields, you can invoke ‘sort’ more than
 once.

 The choice of hash function is affected by the ‘--random-source’
 option.
```

Other options are:

‘--compress-program=PROG’ Compress any temporary files with the program
PROG.

``` 
 With no arguments, PROG must compress standard input to standard
 output, and when given the ‘-d’ option it must decompress standard
 input to standard output.

 Terminate with an error if PROG exits with nonzero status.

 White space and the backslash character should not appear in PROG;
 they are reserved for future use.
```

‘--files0-from=FILE’ Disallow processing files named on the command
line, and instead process those named in file FILE; each name being
terminated by a zero byte (ASCII NUL). This is useful when the list of
file names is so long that it may exceed a command line length
limitation. In such cases, running ‘sort’ via ‘xargs’ is undesirable
because it splits the list into pieces and makes ‘sort’ print sorted
output for each sublist rather than for the entire list. One way to
produce a list of ASCII NUL terminated file names is with GNU ‘find’,
using its ‘-print0’ predicate. If FILE is ‘-’ then the ASCII NUL
terminated file names are read from standard input.

‘-k POS1\[,POS2\]’ ‘--key=POS1\[,POS2\]’ Specify a sort field that
consists of the part of the line between POS1 and POS2 (or the end of
the line, if POS2 is omitted), *inclusive*.

``` 
 In its simplest form POS specifies a field number (starting with
 1), with fields being separated by runs of blank characters, and by
 default those blanks being included in the comparison at the start
 of each field.  To adjust the handling of blank characters see the
 ‘-b’ and ‘-t’ options.

 More generally, each POS has the form ‘F[.C][OPTS]’, where F is the
 number of the field to use, and C is the number of the first
 character from the beginning of the field.  Fields and character
 positions are numbered starting with 1; a character position of
 zero in POS2 indicates the field’s last character.  If ‘.C’ is
 omitted from POS1, it defaults to 1 (the beginning of the field);
 if omitted from POS2, it defaults to 0 (the end of the field).
 OPTS are ordering options, allowing individual keys to be sorted
 according to different rules; see below for details.  Keys can span
 multiple fields.

 Example: To sort on the second field, use ‘--key=2,2’ (‘-k 2,2’).
 See below for more notes on keys and more examples.  See also the
 ‘--debug’ option to help determine the part of the line being used
 in the sort.
```

‘--debug’ Highlight the portion of each line used for sorting. Also
issue warnings about questionable usage to stderr.

‘--batch-size=NMERGE’ Merge at most NMERGE inputs at once.

``` 
 When ‘sort’ has to merge more than NMERGE inputs, it merges them in
 groups of NMERGE, saving the result in a temporary file, which is
 then used as an input in a subsequent merge.

 A large value of NMERGE may improve merge performance and decrease
 temporary storage utilization at the expense of increased memory
 usage and I/O.  Conversely a small value of NMERGE may reduce
 memory requirements and I/O at the expense of temporary storage
 consumption and merge performance.

 The value of NMERGE must be at least 2.  The default value is
 currently 16, but this is implementation-dependent and may change
 in the future.

 The value of NMERGE may be bounded by a resource limit for open
 file descriptors.  The commands ‘ulimit -n’ or ‘getconf OPEN_MAX’
 may display limits for your systems; these limits may be modified
 further if your program already has some files open, or if the
 operating system has other limits on the number of open files.  If
 the value of NMERGE exceeds the resource limit, ‘sort’ silently
 uses a smaller value.
```

‘-o OUTPUT-FILE’ ‘--output=OUTPUT-FILE’ Write output to OUTPUT-FILE
instead of standard output. Normally, ‘sort’ reads all input before
opening OUTPUT-FILE, so you can sort a file in place by using commands
like ‘sort -o F F’ and ‘cat F | sort -o F’. However, it is often safer
to output to an otherwise-unused file, as data may be lost if the system
crashes or ‘sort’ encounters an I/O or other serious error while a file
is being sorted in place. Also, ‘sort’ with ‘--merge’ (‘-m’) can open
the output file before reading all input, so a command like ‘cat F |
sort -m -o F - G’ is not safe as ‘sort’ might start writing ‘F’ before
‘cat’ is done reading it.

``` 
 On newer systems, ‘-o’ cannot appear after an input file if
 ‘POSIXLY_CORRECT’ is set, e.g., ‘sort F -o F’.  Portable scripts
 should specify ‘-o OUTPUT-FILE’ before any input files.
```

‘--random-source=FILE’ Use FILE as a source of random data used to
determine which random hash function to use with the ‘-R’ option. \*Note
Random sources::.

‘-s’ ‘--stable’

``` 
 Make ‘sort’ stable by disabling its last-resort comparison.  This
 option has no effect if no fields or global ordering options other
 than ‘--reverse’ (‘-r’) are specified.
```

‘-S SIZE’ ‘--buffer-size=SIZE’ Use a main-memory sort buffer of the
given SIZE. By default, SIZE is in units of 1024 bytes. Appending ‘%’
causes SIZE to be interpreted as a percentage of physical memory.
Appending ‘K’ multiplies SIZE by 1024 (the default), ‘M’ by 1,048,576,
‘G’ by 1,073,741,824, and so on for ‘T’, ‘P’, ‘E’, ‘Z’, and ‘Y’.
Appending ‘b’ causes SIZE to be interpreted as a byte count, with no
multiplication.

``` 
 This option can improve the performance of ‘sort’ by causing it to
 start with a larger or smaller sort buffer than the default.
 However, this option affects only the initial buffer size.  The
 buffer grows beyond SIZE if ‘sort’ encounters input lines larger
 than SIZE.
```

‘-t SEPARATOR’ ‘--field-separator=SEPARATOR’ Use character SEPARATOR as
the field separator when finding the sort keys in each line. By default,
fields are separated by the empty string between a non-blank character
and a blank character. By default a blank is a space or a tab, but the
‘LC\_CTYPE’ locale can change this.

``` 
 That is, given the input line ‘ foo bar’, ‘sort’ breaks it into
 fields ‘ foo’ and ‘ bar’.  The field separator is not considered to
 be part of either the field preceding or the field following, so
 with ‘sort -t " "’ the same input line has three fields: an empty
 field, ‘foo’, and ‘bar’.  However, fields that extend to the end of
 the line, as ‘-k 2’, or fields consisting of a range, as ‘-k 2,3’,
 retain the field separators present between the endpoints of the
 range.

 To specify ASCII NUL as the field separator, use the two-character
 string ‘\0’, e.g., ‘sort -t '\0'’.
```

‘-T TEMPDIR’ ‘--temporary-directory=TEMPDIR’ Use directory TEMPDIR to
store temporary files, overriding the ‘TMPDIR’ environment variable. If
this option is given more than once, temporary files are stored in all
the directories given. If you have a large sort or merge that is
I/O-bound, you can often improve performance by using this option to
specify directories on different disks and controllers.

‘--parallel=N’ Set the number of sorts run in parallel to N. By default,
N is set to the number of available processors, but limited to 8, as
there are diminishing performance gains after that. Note also that using
N threads increases the memory usage by a factor of log N. Also see
\*note nproc invocation::.

‘-u’ ‘--unique’

``` 
 Normally, output only the first of a sequence of lines that compare
 equal.  For the ‘--check’ (‘-c’ or ‘-C’) option, check that no pair
 of consecutive lines compares equal.

 This option also disables the default last-resort comparison.

 The commands ‘sort -u’ and ‘sort | uniq’ are equivalent, but this
 equivalence does not extend to arbitrary ‘sort’ options.  For
 example, ‘sort -n -u’ inspects only the value of the initial
 numeric string when checking for uniqueness, whereas ‘sort -n |
 uniq’ inspects the entire line.  *Note uniq invocation::.
```

‘-z’ ‘--zero-terminated’ Delimit items with a zero byte rather than a
newline (ASCII LF). I.e., treat input as items separated by ASCII NUL
and terminate output items with ASCII NUL. This option can be useful in
conjunction with ‘perl -0’ or ‘find -print0’ and ‘xargs -0’ which do the
same in order to reliably handle arbitrary file names (even those
containing blanks or other special characters).

Historical (BSD and System V) implementations of ‘sort’ have differed in
their interpretation of some options, particularly ‘-b’, ‘-f’, and ‘-n’.
GNU sort follows the POSIX behavior, which is usually (but not always\!)
like the System V behavior. According to POSIX, ‘-n’ no longer implies
‘-b’. For consistency, ‘-M’ has been changed in the same way. This may
affect the meaning of character positions in field specifications in
obscure cases. The only fix is to add an explicit ‘-b’.

A position in a sort field specified with ‘-k’ may have any of the
option letters ‘MbdfghinRrV’ appended to it, in which case no global
ordering options are inherited by that particular field. The ‘-b’ option
may be independently attached to either or both of the start and end
positions of a field specification, and if it is inherited from the
global options it will be attached to both. If input lines can contain
leading or adjacent blanks and ‘-t’ is not used, then ‘-k’ is typically
combined with ‘-b’ or an option that implicitly ignores leading blanks
(‘Mghn’) as otherwise the varying numbers of leading blanks in fields
can cause confusing results.

If the start position in a sort field specifier falls after the end of
the line or after the end field, the field is empty. If the ‘-b’ option
was specified, the ‘.C’ part of a field specification is counted from
the first nonblank character of the field.

On systems not conforming to POSIX 1003.1-2001, ‘sort’ supports a
traditional origin-zero syntax ‘+POS1 \[-POS2\]’ for specifying sort
keys. The traditional command ‘sort +A.X -B.Y’ is equivalent to ‘sort -k
A+1.X+1,B’ if Y is ‘0’ or absent, otherwise it is equivalent to ‘sort -k
A+1.X+1,B+1.Y’.

This traditional behavior can be controlled with the ‘\_POSIX2\_VERSION’
environment variable (\*note Standards conformance::); it can also be
enabled when ‘POSIXLY\_CORRECT’ is not set by using the traditional
syntax with ‘-POS2’ present.

Scripts intended for use on standard hosts should avoid traditional
syntax and should use ‘-k’ instead. For example, avoid ‘sort +2’, since
it might be interpreted as either ‘sort ./+2’ or ‘sort -k 3’. If your
script must also run on hosts that support only the traditional syntax,
it can use a test like ‘if sort -k 1 \</dev/null \>/dev/null 2\>&1; then
...’ to decide which syntax to use.

Here are some examples to illustrate various combinations of options.

• Sort in descending (reverse) numeric order.

``` 
      sort -n -r
```

• Run no more than 4 sorts concurrently, using a buffer size of 10M.

``` 
      sort --parallel=4 -S 10M
```

• Sort alphabetically, omitting the first and second fields and the
blanks at the start of the third field. This uses a single key composed
of the characters beginning at the start of the first nonblank character
in field three and extending to the end of each line.

``` 
      sort -k 3b
```

• Sort numerically on the second field and resolve ties by sorting
alphabetically on the third and fourth characters of field five. Use ‘:’
as the field delimiter.

``` 
      sort -t : -k 2,2n -k 5.3,5.4

 Note that if you had written ‘-k 2n’ instead of ‘-k 2,2n’ ‘sort’
 would have used all characters beginning in the second field and
 extending to the end of the line as the primary _numeric_ key.  For
 the large majority of applications, treating keys spanning more
 than one field as numeric will not do what you expect.

 Also note that the ‘n’ modifier was applied to the field-end
 specifier for the first key.  It would have been equivalent to
 specify ‘-k 2n,2’ or ‘-k 2n,2n’.  All modifiers except ‘b’ apply to
 the associated _field_, regardless of whether the modifier
 character is attached to the field-start and/or the field-end part
 of the key specifier.
```

• Sort the password file on the fifth field and ignore any leading
blanks. Sort lines with equal values in field five on the numeric user
ID in field three. Fields are separated by ‘:’.

``` 
      sort -t : -k 5b,5 -k 3,3n /etc/passwd
      sort -t : -n -k 5b,5 -k 3,3 /etc/passwd
      sort -t : -b -k 5,5 -k 3,3n /etc/passwd

 These three commands have equivalent effect.  The first specifies
 that the first key’s start position ignores leading blanks and the
 second key is sorted numerically.  The other two commands rely on
 global options being inherited by sort keys that lack modifiers.
 The inheritance works in this case because ‘-k 5b,5b’ and ‘-k 5b,5’
 are equivalent, as the location of a field-end lacking a ‘.C’
 character position is not affected by whether initial blanks are
 skipped.
```

• Sort a set of log files, primarily by IPv4 address and secondarily by
timestamp. If two lines’ primary and secondary keys are identical,
output the lines in the same order that they were input. The log files
contain lines that look like this:

``` 
      4.150.156.3 - - [01/Apr/2004:06:31:51 +0000] message 1
      211.24.3.231 - - [24/Apr/2004:20:17:39 +0000] message 2

 Fields are separated by exactly one space.  Sort IPv4 addresses
 lexicographically, e.g., 212.61.52.2 sorts before 212.129.233.201
 because 61 is less than 129.

      sort -s -t ' ' -k 4.9n -k 4.5M -k 4.2n -k 4.14,4.21 file*.log |
      sort -s -t '.' -k 1,1n -k 2,2n -k 3,3n -k 4,4n

 This example cannot be done with a single ‘sort’ invocation, since
 IPv4 address components are separated by ‘.’ while dates come just
 after a space.  So it is broken down into two invocations of
 ‘sort’: the first sorts by timestamp and the second by IPv4
 address.  The timestamp is sorted by year, then month, then day,
 and finally by hour-minute-second field, using ‘-k’ to isolate each
 field.  Except for hour-minute-second there’s no need to specify
 the end of each key field, since the ‘n’ and ‘M’ modifiers sort
 based on leading prefixes that cannot cross field boundaries.  The
 IPv4 addresses are sorted lexicographically.  The second sort uses
 ‘-s’ so that ties in the primary key are broken by the secondary
 key; the first sort uses ‘-s’ so that the combination of the two
 sorts is stable.
```

• Generate a tags file in case-insensitive sorted order.

``` 
      find src -type f -print0 | sort -z -f | xargs -0 etags --append

 The use of ‘-print0’, ‘-z’, and ‘-0’ in this case means that file
 names that contain blanks or other special characters are not
 broken up by the sort operation.
```

• Use the common DSU, Decorate Sort Undecorate idiom to sort lines
according to their length.

``` 
      awk '{print length, $0}' /etc/passwd | sort -n | cut -f2- -d' '

 In general this technique can be used to sort data that the ‘sort’
 command does not support, or is inefficient at, sorting directly.
```

• Shuffle a list of directories, but preserve the order of files within
each directory. For instance, one could use this to generate a music
playlist in which albums are shuffled but the songs of each album are
played in order.

``` 
      ls */* | sort -t / -k 1,1R -k 2,2
```

\---------- Footnotes ----------

(1) If you use a non-POSIX locale (e.g., by setting ‘LC\_ALL’ to
‘en\_US’), then ‘sort’ may produce output that is sorted differently
than you’re accustomed to. In that case, set the ‘LC\_ALL’ environment
variable to ‘C’. Note that setting only ‘LC\_COLLATE’ has two problems.
First, it is ineffective if ‘LC\_ALL’ is also set. Second, it has
undefined behavior if ‘LC\_CTYPE’ (or ‘LANG’, if ‘LC\_CTYPE’ is unset)
is set to an incompatible value. For example, you get undefined behavior
if ‘LC\_CTYPE’ is ‘ja\_JP.PCK’ but ‘LC\_COLLATE’ is ‘en\_US.UTF-8’.
