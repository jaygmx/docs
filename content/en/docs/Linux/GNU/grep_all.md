---
title: "Grep"
linkTitle: "Grep"
weight: 100
description: >-
     GNU Grep
---

# GNU Grep 3.7

<div id="Top" class="top">

<div class="header">

Next: <a href="#Introduction" accesskey="n" rel="next">Introduction</a>,
Up: <a href="/manual" accesskey="u" rel="up">(dir)</a>  
\[<a href="#SEC_Contents" rel="contents"
title="Table of contents">Contents</a>\]\[<a href="#Index" rel="index" title="Index">Index</a>\]

</div>

<span id="grep"></span>

# grep

`grep` prints lines that contain a match for one or more patterns.

This manual is for version 3.7 of GNU Grep.

This manual is for `grep`, a pattern matching engine.

<div id="SEC_Contents" class="Contents_element">

## Table of Contents

<div class="contents">

-   <a href="#Introduction" id="toc-Introduction-1">1 Introduction</a>
-   <a href="#Invoking" id="toc-Invoking-grep">2 Invoking
    <code>grep</code></a>
    -   <a href="#Command_002dline-Options"
        id="toc-Command_002dline-Options-1">2.1 Command-line Options</a>
        -   <a href="#Generic-Program-Information"
            id="toc-Generic-Program-Information-1">2.1.1 Generic Program
            Information</a>
        -   <a href="#Matching-Control" id="toc-Matching-Control-1">2.1.2 Matching
            Control</a>
        -   <a href="#General-Output-Control"
            id="toc-General-Output-Control-1">2.1.3 General Output Control</a>
        -   <a href="#Output-Line-Prefix-Control"
            id="toc-Output-Line-Prefix-Control-1">2.1.4 Output Line Prefix
            Control</a>
        -   <a href="#Context-Line-Control" id="toc-Context-Line-Control-1">2.1.5
            Context Line Control</a>
        -   <a href="#File-and-Directory-Selection"
            id="toc-File-and-Directory-Selection-1">2.1.6 File and Directory
            Selection</a>
        -   <a href="#Other-Options" id="toc-Other-Options-1">2.1.7 Other
            Options</a>
    -   <a href="#Environment-Variables" id="toc-Environment-Variables-1">2.2
        Environment Variables</a>
    -   <a href="#Exit-Status" id="toc-Exit-Status-1">2.3 Exit Status</a>
    -   <a href="#grep-Programs" id="toc-grep-Programs-1">2.4 <code>grep</code>
        Programs</a>
-   <a href="#Regular-Expressions" id="toc-Regular-Expressions-1">3 Regular
    Expressions</a>
    -   <a href="#Fundamental-Structure" id="toc-Fundamental-Structure-1">3.1
        Fundamental Structure</a>
    -   <a href="#Character-Classes-and-Bracket-Expressions"
        id="toc-Character-Classes-and-Bracket-Expressions-1">3.2 Character
        Classes and Bracket Expressions</a>
    -   <a href="#The-Backslash-Character-and-Special-Expressions"
        id="toc-The-Backslash-Character-and-Special-Expressions-1">3.3 The
        Backslash Character and Special Expressions</a>
    -   <a href="#Anchoring" id="toc-Anchoring-1">3.4 Anchoring</a>
    -   <a href="#Back_002dreferences-and-Subexpressions"
        id="toc-Back_002dreferences-and-Subexpressions-1">3.5 Back-references
        and Subexpressions</a>
    -   <a href="#Basic-vs-Extended"
        id="toc-Basic-vs-Extended-Regular-Expressions">3.6 Basic vs Extended
        Regular Expressions</a>
    -   <a href="#Character-Encoding" id="toc-Character-Encoding-1">3.7
        Character Encoding</a>
    -   <a href="#Matching-Non_002dASCII"
        id="toc-Matching-Non_002dASCII-and-Non_002dprintable-Characters">3.8
        Matching Non-ASCII and Non-printable Characters</a>
-   <a href="#Usage" id="toc-Usage-1">4 Usage</a>
-   <a href="#Performance" id="toc-Performance-1">5 Performance</a>
-   <a href="#Reporting-Bugs" id="toc-Reporting-bugs">6 Reporting bugs</a>
    -   <a href="#Known-Bugs" id="toc-Known-Bugs-1">6.1 Known Bugs</a>
-   <a href="#Copying" id="toc-Copying-1">7 Copying</a>
    -   <a href="#GNU-Free-Documentation-License"
        id="toc-GNU-Free-Documentation-License-1">7.1 GNU Free Documentation
        License</a>
-   <a href="#Index" id="toc-Index-1" rel="index">Index</a>

</div>

</div>

------------------------------------------------------------------------

<div id="Introduction" class="chapter">

<div class="header">

Next: <a href="#Invoking" accesskey="n" rel="next">Invoking
<code>grep</code></a>, Previous:
<a href="#Top" accesskey="p" rel="prev">grep</a>, Up:
<a href="#Top" accesskey="u" rel="up">grep</a>  
\[<a href="#SEC_Contents" rel="contents"
title="Table of contents">Contents</a>\]\[<a href="#Index" rel="index" title="Index">Index</a>\]

</div>

<span id="Introduction-1"></span>

## 1 Introduction

<span id="index-searching-for-patterns"></span>

Given one or more patterns, `grep` searches input files for matches to
the patterns. When it finds a match in a line, it copies the line to
standard output (by default), or produces whatever other sort of output
you have requested with options.

Though `grep` expects to do the matching on text, it has no limits on
input line length other than available memory, and it can match
arbitrary characters within a line. If the final byte of an input file
is not a newline, `grep` silently supplies one. Since newline is also a
separator for the list of patterns, there is no way to match newline
characters in a text.

------------------------------------------------------------------------

</div>

<div id="Invoking" class="chapter">

<div class="header">

Next: <a href="#Regular-Expressions" accesskey="n" rel="next">Regular
Expressions</a>, Previous:
<a href="#Introduction" accesskey="p" rel="prev">Introduction</a>, Up:
<a href="#Top" accesskey="u" rel="up">grep</a>  
\[<a href="#SEC_Contents" rel="contents"
title="Table of contents">Contents</a>\]\[<a href="#Index" rel="index" title="Index">Index</a>\]

</div>

<span id="Invoking-grep"></span>

## 2 Invoking `grep`

The general synopsis of the `grep` command line is

<div class="example">

``` example
grep [option...] [patterns] [file...]
```

</div>

There can be zero or more `option` arguments, and zero or more `file`
arguments. The `patterns` argument contains one or more patterns
separated by newlines, and is omitted when patterns are given via the
‘`-e patterns`’ or ‘`-f file`’ options. Typically `patterns` should be
quoted when `grep` is used in a shell command.

-   <a href="#Command_002dline-Options" accesskey="1">Command-line
    Options</a>
-   <a href="#Environment-Variables" accesskey="2">Environment Variables</a>
-   <a href="#Exit-Status" accesskey="3">Exit Status</a>
-   <a href="#grep-Programs" accesskey="4"><code>grep</code> Programs</a>

------------------------------------------------------------------------

<div id="Command_002dline-Options" class="section">

<div class="header">

Next:
<a href="#Environment-Variables" accesskey="n" rel="next">Environment
Variables</a>, Up: <a href="#Invoking" accesskey="u" rel="up">Invoking
<code>grep</code></a>   \[<a href="#SEC_Contents" rel="contents"
title="Table of contents">Contents</a>\]\[<a href="#Index" rel="index" title="Index">Index</a>\]

</div>

<span id="Command_002dline-Options-1"></span>

### 2.1 Command-line Options

`grep` comes with a rich set of options: some from POSIX and some being
GNU extensions. Long option names are always a GNU extension, even for
options that are from POSIX specifications. Options that are specified
by POSIX, under their short names, are explicitly marked as such to
facilitate POSIX-portable programming. A few option names are provided
for compatibility with older or more exotic implementations.

Several additional options control which variant of the `grep` matching
engine is used. See [`grep` Programs](#grep-Programs).

-   <a href="#Generic-Program-Information" accesskey="1">Generic Program
    Information</a>
-   <a href="#Matching-Control" accesskey="2">Matching Control</a>
-   <a href="#General-Output-Control" accesskey="3">General Output
    Control</a>
-   <a href="#Output-Line-Prefix-Control" accesskey="4">Output Line Prefix
    Control</a>
-   <a href="#Context-Line-Control" accesskey="5">Context Line Control</a>
-   <a href="#File-and-Directory-Selection" accesskey="6">File and Directory
    Selection</a>
-   <a href="#Other-Options" accesskey="7">Other Options</a>

------------------------------------------------------------------------

<div id="Generic-Program-Information" class="subsection">

<div class="header">

Next: <a href="#Matching-Control" accesskey="n" rel="next">Matching
Control</a>, Up:
<a href="#Command_002dline-Options" accesskey="u" rel="up">Command-line
Options</a>   \[<a href="#SEC_Contents" rel="contents"
title="Table of contents">Contents</a>\]\[<a href="#Index" rel="index" title="Index">Index</a>\]

</div>

<span id="Generic-Program-Information-1"></span>

#### 2.1.1 Generic Program Information

`--help` <a href="#index-_002d_002dhelp" class="copiable-anchor">¶</a>  
<span id="index-usage-summary_002c-printing"></span>

Print a usage message briefly summarizing the command-line options and
the bug-reporting address, then exit.

`-V` <a href="#index-_002dV" class="copiable-anchor">¶</a>  
`--version`  
<span id="index-_002d_002dversion"></span> <span
id="index-version_002c-printing"></span>

Print the version number of `grep` to the standard output stream. This
version number should be included in all bug reports.

------------------------------------------------------------------------

</div>

<div id="Matching-Control" class="subsection">

<div class="header">

Next: <a href="#General-Output-Control" accesskey="n" rel="next">General
Output Control</a>, Previous:
<a href="#Generic-Program-Information" accesskey="p" rel="prev">Generic
Program Information</a>, Up:
<a href="#Command_002dline-Options" accesskey="u" rel="up">Command-line
Options</a>   \[<a href="#SEC_Contents" rel="contents"
title="Table of contents">Contents</a>\]\[<a href="#Index" rel="index" title="Index">Index</a>\]

</div>

<span id="Matching-Control-1"></span>

#### 2.1.2 Matching Control

`-e patterns` <a href="#index-_002de" class="copiable-anchor">¶</a>  
`--regexp=patterns`  
<span id="index-_002d_002dregexp_003dpatterns"></span> <span
id="index-patterns-option"></span>

Use `patterns` as one or more patterns; newlines within `patterns`
separate each pattern from the next. If this option is used multiple
times or is combined with the `-f` (`--file`) option, search for all
patterns given. Typically `patterns` should be quoted when `grep` is
used in a shell command. (`-e` is specified by POSIX.)

`-f file` <a href="#index-_002df" class="copiable-anchor">¶</a>  
`--file=file`  
<span id="index-_002d_002dfile"></span> <span
id="index-patterns-from-file"></span>

Obtain patterns from `file`, one per line. If this option is used
multiple times or is combined with the `-e` (`--regexp`) option, search
for all patterns given. The empty file contains zero patterns, and
therefore matches nothing. (`-f` is specified by POSIX.)

`-i` <a href="#index-_002di" class="copiable-anchor">¶</a>  
`-y`  
`--ignore-case`  
<span id="index-_002dy"></span> <span
id="index-_002d_002dignore_002dcase"></span> <span
id="index-case-insensitive-search"></span>

Ignore case distinctions in patterns and input data, so that characters
that differ only in case match each other. Although this is
straightforward when letters differ in case only via lowercase-uppercase
pairs, the behavior is unspecified in other situations. For example,
uppercase “S” has an unusual lowercase counterpart “ſ” (Unicode
character U+017F, LATIN SMALL LETTER LONG S) in many locales, and it is
unspecified whether this unusual character matches “S” or “s” even
though uppercasing it yields “S”. Another example: the lowercase German
letter “ß” (U+00DF, LATIN SMALL LETTER SHARP S) is normally capitalized
as the two-character string “SS” but it does not match “SS”, and it
might not match the uppercase letter “ẞ” (U+1E9E, LATIN CAPITAL LETTER
SHARP S) even though lowercasing the latter yields the former.

`-y` is an obsolete synonym that is provided for compatibility. (`-i` is
specified by POSIX.)

`--no-ignore-case` <a href="#index-_002d_002dno_002dignore_002dcase"
class="copiable-anchor">¶</a>  
Do not ignore case distinctions in patterns and input data. This is the
default. This option is useful for passing to shell scripts that already
use `-i`, in order to cancel its effects because the two options
override each other.

`-v` <a href="#index-_002dv" class="copiable-anchor">¶</a>  
`--invert-match`  
<span id="index-_002d_002dinvert_002dmatch"></span> <span
id="index-invert-matching"></span> <span
id="index-print-non_002dmatching-lines"></span>

Invert the sense of matching, to select non-matching lines. (`-v` is
specified by POSIX.)

`-w` <a href="#index-_002dw" class="copiable-anchor">¶</a>  
`--word-regexp`  
<span id="index-_002d_002dword_002dregexp"></span> <span
id="index-matching-whole-words"></span>

Select only those lines containing matches that form whole words. The
test is that the matching substring must either be at the beginning of
the line, or preceded by a non-word constituent character. Similarly, it
must be either at the end of the line or followed by a non-word
constituent character. Word constituent characters are letters, digits,
and the underscore. This option has no effect if `-x` is also specified.

Because the `-w` option can match a substring that does not begin and
end with word constituents, it differs from surrounding a regular
expression with ‘`\<`’ and ‘`\>`’. For example, although ‘`grep -w @`’
matches a line containing only ‘`@`’, ‘`grep '\<@\>'`’ cannot match any
line because ‘`@`’ is not a word constituent. See [The Backslash
Character and Special
Expressions](#The-Backslash-Character-and-Special-Expressions).

`-x` <a href="#index-_002dx" class="copiable-anchor">¶</a>  
`--line-regexp`  
<span id="index-_002d_002dline_002dregexp"></span> <span
id="index-match-the-whole-line"></span>

Select only those matches that exactly match the whole line. For regular
expression patterns, this is like parenthesizing each pattern and then
surrounding it with ‘`^`’ and ‘`$`’. (`-x` is specified by POSIX.)

------------------------------------------------------------------------

</div>

<div id="General-Output-Control" class="subsection">

<div class="header">

Next:
<a href="#Output-Line-Prefix-Control" accesskey="n" rel="next">Output
Line Prefix Control</a>, Previous:
<a href="#Matching-Control" accesskey="p" rel="prev">Matching
Control</a>, Up:
<a href="#Command_002dline-Options" accesskey="u" rel="up">Command-line
Options</a>   \[<a href="#SEC_Contents" rel="contents"
title="Table of contents">Contents</a>\]\[<a href="#Index" rel="index" title="Index">Index</a>\]

</div>

<span id="General-Output-Control-1"></span>

#### 2.1.3 General Output Control

`-c` <a href="#index-_002dc" class="copiable-anchor">¶</a>  
`--count`  
<span id="index-_002d_002dcount"></span> <span
id="index-counting-lines"></span>

Suppress normal output; instead print a count of matching lines for each
input file. With the `-v` (`--invert-match`) option, count non-matching
lines. (`-c` is specified by POSIX.)

`--color[=WHEN]` <a href="#index-_002d_002dcolor" class="copiable-anchor">¶</a>  
`--colour[=WHEN]`  
<span id="index-_002d_002dcolour"></span> <span
id="index-highlight_002c-color_002c-colour"></span>

Surround the matched (non-empty) strings, matching lines, context lines,
file names, line numbers, byte offsets, and separators (for fields and
groups of context lines) with escape sequences to display them in color
on the terminal. The colors are defined by the environment variable
`GREP_COLORS` and default to
‘`ms=01;31:mc=01;31:sl=:cx=:fn=35:ln=32:bn=32:se=36`’ for bold red
matched text, magenta file names, green line numbers, green byte
offsets, cyan separators, and default terminal colors otherwise. The
deprecated environment variable `GREP_COLOR` is still supported, but its
setting does not have priority; it defaults to ‘`01;31`’ (bold red)
which only covers the color for matched text. `WHEN` is ‘`never`’,
‘`always`’, or ‘`auto`’.

`-L` <a href="#index-_002dL" class="copiable-anchor">¶</a>  
`--files-without-match`  
<span id="index-_002d_002dfiles_002dwithout_002dmatch"></span> <span
id="index-files-which-don_0027t-match"></span>

Suppress normal output; instead print the name of each input file from
which no output would normally have been printed.

`-l` <a href="#index-_002dl" class="copiable-anchor">¶</a>  
`--files-with-matches`  
<span id="index-_002d_002dfiles_002dwith_002dmatches"></span> <span
id="index-names-of-matching-files"></span>

Suppress normal output; instead print the name of each input file from
which output would normally have been printed. Scanning each input file
stops upon first match. (`-l` is specified by POSIX.)

`-m num` <a href="#index-_002dm" class="copiable-anchor">¶</a>  
`--max-count=num`  
<span id="index-_002d_002dmax_002dcount"></span> <span
id="index-max_002dcount"></span>

Stop after the first `num` selected lines. If the input is standard
input from a regular file, and `num` selected lines are output, `grep`
ensures that the standard input is positioned just after the last
selected line before exiting, regardless of the presence of trailing
context lines. This enables a calling process to resume a search. For
example, the following shell script makes use of it:

<div class="example">

``` example
while grep -m 1 'PATTERN'
do
  echo xxxx
done < FILE
```

</div>

But the following probably will not work because a pipe is not a regular
file:

<div class="example">

``` example
# This probably will not work.
cat FILE |
while grep -m 1 'PATTERN'
do
  echo xxxx
done
```

</div>

<span id="index-context-lines"></span>

When `grep` stops after `num` selected lines, it outputs any trailing
context lines. When the `-c` or `--count` option is also used, `grep`
does not output a count greater than `num`. When the `-v` or
`--invert-match` option is also used, `grep` stops after outputting
`num` non-matching lines.

`-o` <a href="#index-_002do" class="copiable-anchor">¶</a>  
`--only-matching`  
<span id="index-_002d_002donly_002dmatching"></span> <span
id="index-only-matching"></span>

Print only the matched (non-empty) parts of matching lines, with each
such part on a separate output line. Output lines use the same
delimiters as input, and delimiters are null bytes if `-z`
(`--null-data`) is also used (see [Other Options](#Other-Options)).

`-q` <a href="#index-_002dq" class="copiable-anchor">¶</a>  
`--quiet`  
`--silent`  
<span id="index-_002d_002dquiet"></span> <span
id="index-_002d_002dsilent"></span> <span
id="index-quiet_002c-silent"></span>

Quiet; do not write anything to standard output. Exit immediately with
zero status if any match is found, even if an error was detected. Also
see the `-s` or `--no-messages` option. (`-q` is specified by POSIX.)

`-s` <a href="#index-_002ds" class="copiable-anchor">¶</a>  
`--no-messages`  
<span id="index-_002d_002dno_002dmessages"></span> <span
id="index-suppress-error-messages"></span>

Suppress error messages about nonexistent or unreadable files.
Portability note: unlike GNU `grep`, 7th Edition Unix `grep` did not
conform to POSIX, because it lacked `-q` and its `-s` option behaved
like GNU `grep`’s `-q`
option.<a href="#FOOT1" id="DOCF1"><sup>1</sup></a> USG-style `grep`
also lacked `-q` but its `-s` option behaved like GNU `grep`’s. Portable
shell scripts should avoid both `-q` and `-s` and should redirect
standard and error output to `/dev/null` instead. (`-s` is specified by
POSIX.)

------------------------------------------------------------------------

</div>

<div id="Output-Line-Prefix-Control" class="subsection">

<div class="header">

Next:
<a href="#Context-Line-Control" accesskey="n" rel="next">Context Line
Control</a>, Previous:
<a href="#General-Output-Control" accesskey="p" rel="prev">General
Output Control</a>, Up:
<a href="#Command_002dline-Options" accesskey="u" rel="up">Command-line
Options</a>   \[<a href="#SEC_Contents" rel="contents"
title="Table of contents">Contents</a>\]\[<a href="#Index" rel="index" title="Index">Index</a>\]

</div>

<span id="Output-Line-Prefix-Control-1"></span>

#### 2.1.4 Output Line Prefix Control

When several prefix fields are to be output, the order is always file
name, line number, and byte offset, regardless of the order in which
these options were specified.

`-b` <a href="#index-_002db" class="copiable-anchor">¶</a>  
`--byte-offset`  
<span id="index-_002d_002dbyte_002doffset"></span> <span
id="index-byte-offset"></span>

Print the 0-based byte offset within the input file before each line of
output. If `-o` (`--only-matching`) is specified, print the offset of
the matching part itself.

`-H` <a href="#index-_002dH" class="copiable-anchor">¶</a>  
`--with-filename`  
<span id="index-_002d_002dwith_002dfilename"></span> <span
id="index-with-filename-prefix"></span>

Print the file name for each match. This is the default when there is
more than one file to search.

`-h` <a href="#index-_002dh" class="copiable-anchor">¶</a>  
`--no-filename`  
<span id="index-_002d_002dno_002dfilename"></span> <span
id="index-no-filename-prefix"></span>

Suppress the prefixing of file names on output. This is the default when
there is only one file (or only standard input) to search.

`--label=LABEL` <a href="#index-_002d_002dlabel" class="copiable-anchor">¶</a>  
<span id="index-changing-name-of-standard-input"></span>

Display input actually coming from standard input as input coming from
file `LABEL`. This can be useful for commands that transform a file’s
contents before searching; e.g.:

<div class="example">

``` example
gzip -cd foo.gz | grep --label=foo -H 'some pattern'
```

</div>

`-n` <a href="#index-_002dn" class="copiable-anchor">¶</a>  
`--line-number`  
<span id="index-_002d_002dline_002dnumber"></span> <span
id="index-line-numbering"></span>

Prefix each line of output with the 1-based line number within its input
file. (`-n` is specified by POSIX.)

`-T` <a href="#index-_002dT" class="copiable-anchor">¶</a>  
`--initial-tab`  
<span id="index-_002d_002dinitial_002dtab"></span> <span
id="index-tab_002daligned-content-lines"></span>

Make sure that the first character of actual line content lies on a tab
stop, so that the alignment of tabs looks normal. This is useful with
options that prefix their output to the actual content: `-H`, `-n`, and
`-b`. This may also prepend spaces to output line numbers and byte
offsets so that lines from a single file all start at the same column.

`-Z` <a href="#index-_002dZ" class="copiable-anchor">¶</a>  
`--null`  
<span id="index-_002d_002dnull"></span> <span
id="index-zero_002dterminated-file-names"></span>

Output a zero byte (the ASCII NUL character) instead of the character
that normally follows a file name. For example, ‘`grep -lZ`’ outputs a
zero byte after each file name instead of the usual newline. This option
makes the output unambiguous, even in the presence of file names
containing unusual characters like newlines. This option can be used
with commands like ‘`find -print0`’, ‘`perl -0`’, ‘`sort -z`’, and
‘`xargs -0`’ to process arbitrary file names, even those that contain
newline characters.

------------------------------------------------------------------------

</div>

<div id="Context-Line-Control" class="subsection">

<div class="header">

Next:
<a href="#File-and-Directory-Selection" accesskey="n" rel="next">File
and Directory Selection</a>, Previous:
<a href="#Output-Line-Prefix-Control" accesskey="p" rel="prev">Output
Line Prefix Control</a>, Up:
<a href="#Command_002dline-Options" accesskey="u" rel="up">Command-line
Options</a>   \[<a href="#SEC_Contents" rel="contents"
title="Table of contents">Contents</a>\]\[<a href="#Index" rel="index" title="Index">Index</a>\]

</div>

<span id="Context-Line-Control-1"></span>

#### 2.1.5 Context Line Control

<span id="index-context-lines-1"></span>

*Context lines* are non-matching lines that are near a matching line.
They are output only if one of the following options are used.
Regardless of how these options are set, `grep` never outputs any given
line more than once. If the `-o` (`--only-matching`) option is
specified, these options have no effect and a warning is given upon
their use.

`-A num` <a href="#index-_002dA" class="copiable-anchor">¶</a>  
`--after-context=num`  
<span id="index-_002d_002dafter_002dcontext"></span> <span
id="index-after-context"></span> <span
id="index-context-lines_002c-after-match"></span>

Print `num` lines of trailing context after matching lines.

`-B num` <a href="#index-_002dB" class="copiable-anchor">¶</a>  
`--before-context=num`  
<span id="index-_002d_002dbefore_002dcontext"></span> <span
id="index-before-context"></span> <span
id="index-context-lines_002c-before-match"></span>

Print `num` lines of leading context before matching lines.

`-C num` <a href="#index-_002dC" class="copiable-anchor">¶</a>  
`-num`  
`--context=num`  
<span id="index-_002d_002dcontext"></span> <span
id="index-_002dnum"></span> <span id="index-context-lines-2"></span>

Print `num` lines of leading and trailing output context.

`--group-separator=string` <a href="#index-_002d_002dgroup_002dseparator"
class="copiable-anchor">¶</a>  
<span id="index-group-separator"></span>

When `-A`, `-B` or `-C` are in use, print `string` instead of `--`
between groups of lines.

`--no-group-separator` <a href="#index-_002d_002dgroup_002dseparator-1"
class="copiable-anchor">¶</a>  
<span id="index-group-separator-1"></span>

When `-A`, `-B` or `-C` are in use, do not print a separator between
groups of lines.

Here are some points about how `grep` chooses the separator to print
between prefix fields and line content:

-   Matching lines normally use ‘`:`’ as a separator between prefix
    fields and actual line content.
-   Context (i.e., non-matching) lines use ‘`-`’ instead.
-   When context is not specified, matching lines are simply output one
    right after another.
-   When context is specified, lines that are adjacent in the input form
    a group and are output one right after another, while by default a
    separator appears between non-adjacent groups.
-   The default separator is a ‘`--`’ line; its presence and appearance
    can be changed with the options above.
-   Each group may contain several matching lines when they are close
    enough to each other that two adjacent groups connect and can merge
    into a single contiguous one.

------------------------------------------------------------------------

</div>

<div id="File-and-Directory-Selection" class="subsection">

<div class="header">

Next:
<a href="#Other-Options" accesskey="n" rel="next">Other Options</a>,
Previous:
<a href="#Context-Line-Control" accesskey="p" rel="prev">Context Line
Control</a>, Up:
<a href="#Command_002dline-Options" accesskey="u" rel="up">Command-line
Options</a>   \[<a href="#SEC_Contents" rel="contents"
title="Table of contents">Contents</a>\]\[<a href="#Index" rel="index" title="Index">Index</a>\]

</div>

<span id="File-and-Directory-Selection-1"></span>

#### 2.1.6 File and Directory Selection

`-a` <a href="#index-_002da" class="copiable-anchor">¶</a>  
`--text`  
<span id="index-_002d_002dtext"></span> <span
id="index-suppress-binary-data"></span> <span
id="index-binary-files"></span>

Process a binary file as if it were text; this is equivalent to the
‘`--binary-files=text`’ option.

`--binary-files=type` <a href="#index-_002d_002dbinary_002dfiles"
class="copiable-anchor">¶</a>  
<span id="index-binary-files-1"></span>

If a file’s data or metadata indicate that the file contains binary
data, assume that the file is of type `type`. Non-text bytes indicate
binary data; these are either output bytes that are improperly encoded
for the current locale (see [Environment
Variables](#Environment-Variables)), or null input bytes when the `-z`
(`--null-data`) option is not given (see [Other
Options](#Other-Options)).

By default, `type` is ‘`binary`’, and `grep` suppresses output after
null input binary data is discovered, and suppresses output lines that
contain improperly encoded data. When some output is suppressed, `grep`
follows any output with a one-line message saying that a binary file
matches.

If `type` is ‘`without-match`’, when `grep` discovers null input binary
data it assumes that the rest of the file does not match; this is
equivalent to the `-I` option.

If `type` is ‘`text`’, `grep` processes binary data as if it were text;
this is equivalent to the `-a` option.

When `type` is ‘`binary`’, `grep` may treat non-text bytes as line
terminators even without the `-z` (`--null-data`) option. This means
choosing ‘`binary`’ versus ‘`text`’ can affect whether a pattern matches
a file. For example, when `type` is ‘`binary`’ the pattern ‘`q$`’ might
match ‘`q`’ immediately followed by a null byte, even though this is not
matched when `type` is ‘`text`’. Conversely, when `type` is ‘`binary`’
the pattern ‘`.`’ (period) might not match a null byte.

*Warning:* The `-a` (`--binary-files=text`) option might output binary
garbage, which can have nasty side effects if the output is a terminal
and if the terminal driver interprets some of it as commands. On the
other hand, when reading files whose text encodings are unknown, it can
be helpful to use `-a` or to set ‘`LC_ALL='C'`’ in the environment, in
order to find more matches even if the matches are unsafe for direct
display.

`-D action` <a href="#index-_002dD" class="copiable-anchor">¶</a>  
`--devices=action`  
<span id="index-_002d_002ddevices"></span> <span
id="index-device-search"></span>

If an input file is a device, FIFO, or socket, use `action` to process
it. If `action` is ‘`read`’, all devices are read just as if they were
ordinary files. If `action` is ‘`skip`’, devices, FIFOs, and sockets are
silently skipped. By default, devices are read if they are on the
command line or if the `-R` (`--dereference-recursive`) option is used,
and are skipped if they are encountered recursively and the `-r`
(`--recursive`) option is used. This option has no effect on a file that
is read via standard input.

`-d action` <a href="#index-_002dd" class="copiable-anchor">¶</a>  
`--directories=action`  
<span id="index-_002d_002ddirectories"></span> <span
id="index-directory-search"></span> <span
id="index-symbolic-links"></span>

If an input file is a directory, use `action` to process it. By default,
`action` is ‘`read`’, which means that directories are read just as if
they were ordinary files (some operating systems and file systems
disallow this, and will cause `grep` to print error messages for every
directory or silently skip them). If `action` is ‘`skip`’, directories
are silently skipped. If `action` is ‘`recurse`’, `grep` reads all files
under each directory, recursively, following command-line symbolic links
and skipping other symlinks; this is equivalent to the `-r` option.

`--exclude=glob` <a href="#index-_002d_002dexclude" class="copiable-anchor">¶</a>  
<span id="index-exclude-files"></span> <span
id="index-searching-directory-trees"></span>

Skip any command-line file with a name suffix that matches the pattern
`glob`, using wildcard matching; a name suffix is either the whole name,
or a trailing part that starts with a non-slash character immediately
after a slash (‘`/`’) in the name. When searching recursively, skip any
subfile whose base name matches `glob`; the base name is the part after
the last slash. A pattern can use ‘`*`’, ‘`?`’, and ‘`[`’...‘`]`’ as
wildcards, and `\` to quote a wildcard or backslash character literally.

`--exclude-from=file` <a href="#index-_002d_002dexclude_002dfrom"
class="copiable-anchor">¶</a>  
<span id="index-exclude-files-1"></span> <span
id="index-searching-directory-trees-1"></span>

Skip files whose name matches any of the patterns read from `file`
(using wildcard matching as described under `--exclude`).

`--exclude-dir=glob` <a href="#index-_002d_002dexclude_002ddir" class="copiable-anchor">¶</a>  
<span id="index-exclude-directories"></span>

Skip any command-line directory with a name suffix that matches the
pattern `glob`. When searching recursively, skip any subdirectory whose
base name matches `glob`. Ignore any redundant trailing slashes in
`glob`.

`-I`  
Process a binary file as if it did not contain matching data; this is
equivalent to the ‘`--binary-files=without-match`’ option.

`--include=glob` <a href="#index-_002d_002dinclude" class="copiable-anchor">¶</a>  
<span id="index-include-files"></span> <span
id="index-searching-directory-trees-2"></span>

Search only files whose name matches `glob`, using wildcard matching as
described under `--exclude`. If contradictory `--include` and
`--exclude` options are given, the last matching one wins. If no
`--include` or `--exclude` options match, a file is included unless the
first such option is `--include`.

`-r` <a href="#index-_002dr" class="copiable-anchor">¶</a>  
`--recursive`  
<span id="index-_002d_002drecursive"></span> <span
id="index-recursive-search"></span> <span
id="index-searching-directory-trees-3"></span> <span
id="index-symbolic-links-1"></span>

For each directory operand, read and process all files in that
directory, recursively. Follow symbolic links on the command line, but
skip symlinks that are encountered recursively. Note that if no file
operand is given, grep searches the working directory. This is the same
as the ‘`--directories=recurse`’ option.

`-R` <a href="#index-_002dR" class="copiable-anchor">¶</a>  
`--dereference-recursive`  
<span id="index-_002d_002ddereference_002drecursive"></span> <span
id="index-recursive-search-1"></span> <span
id="index-searching-directory-trees-4"></span> <span
id="index-symbolic-links-2"></span>

For each directory operand, read and process all files in that
directory, recursively, following all symbolic links.

------------------------------------------------------------------------

</div>

<div id="Other-Options" class="subsection">

<div class="header">

Previous:
<a href="#File-and-Directory-Selection" accesskey="p" rel="prev">File
and Directory Selection</a>, Up:
<a href="#Command_002dline-Options" accesskey="u" rel="up">Command-line
Options</a>   \[<a href="#SEC_Contents" rel="contents"
title="Table of contents">Contents</a>\]\[<a href="#Index" rel="index" title="Index">Index</a>\]

</div>

<span id="Other-Options-1"></span>

#### 2.1.7 Other Options

`--` <a href="#index-_002d_002d" class="copiable-anchor">¶</a>  
<span id="index-option-delimiter"></span>

Delimit the option list. Later arguments, if any, are treated as
operands even if they begin with ‘`-`’. For example,
‘`grep PAT -- -file1 file2`’ searches for the pattern PAT in the files
named `-file1` and `file2`.

`--line-buffered` <a href="#index-_002d_002dline_002dbuffered"
class="copiable-anchor">¶</a>  
<span id="index-line-buffering"></span>

Use line buffering for standard output, regardless of output device. By
default, standard output is line buffered for interactive devices, and
is fully buffered otherwise. With full buffering, the output buffer is
flushed when full; with line buffering, the buffer is also flushed after
every output line. The buffer size is system dependent.

`-U` <a href="#index-_002dU" class="copiable-anchor">¶</a>  
`--binary`  
<span id="index-_002d_002dbinary"></span> <span
id="index-MS_002dWindows-binary-I_002fO"></span> <span
id="index-binary-I_002fO"></span>

On platforms that distinguish between text and binary I/O, use the
latter when reading and writing files other than the user’s terminal, so
that all input bytes are read and written as-is. This overrides the
default behavior where `grep` follows the operating system’s advice
whether to use text or binary I/O. On MS-Windows when `grep` uses text
I/O it reads a carriage return–newline pair as a newline and a Control-Z
as end-of-file, and it writes a newline as a carriage return–newline
pair.

When using text I/O `--byte-offset` (`-b`) counts and `--binary-files`
heuristics apply to input data after text-I/O processing. Also, the
`--binary-files` heuristics need not agree with the `--binary` option;
that is, they may treat the data as text even if `--binary` is given, or
vice versa. See [File and Directory
Selection](#File-and-Directory-Selection).

This option has no effect on GNU and other POSIX-compatible platforms,
which do not distinguish text from binary I/O.

`-z` <a href="#index-_002dz" class="copiable-anchor">¶</a>  
`--null-data`  
<span id="index-_002d_002dnull_002ddata"></span> <span
id="index-zero_002dterminated-lines"></span>

Treat input and output data as sequences of lines, each terminated by a
zero byte (the ASCII NUL character) instead of a newline. Like the `-Z`
or `--null` option, this option can be used with commands like
‘`sort -z`’ to process arbitrary file names.

------------------------------------------------------------------------

</div>

</div>

<div id="Environment-Variables" class="section">

<div class="header">

Next: <a href="#Exit-Status" accesskey="n" rel="next">Exit Status</a>,
Previous: <a href="#Command_002dline-Options" accesskey="p"
rel="prev">Command-line Options</a>, Up:
<a href="#Invoking" accesskey="u" rel="up">Invoking
<code>grep</code></a>   \[<a href="#SEC_Contents" rel="contents"
title="Table of contents">Contents</a>\]\[<a href="#Index" rel="index" title="Index">Index</a>\]

</div>

<span id="Environment-Variables-1"></span>

### 2.2 Environment Variables

The behavior of `grep` is affected by the following environment
variables.

<span id="index-LANGUAGE-environment-variable"></span> <span
id="index-LC_005fALL-environment-variable"></span> <span
id="index-LC_005fMESSAGES-environment-variable"></span> <span
id="index-LANG-environment-variable"></span>

The locale for category `LC_foo` is specified by examining the three
environment variables `LC_ALL`, `LC_foo`, and `LANG`, in that order. The
first of these variables that is set specifies the locale. For example,
if `LC_ALL` is not set, but `LC_COLLATE` is set to ‘`pt_BR`’, then the
Brazilian Portuguese locale is used for the `LC_COLLATE` category. As a
special case for `LC_MESSAGES` only, the environment variable `LANGUAGE`
can contain a colon-separated list of languages that overrides the three
environment variables that ordinarily specify the `LC_MESSAGES`
category. The ‘`C`’ locale is used if none of these environment
variables are set, if the locale catalog is not installed, or if `grep`
was not compiled with national language support (NLS). The shell command
`locale -a` lists locales that are currently available.

Many of the environment variables in the following list let you control
highlighting using Select Graphic Rendition (SGR) commands interpreted
by the terminal or terminal emulator. (See the section in the
documentation of your text terminal for permitted values and their
meanings as character attributes.) These substring values are integers
in decimal representation and can be concatenated with semicolons.
`grep` takes care of assembling the result into a complete SGR sequence
(‘`\33[`’...‘`m`’). Common values to concatenate include ‘`1`’ for bold,
‘`4`’ for underline, ‘`5`’ for blink, ‘`7`’ for inverse, ‘`39`’ for
default foreground color, ‘`30`’ to ‘`37`’ for foreground colors, ‘`90`’
to ‘`97`’ for 16-color mode foreground colors, ‘`38;5;0`’ to
‘`38;5;255`’ for 88-color and 256-color modes foreground colors, ‘`49`’
for default background color, ‘`40`’ to ‘`47`’ for background colors,
‘`100`’ to ‘`107`’ for 16-color mode background colors, and ‘`48;5;0`’
to ‘`48;5;255`’ for 88-color and 256-color modes background colors.

The two-letter names used in the `GREP_COLORS` environment variable (and
some of the others) refer to terminal “capabilities,” the ability of a
terminal to highlight text, or change its color, and so on. These
capabilities are stored in an online database and accessed by the
`terminfo` library.

<span id="index-environment-variables"></span>

`GREP_COLOR` <a href="#index-GREP_005fCOLOR-environment-variable"
class="copiable-anchor">¶</a>  
<span id="index-highlight-markers"></span>

This variable specifies the color used to highlight matched (non-empty)
text. It is deprecated in favor of `GREP_COLORS`, but still supported.
The ‘`mt`’, ‘`ms`’, and ‘`mc`’ capabilities of `GREP_COLORS` have
priority over it. It can only specify the color used to highlight the
matching non-empty text in any matching line (a selected line when the
`-v` command-line option is omitted, or a context line when `-v` is
specified). The default is ‘`01;31`’, which means a bold red foreground
text on the terminal’s default background.

`GREP_COLORS` <a href="#index-GREP_005fCOLORS-environment-variable"
class="copiable-anchor">¶</a>  
<span id="index-highlight-markers-1"></span>

This variable specifies the colors and other attributes used to
highlight various parts of the output. Its value is a colon-separated
list of `terminfo` capabilities that defaults to
‘`ms=01;31:mc=01;31:sl=:cx=:fn=35:ln=32:bn=32:se=36`’ with the ‘`rv`’
and ‘`ne`’ boolean capabilities omitted (i.e., false). Supported
capabilities are as follows.

`sl=` <a href="#index-sl-GREP_005fCOLORS-capability"
class="copiable-anchor">¶</a>  
SGR substring for whole selected lines (i.e., matching lines when the
`-v` command-line option is omitted, or non-matching lines when `-v` is
specified). If however the boolean ‘`rv`’ capability and the `-v`
command-line option are both specified, it applies to context matching
lines instead. The default is empty (i.e., the terminal’s default color
pair).

`cx=` <a href="#index-cx-GREP_005fCOLORS-capability"
class="copiable-anchor">¶</a>  
SGR substring for whole context lines (i.e., non-matching lines when the
`-v` command-line option is omitted, or matching lines when `-v` is
specified). If however the boolean ‘`rv`’ capability and the `-v`
command-line option are both specified, it applies to selected
non-matching lines instead. The default is empty (i.e., the terminal’s
default color pair).

`rv` <a href="#index-rv-GREP_005fCOLORS-capability"
class="copiable-anchor">¶</a>  
Boolean value that reverses (swaps) the meanings of the ‘`sl=`’ and
‘`cx=`’ capabilities when the `-v` command-line option is specified. The
default is false (i.e., the capability is omitted).

`mt=01;31` <a href="#index-mt-GREP_005fCOLORS-capability"
class="copiable-anchor">¶</a>  
SGR substring for matching non-empty text in any matching line (i.e., a
selected line when the `-v` command-line option is omitted, or a context
line when `-v` is specified). Setting this is equivalent to setting both
‘`ms=`’ and ‘`mc=`’ at once to the same value. The default is a bold red
text foreground over the current line background.

`ms=01;31` <a href="#index-ms-GREP_005fCOLORS-capability"
class="copiable-anchor">¶</a>  
SGR substring for matching non-empty text in a selected line. (This is
used only when the `-v` command-line option is omitted.) The effect of
the ‘`sl=`’ (or ‘`cx=`’ if ‘`rv`’) capability remains active when this
takes effect. The default is a bold red text foreground over the current
line background.

`mc=01;31` <a href="#index-mc-GREP_005fCOLORS-capability"
class="copiable-anchor">¶</a>  
SGR substring for matching non-empty text in a context line. (This is
used only when the `-v` command-line option is specified.) The effect of
the ‘`cx=`’ (or ‘`sl=`’ if ‘`rv`’) capability remains active when this
takes effect. The default is a bold red text foreground over the current
line background.

`fn=35` <a href="#index-fn-GREP_005fCOLORS-capability"
class="copiable-anchor">¶</a>  
SGR substring for file names prefixing any content line. The default is
a magenta text foreground over the terminal’s default background.

`ln=32` <a href="#index-ln-GREP_005fCOLORS-capability"
class="copiable-anchor">¶</a>  
SGR substring for line numbers prefixing any content line. The default
is a green text foreground over the terminal’s default background.

`bn=32` <a href="#index-bn-GREP_005fCOLORS-capability"
class="copiable-anchor">¶</a>  
SGR substring for byte offsets prefixing any content line. The default
is a green text foreground over the terminal’s default background.

`se=36` <a href="#index-fn-GREP_005fCOLORS-capability-1"
class="copiable-anchor">¶</a>  
SGR substring for separators that are inserted between selected line
fields (‘`:`’), between context line fields (‘`-`’), and between groups
of adjacent lines when nonzero context is specified (‘`--`’). The
default is a cyan text foreground over the terminal’s default
background.

`ne` <a href="#index-ne-GREP_005fCOLORS-capability"
class="copiable-anchor">¶</a>  
Boolean value that prevents clearing to the end of line using Erase in
Line (EL) to Right (‘`\33[K`’) each time a colorized item ends. This is
needed on terminals on which EL is not supported. It is otherwise useful
on terminals for which the `back_color_erase` (`bce`) boolean `terminfo`
capability does not apply, when the chosen highlight colors do not
affect the background, or when EL is too slow or causes too much
flicker. The default is false (i.e., the capability is omitted).

Note that boolean capabilities have no ‘`=`’... part. They are omitted
(i.e., false) by default and become true when specified.

`LC_ALL` <a href="#index-LC_005fALL-environment-variable-1"
class="copiable-anchor">¶</a>  
`LC_COLLATE`  
`LANG`  
<span id="index-LC_005fCOLLATE-environment-variable"></span> <span
id="index-LANG-environment-variable-1"></span> <span
id="index-character-type"></span> <span
id="index-national-language-support"></span> <span
id="index-NLS"></span>

These variables specify the locale for the `LC_COLLATE` category, which
might affect how range expressions like ‘`[a-z]`’ are interpreted.

`LC_ALL` <a href="#index-LC_005fALL-environment-variable-2"
class="copiable-anchor">¶</a>  
`LC_CTYPE`  
`LANG`  
<span id="index-LC_005fCTYPE-environment-variable"></span> <span
id="index-LANG-environment-variable-2"></span> <span
id="index-encoding-error"></span> <span
id="index-null-character"></span>

These variables specify the locale for the `LC_CTYPE` category, which
determines the type of characters, e.g., which characters are
whitespace. This category also determines the character encoding. See
[Character Encoding](#Character-Encoding).

`LANGUAGE` <a href="#index-LANGUAGE-environment-variable-1"
class="copiable-anchor">¶</a>  
`LC_ALL`  
`LC_MESSAGES`  
`LANG`  
<span id="index-LC_005fALL-environment-variable-3"></span> <span
id="index-LC_005fMESSAGES-environment-variable-1"></span> <span
id="index-LANG-environment-variable-3"></span> <span
id="index-language-of-messages"></span> <span
id="index-message-language"></span> <span
id="index-national-language-support-1"></span> <span
id="index-translation-of-message-language"></span>

These variables specify the locale for the `LC_MESSAGES` category, which
determines the language that `grep` uses for messages. The default ‘`C`’
locale uses American English messages.

`POSIXLY_CORRECT` <a href="#index-POSIXLY_005fCORRECT-environment-variable"
class="copiable-anchor">¶</a>  
If set, `grep` behaves as POSIX requires; otherwise, `grep` behaves more
like other GNU programs. POSIX requires that options that follow file
names must be treated as file names; by default, such options are
permuted to the front of the operand list and are treated as options.
Also, `POSIXLY_CORRECT` disables special handling of an invalid bracket
expression. See [invalid-bracket-expr](#invalid_002dbracket_002dexpr).

`_N_GNU_nonoption_argv_flags_` <a
href="#index-_005fN_005fGNU_005fnonoption_005fargv_005fflags_005f-environment-variable"
class="copiable-anchor">¶</a>  
(Here `N` is `grep`’s numeric process ID.) If the `i`th character of
this environment variable’s value is ‘`1`’, do not consider the `i`th
operand of `grep` to be an option, even if it appears to be one. A shell
can put this variable in the environment for each command it runs,
specifying which operands are the results of file name wildcard
expansion and therefore should not be treated as options. This behavior
is available only with the GNU C library, and only when
`POSIXLY_CORRECT` is not set.

The `GREP_OPTIONS` environment variable of `grep` 2.20 and earlier is no
longer supported, as it caused problems when writing portable scripts.
To make arbitrary changes to how `grep` works, you can use an alias or
script instead. For example, if `grep` is in the directory ‘`/usr/bin`’
you can prepend `$HOME/bin` to your `PATH` and create an executable
script `$HOME/bin/grep` containing the following:

<div class="example">

``` example
#! /bin/sh
export PATH=/usr/bin
exec grep --color=auto --devices=skip "$@"
```

</div>

------------------------------------------------------------------------

</div>

<div id="Exit-Status" class="section">

<div class="header">

Next:
<a href="#grep-Programs" accesskey="n" rel="next"><code>grep</code>
Programs</a>, Previous:
<a href="#Environment-Variables" accesskey="p" rel="prev">Environment
Variables</a>, Up: <a href="#Invoking" accesskey="u" rel="up">Invoking
<code>grep</code></a>   \[<a href="#SEC_Contents" rel="contents"
title="Table of contents">Contents</a>\]\[<a href="#Index" rel="index" title="Index">Index</a>\]

</div>

<span id="Exit-Status-1"></span>

### 2.3 Exit Status

<span id="index-exit-status"></span> <span
id="index-return-status"></span>

Normally the exit status is 0 if a line is selected, 1 if no lines were
selected, and 2 if an error occurred. However, if the `-q` or `--quiet`
or `--silent` option is used and a line is selected, the exit status is
0 even if an error occurred. Other `grep` implementations may exit with
status greater than 2 on error.

------------------------------------------------------------------------

</div>

<div id="grep-Programs" class="section">

<div class="header">

Previous:
<a href="#Exit-Status" accesskey="p" rel="prev">Exit Status</a>, Up:
<a href="#Invoking" accesskey="u" rel="up">Invoking
<code>grep</code></a>   \[<a href="#SEC_Contents" rel="contents"
title="Table of contents">Contents</a>\]\[<a href="#Index" rel="index" title="Index">Index</a>\]

</div>

<span id="grep-Programs-1"></span>

### 2.4 `grep` Programs

<span id="index-grep-programs"></span> <span
id="index-variants-of-grep"></span>

`grep` searches the named input files for lines containing a match to
the given patterns. By default, `grep` prints the matching lines. A file
named `-` stands for standard input. If no input is specified, `grep`
searches the working directory `.` if given a command-line option
specifying recursion; otherwise, `grep` searches standard input. There
are four major variants of `grep`, controlled by the following options.

`-G` <a href="#index-_002dG" class="copiable-anchor">¶</a>  
`--basic-regexp`  
<span id="index-_002d_002dbasic_002dregexp"></span> <span
id="index-matching-basic-regular-expressions"></span>

Interpret patterns as basic regular expressions (BREs). This is the
default.

`-E` <a href="#index-_002dE" class="copiable-anchor">¶</a>  
`--extended-regexp`  
<span id="index-_002d_002dextended_002dregexp"></span> <span
id="index-matching-extended-regular-expressions"></span>

Interpret patterns as extended regular expressions (EREs). (`-E` is
specified by POSIX.)

`-F` <a href="#index-_002dF" class="copiable-anchor">¶</a>  
`--fixed-strings`  
<span id="index-_002d_002dfixed_002dstrings"></span> <span
id="index-matching-fixed-strings"></span>

Interpret patterns as fixed strings, not regular expressions. (`-F` is
specified by POSIX.)

`-P` <a href="#index-_002dP" class="copiable-anchor">¶</a>  
`--perl-regexp`  
<span id="index-_002d_002dperl_002dregexp"></span> <span
id="index-matching-Perl_002dcompatible-regular-expressions"></span>

Interpret patterns as Perl-compatible regular expressions (PCREs). PCRE
support is here to stay, but consider this option experimental when
combined with the `-z` (`--null-data`) option, and note that ‘`grep -P`’
may warn of unimplemented features. See [Other Options](#Other-Options).

In addition, two variant programs `egrep` and `fgrep` are available.
`egrep` is the same as ‘`grep -E`’. `fgrep` is the same as ‘`grep -F`’.
Direct invocation as either `egrep` or `fgrep` is deprecated, but is
provided to allow historical applications that rely on them to run
unmodified.

------------------------------------------------------------------------

</div>

</div>

<div id="Regular-Expressions" class="chapter">

<div class="header">

Next: <a href="#Usage" accesskey="n" rel="next">Usage</a>, Previous:
<a href="#Invoking" accesskey="p" rel="prev">Invoking
<code>grep</code></a>, Up:
<a href="#Top" accesskey="u" rel="up">grep</a>  
\[<a href="#SEC_Contents" rel="contents"
title="Table of contents">Contents</a>\]\[<a href="#Index" rel="index" title="Index">Index</a>\]

</div>

<span id="Regular-Expressions-1"></span>

## 3 Regular Expressions

<span id="index-regular-expressions"></span>

A *regular expression* is a pattern that describes a set of strings.
Regular expressions are constructed analogously to arithmetic
expressions, by using various operators to combine smaller expressions.
`grep` understands three different versions of regular expression
syntax: basic (BRE), extended (ERE), and Perl-compatible (PCRE). In GNU
`grep`, there is no difference in available functionality between the
basic and extended syntaxes. In other implementations, basic regular
expressions are less powerful. The following description applies to
extended regular expressions; differences for basic regular expressions
are summarized afterwards. Perl-compatible regular expressions give
additional functionality, and are documented in the *pcresyntax*(3) and
*pcrepattern*(3) manual pages, but work only if PCRE is available in the
system.

-   <a href="#Fundamental-Structure" accesskey="1">Fundamental Structure</a>
-   <a href="#Character-Classes-and-Bracket-Expressions"
    accesskey="2">Character Classes and Bracket Expressions</a>
-   <a href="#The-Backslash-Character-and-Special-Expressions"
    accesskey="3">The Backslash Character and Special Expressions</a>
-   <a href="#Anchoring" accesskey="4">Anchoring</a>
-   <a href="#Back_002dreferences-and-Subexpressions"
    accesskey="5">Back-references and Subexpressions</a>
-   <a href="#Basic-vs-Extended" accesskey="6">Basic vs Extended Regular
    Expressions</a>
-   <a href="#Character-Encoding" accesskey="7">Character Encoding</a>
-   <a href="#Matching-Non_002dASCII" accesskey="8">Matching Non-ASCII and
    Non-printable Characters</a>

------------------------------------------------------------------------

<div id="Fundamental-Structure" class="section">

<div class="header">

Next: <a href="#Character-Classes-and-Bracket-Expressions" accesskey="n"
rel="next">Character Classes and Bracket Expressions</a>, Up:
<a href="#Regular-Expressions" accesskey="u" rel="up">Regular
Expressions</a>   \[<a href="#SEC_Contents" rel="contents"
title="Table of contents">Contents</a>\]\[<a href="#Index" rel="index" title="Index">Index</a>\]

</div>

<span id="Fundamental-Structure-1"></span>

### 3.1 Fundamental Structure

<span id="index-ordinary-characters"></span> <span
id="index-special-characters"></span>

In regular expressions, the characters ‘`.?*+{|()[\^$`’ are *special
characters* and have uses described below. All other characters are
*ordinary characters*, and each ordinary character is a regular
expression that matches itself.

<span id="index-_002e"></span> <span id="index-dot"></span> <span
id="index-period"></span>

The period ‘`.`’ matches any single character. It is unspecified whether
‘`.`’ matches an encoding error.

<span id="index-interval-expressions"></span>

A regular expression may be followed by one of several repetition
operators; the operators beginning with ‘`{`’ are called *interval
expressions*.

‘`?`’ <a href="#index-_003f" class="copiable-anchor">¶</a>  
<span id="index-question-mark"></span> <span
id="index-match-expression-at-most-once"></span>

The preceding item is optional and is matched at most once.

‘`*`’ <a href="#index-_002a" class="copiable-anchor">¶</a>  
<span id="index-asterisk"></span> <span
id="index-match-expression-zero-or-more-times"></span>

The preceding item is matched zero or more times.

‘`+`’ <a href="#index-_002b" class="copiable-anchor">¶</a>  
<span id="index-plus-sign"></span> <span
id="index-match-expression-one-or-more-times"></span>

The preceding item is matched one or more times.

‘`{n}`’ <a href="#index-_007bn_007d" class="copiable-anchor">¶</a>  
<span id="index-braces_002c-one-argument"></span> <span
id="index-match-expression-n-times"></span>

The preceding item is matched exactly `n` times.

‘`{n,}`’ <a href="#index-_007bn_002c_007d" class="copiable-anchor">¶</a>  
<span id="index-braces_002c-second-argument-omitted"></span> <span
id="index-match-expression-n-or-more-times"></span>

The preceding item is matched `n` or more times.

‘`{,m}`’ <a href="#index-_007b_002cm_007d" class="copiable-anchor">¶</a>  
<span id="index-braces_002c-first-argument-omitted"></span> <span
id="index-match-expression-at-most-m-times"></span>

The preceding item is matched at most `m` times. This is a GNU
extension.

‘`{n,m}`’ <a href="#index-_007bn_002cm_007d" class="copiable-anchor">¶</a>  
<span id="index-braces_002c-two-arguments"></span> <span
id="index-match-expression-from-n-to-m-times"></span>

The preceding item is matched at least `n` times, but not more than `m`
times.

The empty regular expression matches the empty string. Two regular
expressions may be concatenated; the resulting regular expression
matches any string formed by concatenating two substrings that
respectively match the concatenated expressions.

Two regular expressions may be joined by the infix operator ‘`|`’; the
resulting regular expression matches any string matching either
alternate expression.

Repetition takes precedence over concatenation, which in turn takes
precedence over alternation. A whole expression may be enclosed in
parentheses to override these precedence rules and form a subexpression.
An unmatched ‘`)`’ matches just itself.

------------------------------------------------------------------------

</div>

<div id="Character-Classes-and-Bracket-Expressions" class="section">

<div class="header">

Next:
<a href="#The-Backslash-Character-and-Special-Expressions" accesskey="n"
rel="next">The Backslash Character and Special Expressions</a>,
Previous:
<a href="#Fundamental-Structure" accesskey="p" rel="prev">Fundamental
Structure</a>, Up:
<a href="#Regular-Expressions" accesskey="u" rel="up">Regular
Expressions</a>   \[<a href="#SEC_Contents" rel="contents"
title="Table of contents">Contents</a>\]\[<a href="#Index" rel="index" title="Index">Index</a>\]

</div>

<span id="Character-Classes-and-Bracket-Expressions-1"></span>

### 3.2 Character Classes and Bracket Expressions

<span id="index-bracket-expression"></span> <span
id="index-character-class"></span>

A *bracket expression* is a list of characters enclosed by ‘`[`’ and
‘`]`’. It matches any single character in that list. If the first
character of the list is the caret ‘`^`’, then it matches any character
**not** in the list, and it is unspecified whether it matches an
encoding error. For example, the regular expression ‘`[0123456789]`’
matches any single digit, whereas ‘`[^()]`’ matches any single character
that is not an opening or closing parenthesis, and might or might not
match an encoding error.

<span id="index-range-expression"></span>

Within a bracket expression, a *range expression* consists of two
characters separated by a hyphen. It matches any single character that
sorts between the two characters, inclusive. In the default C locale,
the sorting sequence is the native character order; for example,
‘`[a-d]`’ is equivalent to ‘`[abcd]`’. In other locales, the sorting
sequence is not specified, and ‘`[a-d]`’ might be equivalent to
‘`[abcd]`’ or to ‘`[aBbCcDd]`’, or it might fail to match any character,
or the set of characters that it matches might even be erratic. To
obtain the traditional interpretation of bracket expressions, you can
use the ‘`C`’ locale by setting the `LC_ALL` environment variable to the
value ‘`C`’.

Finally, certain named classes of characters are predefined within
bracket expressions, as follows. Their interpretation depends on the
`LC_CTYPE` locale; for example, ‘`[[:alnum:]]`’ means the character
class of numbers and letters in the current locale.

<span id="index-classes-of-characters"></span> <span
id="index-character-classes"></span>

‘`[:alnum:]`’ <a href="#index-alnum-character-class" class="copiable-anchor">¶</a>  
<span id="index-alphanumeric-characters"></span>

Alphanumeric characters: ‘`[:alpha:]`’ and ‘`[:digit:]`’; in the ‘`C`’
locale and ASCII character encoding, this is the same as
‘`[0-9A-Za-z]`’.

‘`[:alpha:]`’ <a href="#index-alpha-character-class" class="copiable-anchor">¶</a>  
<span id="index-alphabetic-characters"></span>

Alphabetic characters: ‘`[:lower:]`’ and ‘`[:upper:]`’; in the ‘`C`’
locale and ASCII character encoding, this is the same as ‘`[A-Za-z]`’.

‘`[:blank:]`’ <a href="#index-blank-character-class" class="copiable-anchor">¶</a>  
<span id="index-blank-characters"></span>

Blank characters: space and tab.

‘`[:cntrl:]`’ <a href="#index-cntrl-character-class" class="copiable-anchor">¶</a>  
<span id="index-control-characters"></span>

Control characters. In ASCII, these characters have octal codes 000
through 037, and 177 (DEL). In other character sets, these are the
equivalent characters, if any.

‘`[:digit:]`’ <a href="#index-digit-character-class" class="copiable-anchor">¶</a>  
<span id="index-digit-characters"></span> <span
id="index-numeric-characters"></span>

Digits: `0 1 2 3 4 5 6 7 8 9`.

‘`[:graph:]`’ <a href="#index-graph-character-class" class="copiable-anchor">¶</a>  
<span id="index-graphic-characters"></span>

Graphical characters: ‘`[:alnum:]`’ and ‘`[:punct:]`’.

‘`[:lower:]`’ <a href="#index-lower-character-class" class="copiable-anchor">¶</a>  
<span id="index-lower_002dcase-letters"></span>

Lower-case letters; in the ‘`C`’ locale and ASCII character encoding,
this is `a b c d e f g h i j k l m n o p q r s t u v w x y z`.

‘`[:print:]`’ <a href="#index-print-character-class" class="copiable-anchor">¶</a>  
<span id="index-printable-characters"></span>

Printable characters: ‘`[:alnum:]`’, ‘`[:punct:]`’, and space.

‘`[:punct:]`’ <a href="#index-punct-character-class" class="copiable-anchor">¶</a>  
<span id="index-punctuation-characters"></span>

Punctuation characters; in the ‘`C`’ locale and ASCII character
encoding, this is
`` ! " # $ % & ' ( ) * + , - . / : ; < = > ? @ [ \ ] ^ _ ` { | } ~ ``.

‘`[:space:]`’ <a href="#index-space-character-class" class="copiable-anchor">¶</a>  
<span id="index-space-characters"></span> <span
id="index-whitespace-characters"></span>

Space characters: in the ‘`C`’ locale, this is tab, newline, vertical
tab, form feed, carriage return, and space. See [Usage](#Usage), for
more discussion of matching newlines.

‘`[:upper:]`’ <a href="#index-upper-character-class" class="copiable-anchor">¶</a>  
<span id="index-upper_002dcase-letters"></span>

Upper-case letters: in the ‘`C`’ locale and ASCII character encoding,
this is `A B C D E F G H I J K L M N O P Q R S T U V W X Y Z`.

‘`[:xdigit:]`’ <a href="#index-xdigit-character-class" class="copiable-anchor">¶</a>  
<span id="index-xdigit-class"></span> <span
id="index-hexadecimal-digits"></span>

Hexadecimal digits: `0 1 2 3 4 5 6 7 8 9 A B C D E F a b c d e f`.

Note that the brackets in these class names are part of the symbolic
names, and must be included in addition to the brackets delimiting the
bracket expression.

<span id="invalid_002dbracket_002dexpr"></span>

If you mistakenly omit the outer brackets, and search for say,
‘`[:upper:]`’, GNU `grep` prints a diagnostic and exits with status 2,
on the assumption that you did not intend to search for the nominally
equivalent regular expression: ‘`[:epru]`’. Set the `POSIXLY_CORRECT`
environment variable to disable this feature.

Special characters lose their special meaning inside bracket
expressions.

‘`]`’  
ends the bracket expression if it’s not the first list item. So, if you
want to make the ‘`]`’ character a list item, you must put it first.

‘`[.`’  
represents the open collating symbol.

‘`.]`’  
represents the close collating symbol.

‘`[=`’  
represents the open equivalence class.

‘`=]`’  
represents the close equivalence class.

‘`[:`’  
represents the open character class symbol, and should be followed by a
valid character class name.

‘`:]`’  
represents the close character class symbol.

‘`-`’  
represents the range if it’s not first or last in a list or the ending
point of a range.

‘`^`’  
represents the characters not in the list. If you want to make the ‘`^`’
character a list item, place it anywhere but first.

------------------------------------------------------------------------

</div>

<div id="The-Backslash-Character-and-Special-Expressions"
class="section">

<div class="header">

Next: <a href="#Anchoring" accesskey="n" rel="next">Anchoring</a>,
Previous:
<a href="#Character-Classes-and-Bracket-Expressions" accesskey="p"
rel="prev">Character Classes and Bracket Expressions</a>, Up:
<a href="#Regular-Expressions" accesskey="u" rel="up">Regular
Expressions</a>   \[<a href="#SEC_Contents" rel="contents"
title="Table of contents">Contents</a>\]\[<a href="#Index" rel="index" title="Index">Index</a>\]

</div>

<span id="The-Backslash-Character-and-Special-Expressions-1"></span>

### 3.3 The Backslash Character and Special Expressions

<span id="index-backslash"></span>

The ‘`\`’ character followed by a special character is a regular
expression that matches the special character. The ‘`\`’ character, when
followed by certain ordinary characters, takes a special meaning:

‘`\b`’  
Match the empty string at the edge of a word.

‘`\B`’  
Match the empty string provided it’s not at the edge of a word.

‘`\<`’  
Match the empty string at the beginning of a word.

‘`\>`’  
Match the empty string at the end of a word.

‘`\w`’  
Match word constituent, it is a synonym for ‘`[_[:alnum:]]`’.

‘`\W`’  
Match non-word constituent, it is a synonym for ‘`[^_[:alnum:]]`’.

‘`\s`’  
Match whitespace, it is a synonym for ‘`[[:space:]]`’.

‘`\S`’  
Match non-whitespace, it is a synonym for ‘`[^[:space:]]`’.

For example, ‘`\brat\b`’ matches the separate word ‘`rat`’, ‘`\Brat\B`’
matches ‘`crate`’ but not ‘`furry rat`’.

------------------------------------------------------------------------

</div>

<div id="Anchoring" class="section">

<div class="header">

Next: <a href="#Back_002dreferences-and-Subexpressions" accesskey="n"
rel="next">Back-references and Subexpressions</a>, Previous:
<a href="#The-Backslash-Character-and-Special-Expressions" accesskey="p"
rel="prev">The Backslash Character and Special Expressions</a>, Up:
<a href="#Regular-Expressions" accesskey="u" rel="up">Regular
Expressions</a>   \[<a href="#SEC_Contents" rel="contents"
title="Table of contents">Contents</a>\]\[<a href="#Index" rel="index" title="Index">Index</a>\]

</div>

<span id="Anchoring-1"></span>

### 3.4 Anchoring

<span id="index-anchoring"></span>

The caret ‘`^`’ and the dollar sign ‘`$`’ are special characters that
respectively match the empty string at the beginning and end of a line.
They are termed *anchors*, since they force the match to be “anchored”
to beginning or end of a line, respectively.

------------------------------------------------------------------------

</div>

<div id="Back_002dreferences-and-Subexpressions" class="section">

<div class="header">

Next:
<a href="#Basic-vs-Extended" accesskey="n" rel="next">Basic vs Extended
Regular Expressions</a>, Previous:
<a href="#Anchoring" accesskey="p" rel="prev">Anchoring</a>, Up:
<a href="#Regular-Expressions" accesskey="u" rel="up">Regular
Expressions</a>   \[<a href="#SEC_Contents" rel="contents"
title="Table of contents">Contents</a>\]\[<a href="#Index" rel="index" title="Index">Index</a>\]

</div>

<span id="Back_002dreferences-and-Subexpressions-1"></span>

### 3.5 Back-references and Subexpressions

<span id="index-subexpression"></span> <span
id="index-back_002dreference"></span>

The back-reference ‘`\n`’, where `n` is a single nonzero digit, matches
the substring previously matched by the `n`th parenthesized
subexpression of the regular expression. For example, ‘`(a)\1`’ matches
‘`aa`’. If the parenthesized subexpression does not participate in the
match, the back-reference makes the whole match fail; for example,
‘`(a)*\1`’ fails to match ‘`a`’. If the parenthesized subexpression
matches more than one substring, the back-reference refers to the last
matched substring; for example, ‘`^(ab*)*\1$`’ matches ‘`ababbabb`’ but
not ‘`ababbab`’. When multiple regular expressions are given with `-e`
or from a file (‘`-f file`’), back-references are local to each
expression.

See [Known Bugs](#Known-Bugs), for some known problems with
back-references.

------------------------------------------------------------------------

</div>

<div id="Basic-vs-Extended" class="section">

<div class="header">

Next: <a href="#Character-Encoding" accesskey="n" rel="next">Character
Encoding</a>, Previous:
<a href="#Back_002dreferences-and-Subexpressions" accesskey="p"
rel="prev">Back-references and Subexpressions</a>, Up:
<a href="#Regular-Expressions" accesskey="u" rel="up">Regular
Expressions</a>   \[<a href="#SEC_Contents" rel="contents"
title="Table of contents">Contents</a>\]\[<a href="#Index" rel="index" title="Index">Index</a>\]

</div>

<span id="Basic-vs-Extended-Regular-Expressions"></span>

### 3.6 Basic vs Extended Regular Expressions

<span id="index-basic-regular-expressions"></span>

In basic regular expressions the characters ‘`?`’, ‘`+`’, ‘`{`’, ‘`|`’,
‘`(`’, and ‘`)`’ lose their special meaning; instead use the backslashed
versions ‘`\?`’, ‘`\+`’, ‘`\{`’, ‘`\|`’, ‘`\(`’, and ‘`\)`’. Also, a
backslash is needed before an interval expression’s closing ‘`}`’, and
an unmatched `\)` is invalid.

Portable scripts should avoid the following constructs, as POSIX says
they produce undefined results:

-   Extended regular expressions that use back-references.
-   Basic regular expressions that use ‘`\?`’, ‘`\+`’, or ‘`\|`’.
-   Empty parenthesized regular expressions like ‘`()`’.
-   Empty alternatives (as in, e.g, ‘`a|`’).
-   Repetition operators that immediately follow empty expressions,
    unescaped ‘`$`’, or other repetition operators.
-   A backslash escaping an ordinary character (e.g., ‘`\S`’), unless it
    is a back-reference.
-   An unescaped ‘`[`’ that is not part of a bracket expression.
-   In extended regular expressions, an unescaped ‘`{`’ that is not part
    of an interval expression.

<span id="index-interval-expressions-1"></span>

Traditional `egrep` did not support interval expressions and some
`egrep` implementations use ‘`\{`’ and ‘`\}`’ instead, so portable
scripts should avoid interval expressions in ‘`grep -E`’ patterns and
should use ‘`[{]`’ to match a literal ‘`{`’.

GNU `grep -E` attempts to support traditional usage by assuming that
‘`{`’ is not special if it would be the start of an invalid interval
expression. For example, the command ‘`grep -E '{1'`’ searches for the
two-character string ‘`{1`’ instead of reporting a syntax error in the
regular expression. POSIX allows this behavior as an extension, but
portable scripts should avoid it.

------------------------------------------------------------------------

</div>

<div id="Character-Encoding" class="section">

<div class="header">

Next:
<a href="#Matching-Non_002dASCII" accesskey="n" rel="next">Matching
Non-ASCII and Non-printable Characters</a>, Previous:
<a href="#Basic-vs-Extended" accesskey="p" rel="prev">Basic vs Extended
Regular Expressions</a>, Up:
<a href="#Regular-Expressions" accesskey="u" rel="up">Regular
Expressions</a>   \[<a href="#SEC_Contents" rel="contents"
title="Table of contents">Contents</a>\]\[<a href="#Index" rel="index" title="Index">Index</a>\]

</div>

<span id="Character-Encoding-1"></span>

### 3.7 Character Encoding

<span id="index-character-encoding"></span>

The `LC_CTYPE` locale specifies the encoding of characters in patterns
and data, that is, whether text is encoded in UTF-8, ASCII, or some
other encoding. See [Environment Variables](#Environment-Variables).

In the ‘`C`’ or ‘`POSIX`’ locale, every character is encoded as a single
byte and every byte is a valid character. In more-complex encodings such
as UTF-8, a sequence of multiple bytes may be needed to represent a
character, and some bytes may be encoding errors that do not contribute
to the representation of any character. POSIX does not specify the
behavior of `grep` when patterns or input data contain encoding errors
or null characters, so portable scripts should avoid such usage. As an
extension to POSIX, GNU `grep` treats null characters like any other
character. However, unless the `-a` (`--binary-files=text`) option is
used, the presence of null characters in input or of encoding errors in
output causes GNU `grep` to treat the file as binary and suppress
details about matches. See [File and Directory
Selection](#File-and-Directory-Selection).

Regardless of locale, the 103 characters in the POSIX Portable Character
Set (a subset of ASCII) are always encoded as a single byte, and the 128
ASCII characters have their usual single-byte encodings on all but
oddball platforms.

------------------------------------------------------------------------

</div>

<div id="Matching-Non_002dASCII" class="section">

<div class="header">

Previous:
<a href="#Character-Encoding" accesskey="p" rel="prev">Character
Encoding</a>, Up:
<a href="#Regular-Expressions" accesskey="u" rel="up">Regular
Expressions</a>   \[<a href="#SEC_Contents" rel="contents"
title="Table of contents">Contents</a>\]\[<a href="#Index" rel="index" title="Index">Index</a>\]

</div>

<span
id="Matching-Non_002dASCII-and-Non_002dprintable-Characters"></span>

### 3.8 Matching Non-ASCII and Non-printable Characters

<span id="index-non_002dASCII-matching"></span> <span
id="index-non_002dprintable-matching"></span>

In a regular expression, non-ASCII and non-printable characters other
than newline are not special, and represent themselves. For example, in
a locale using UTF-8 the command ‘`grep 'Λ ω'`’ (where the white space
between ‘`Λ`’ and the ‘`ω`’ is a tab character) searches for ‘`Λ`’
(Unicode character U+039B GREEK CAPITAL LETTER LAMBDA), followed by a
tab (U+0009 TAB), followed by ‘`ω`’ (U+03C9 GREEK SMALL LETTER OMEGA).

Suppose you want to limit your pattern to only printable characters (or
even only printable ASCII characters) to keep your script readable or
portable, but you also want to match specific non-ASCII or non-null
non-printable characters. If you are using the `-P` (`--perl-regexp`)
option, PCREs give you several ways to do this. Otherwise, if you are
using Bash, the GNU project’s shell, you can represent these characters
via ANSI-C quoting. For example, the Bash commands ‘`grep $'Λ\tω'`’ and
‘`grep $'\u039B\t\u03C9'`’ both search for the same three-character
string ‘`Λ ω`’ mentioned earlier. However, because Bash translates
ANSI-C quoting before `grep` sees the pattern, this technique should not
be used to match printable ASCII characters; for example,
‘`grep $'\u005E'`’ is equivalent to ‘`grep '^'`’ and matches any line,
not just lines containing the character ‘`^`’ (U+005E CIRCUMFLEX
ACCENT).

Since PCREs and ANSI-C quoting are GNU extensions to POSIX, portable
shell scripts written in ASCII should use other methods to match
specific non-ASCII characters. For example, in a UTF-8 locale the
command ‘`grep "$(printf '\316\233\t\317\211\n')"`’ is a portable albeit
hard-to-read alternative to Bash’s ‘`grep $'Λ\tω'`’. However, none of
these techniques will let you put a null character directly into a
command-line pattern; null characters can appear only in a pattern
specified via the `-f` (`--file`) option.

------------------------------------------------------------------------

</div>

</div>

<div id="Usage" class="chapter">

<div class="header">

Next: <a href="#Performance" accesskey="n" rel="next">Performance</a>,
Previous:
<a href="#Regular-Expressions" accesskey="p" rel="prev">Regular
Expressions</a>, Up: <a href="#Top" accesskey="u" rel="up">grep</a>  
\[<a href="#SEC_Contents" rel="contents"
title="Table of contents">Contents</a>\]\[<a href="#Index" rel="index" title="Index">Index</a>\]

</div>

<span id="Usage-1"></span>

## 4 Usage

<span id="index-usage_002c-examples"></span>

Here is an example command that invokes GNU `grep`:

<div class="example">

``` example
grep -i 'hello.*world' menu.h main.c
```

</div>

This lists all lines in the files `menu.h` and `main.c` that contain the
string ‘`hello`’ followed by the string ‘`world`’; this is because
‘`.*`’ matches zero or more characters within a line. See [Regular
Expressions](#Regular-Expressions). The `-i` option causes `grep` to
ignore case, causing it to match the line ‘`Hello, world!`’, which it
would not otherwise match.

Here is a more complex example, showing the location and contents of any
line containing ‘`f`’ and ending in ‘`.c`’, within all files in the
current directory whose names start with non-‘`.`’, contain ‘`g`’, and
end in ‘`.h`’. The `-n` option outputs line numbers, the `--` argument
treats any later arguments as file names not options even if `*g*.h`
expands to a file name that starts with ‘`-`’, and the empty file
`/dev/null` causes file names to be output even if only one file name
happens to be of the form ‘`*g*.h`’.

<div class="example">

``` example
grep -n -- 'f.*\.c$' *g*.h /dev/null
```

</div>

Note that the regular expression syntax used in the pattern differs from
the globbing syntax that the shell uses to match file names.

See [Invoking `grep`](#Invoking), for more details about how to invoke
`grep`.

<span id="index-using-grep_002c-Q_0026A"></span> <span
id="index-FAQ-about-grep-usage"></span>

Here are some common questions and answers about `grep` usage.

1.  How can I list just the names of matching files?

    <div class="example">

    ``` example
    grep -l 'main' test-*.c
    ```

    </div>

    lists names of ‘`test-*.c`’ files in the current directory whose
    contents mention ‘`main`’.

2.  How do I search directories recursively?

    <div class="example">

    ``` example
    grep -r 'hello' /home/gigi
    ```

    </div>

    searches for ‘`hello`’ in all files under the `/home/gigi`
    directory. For more control over which files are searched, use
    `find` and `grep`. For example, the following command searches only
    C files:

    <div class="example">

    ``` example
    find /home/gigi -name '*.c' ! -type d \
      -exec grep -H 'hello' '{}' +
    ```

    </div>

    This differs from the command:

    <div class="example">

    ``` example
    grep -H 'hello' /home/gigi/*.c
    ```

    </div>

    which merely looks for ‘`hello`’ in non-hidden C files in
    `/home/gigi` whose names end in ‘`.c`’. The `find` command line
    above is more similar to the command:

    <div class="example">

    ``` example
    grep -r --include='*.c' 'hello' /home/gigi
    ```

    </div>

3.  What if a pattern or file has a leading ‘`-`’?

    <div class="example">

    ``` example
    grep -- '--cut here--' *
    ```

    </div>

    searches for all lines matching ‘`--cut here--`’. Without `--`,
    `grep` would attempt to parse ‘`--cut here--`’ as a list of options,
    and there would be similar problems with any file names beginning
    with ‘`-`’.

    Alternatively, you can prevent misinterpretation of leading ‘`-`’ by
    using `-e` for patterns and leading ‘`./`’ for files:

    <div class="example">

    ``` example
    grep -e '--cut here--' ./*
    ```

    </div>

4.  Suppose I want to search for a whole word, not a part of a word?

    <div class="example">

    ``` example
    grep -w 'hello' test*.log
    ```

    </div>

    searches only for instances of ‘`hello`’ that are entire words; it
    does not match ‘`Othello`’. For more control, use ‘`\<`’ and ‘`\>`’
    to match the start and end of words. For example:

    <div class="example">

    ``` example
    grep 'hello\>' test*.log
    ```

    </div>

    searches only for words ending in ‘`hello`’, so it matches the word
    ‘`Othello`’.

5.  How do I output context around the matching lines?

    <div class="example">

    ``` example
    grep -C 2 'hello' test*.log
    ```

    </div>

    prints two lines of context around each matching line.

6.  How do I force `grep` to print the name of the file?

    Append `/dev/null`:

    <div class="example">

    ``` example
    grep 'eli' /etc/passwd /dev/null
    ```

    </div>

    gets you:

    <div class="example">

    ``` example
    /etc/passwd:eli:x:2098:1000:Eli Smith:/home/eli:/bin/bash
    ```

    </div>

    Alternatively, use `-H`, which is a GNU extension:

    <div class="example">

    ``` example
    grep -H 'eli' /etc/passwd
    ```

    </div>

7.  Why do people use strange regular expressions on `ps` output?

    <div class="example">

    ``` example
    ps -ef | grep '[c]ron'
    ```

    </div>

    If the pattern had been written without the square brackets, it
    would have matched not only the `ps` output line for `cron`, but
    also the `ps` output line for `grep`. Note that on some platforms,
    `ps` limits the output to the width of the screen; `grep` does not
    have any limit on the length of a line except the available memory.

8.  Why does `grep` report “Binary file matches”?

    If `grep` listed all matching “lines” from a binary file, it would
    probably generate output that is not useful, and it might even muck
    up your display. So GNU `grep` suppresses output from files that
    appear to be binary files. To force GNU `grep` to output lines even
    from files that appear to be binary, use the `-a` or
    ‘`--binary-files=text`’ option. To eliminate the “Binary file
    matches” messages, use the `-I` or ‘`--binary-files=without-match`’
    option, or the `-s` or `--no-messages` option.

9.  Why doesn’t ‘`grep -lv`’ print non-matching file names?

    ‘`grep -lv`’ lists the names of all files containing one or more
    lines that do not match. To list the names of all files that contain
    no matching lines, use the `-L` or `--files-without-match` option.

10. I can do “OR” with ‘`|`’, but what about “AND”?

    <div class="example">

    ``` example
    grep 'paul' /etc/motd | grep 'franc,ois'
    ```

    </div>

    finds all lines that contain both ‘`paul`’ and ‘`franc,ois`’.

11. Why does the empty pattern match every input line?

    The `grep` command searches for lines that contain strings that
    match a pattern. Every line contains the empty string, so an empty
    pattern causes `grep` to find a match on each line. It is not the
    only such pattern: ‘`^`’, ‘`$`’, and many other patterns cause
    `grep` to match every line.

    To match empty lines, use the pattern ‘`^$`’. To match blank lines,
    use the pattern ‘`^[[:blank:]]*$`’. To match no lines at all, use
    the command ‘`grep -f /dev/null`’.

12. How can I search in both standard input and in files?

    Use the special file name ‘`-`’:

    <div class="example">

    ``` example
    cat /etc/passwd | grep 'alain' - /etc/motd
    ```

    </div>

13. Why is this back-reference failing?

    <div class="example">

    ``` example
    echo 'ba' | grep -E '(a)\1|b\1'
    ```

    </div>

    This outputs an error message, because the second ‘`\1`’ has nothing
    to refer back to, meaning it will never match anything.

14. How can I match across lines?

    Standard grep cannot do this, as it is fundamentally line-based.
    Therefore, merely using the `[:space:]` character class does not
    match newlines in the way you might expect.

    With the GNU `grep` option `-z` (`--null-data`), each input and
    output “line” is null-terminated; see [Other
    Options](#Other-Options). Thus, you can match newlines in the input,
    but typically if there is a match the entire input is output, so
    this usage is often combined with output-suppressing options like
    `-q`, e.g.:

    <div class="example">

    ``` example
    printf 'foo\nbar\n' | grep -z -q 'foo[[:space:]]\+bar'
    ```

    </div>

    If this does not suffice, you can transform the input before giving
    it to `grep`, or turn to `awk`, `sed`, `perl`, or many other
    utilities that are designed to operate across lines.

15. What do `grep`, `fgrep`, and `egrep` stand for?

    The name `grep` comes from the way line editing was done on Unix.
    For example, `ed` uses the following syntax to print a list of
    matching lines on the screen:

    <div class="example">

    ``` example
    global/regular expression/print
    g/re/p
    ```

    </div>

    `fgrep` stands for Fixed `grep`; `egrep` stands for Extended `grep`.

------------------------------------------------------------------------

</div>

<div id="Performance" class="chapter">

<div class="header">

Next:
<a href="#Reporting-Bugs" accesskey="n" rel="next">Reporting bugs</a>,
Previous: <a href="#Usage" accesskey="p" rel="prev">Usage</a>, Up:
<a href="#Top" accesskey="u" rel="up">grep</a>  
\[<a href="#SEC_Contents" rel="contents"
title="Table of contents">Contents</a>\]\[<a href="#Index" rel="index" title="Index">Index</a>\]

</div>

<span id="Performance-1"></span>

## 5 Performance

<span id="index-performance"></span>

Typically `grep` is an efficient way to search text. However, it can be
quite slow in some cases, and it can search large files where even minor
performance tweaking can help significantly. Although the algorithm used
by `grep` is an implementation detail that can change from release to
release, understanding its basic strengths and weaknesses can help you
improve its performance.

The `grep` command operates partly via a set of automata that are
designed for efficiency, and partly via a slower matcher that takes over
when the fast matchers run into unusual features like back-references.
When feasible, the Boyer–Moore fast string searching algorithm is used
to match a single fixed pattern, and the Aho–Corasick algorithm is used
to match multiple fixed patterns.

<span id="index-locales"></span>

Generally speaking `grep` operates more efficiently in single-byte
locales, since it can avoid the special processing needed for multi-byte
characters. If your patterns will work just as well that way, setting
`LC_ALL` to a single-byte locale can help performance considerably.
Setting ‘`LC_ALL='C'`’ can be particularly efficient, as `grep` is tuned
for that locale.

<span id="index-case-insensitive-search-1"></span>

Outside the ‘`C`’ locale, case-insensitive search, and search for
bracket expressions like ‘`[a-z]`’ and ‘`[[=a=]b]`’, can be surprisingly
inefficient due to difficulties in fast portable access to concepts like
multi-character collating elements.

<span id="index-back_002dreferences"></span>

A back-reference such as ‘`\1`’ can hurt performance significantly in
some cases, since back-references cannot in general be implemented via a
finite state automaton, and instead trigger a backtracking algorithm
that can be quite inefficient. For example, although the pattern
‘`^(.*)\1{14}(.*)\2{13}$`’ matches only lines whose lengths can be
written as a sum *15x + 14y* for nonnegative integers *x* and *y*, the
pattern matcher does not perform linear Diophantine analysis and instead
backtracks through all possible matching strings, using an algorithm
that is exponential in the worst case.

<span id="index-holes-in-files"></span>

On some operating systems that support files with holes—large regions of
zeros that are not physically present on secondary storage—`grep` can
skip over the holes efficiently without needing to read the zeros. This
optimization is not available if the `-a` (`--binary-files=text`) option
is used (see [File and Directory
Selection](#File-and-Directory-Selection)), unless the `-z`
(`--null-data`) option is also used (see [Other
Options](#Other-Options)).

For more about the algorithms used by `grep` and about related string
matching algorithms, see:

-   Aho AV. Algorithms for finding patterns in strings. In: van
    Leeuwen J. *Handbook of Theoretical Computer Science*, vol. A. New
    York: Elsevier; 1990. p. 255–300. This surveys classic string
    matching algorithms, some of which are used by `grep`.
-   Aho AV, Corasick MJ. Efficient string matching: an aid to
    bibliographic search. *CACM*. 1975;18(6):333–40.
    <https://dx.doi.org/10.1145/360825.360855>. This introduces the
    Aho–Corasick algorithm.
-   Boyer RS, Moore JS. A fast string searching algorithm. *CACM*.
    1977;20(10):762–72. <https://dx.doi.org/10.1145/359842.359859>. This
    introduces the Boyer–Moore algorithm.
-   Faro S, Lecroq T. The exact online string matching problem: a review
    of the most recent results. *ACM Comput Surv*. 2013;45(2):13.
    <https://dx.doi.org/10.1145/2431211.2431212>. This surveys string
    matching algorithms that might help improve the performance of
    `grep` in the future.

------------------------------------------------------------------------

</div>

<div id="Reporting-Bugs" class="chapter">

<div class="header">

Next: <a href="#Copying" accesskey="n" rel="next">Copying</a>, Previous:
<a href="#Performance" accesskey="p" rel="prev">Performance</a>, Up:
<a href="#Top" accesskey="u" rel="up">grep</a>  
\[<a href="#SEC_Contents" rel="contents"
title="Table of contents">Contents</a>\]\[<a href="#Index" rel="index" title="Index">Index</a>\]

</div>

<span id="Reporting-bugs"></span>

## 6 Reporting bugs

<span id="index-bugs_002c-reporting"></span>

Bug reports can be found at the [GNU bug report logs for
`grep`](https://debbugs.gnu.org/cgi/pkgreport.cgi?package=grep).

-   <a href="#Known-Bugs" accesskey="1">Known Bugs</a>

------------------------------------------------------------------------

<div id="Known-Bugs" class="section">

<div class="header">

Up: <a href="#Reporting-Bugs" accesskey="u" rel="up">Reporting bugs</a>
  \[<a href="#SEC_Contents" rel="contents"
title="Table of contents">Contents</a>\]\[<a href="#Index" rel="index" title="Index">Index</a>\]

</div>

<span id="Known-Bugs-1"></span>

### 6.1 Known Bugs

<span id="index-Bugs_002c-known"></span>

Large repetition counts in the ‘`{n,m}`’ construct may cause `grep` to
use lots of memory. In addition, certain other obscure regular
expressions require exponential time and space, and may cause `grep` to
run out of memory.

Back-references can greatly slow down matching, as they can generate
exponentially many matching possibilities that can consume both time and
memory to explore. Also, the POSIX specification for back-references is
at times unclear. Furthermore, many regular expression implementations
have back-reference bugs that can cause programs to return incorrect
answers or even crash, and fixing these bugs has often been
low-priority: for example, as of 2021 the [GNU C library bug
database](https://sourceware.org/bugzilla/) contained back-reference
bugs [52](https://sourceware.org/bugzilla/show_bug.cgi?id=52),
[10844](https://sourceware.org/bugzilla/show_bug.cgi?id=10844),
[11053](https://sourceware.org/bugzilla/show_bug.cgi?id=11053),
[24269](https://sourceware.org/bugzilla/show_bug.cgi?id=24269) and
[25322](https://sourceware.org/bugzilla/show_bug.cgi?id=25322), with
little sign of forthcoming fixes. Luckily, back-references are rarely
useful and it should be little trouble to avoid them in practical
applications.

------------------------------------------------------------------------

</div>

</div>

<div id="Copying" class="chapter">

<div class="header">

Next: <a href="#Index" accesskey="n" rel="next">Index</a>, Previous:
<a href="#Reporting-Bugs" accesskey="p" rel="prev">Reporting bugs</a>,
Up: <a href="#Top" accesskey="u" rel="up">grep</a>  
\[<a href="#SEC_Contents" rel="contents"
title="Table of contents">Contents</a>\]\[<a href="#Index" rel="index" title="Index">Index</a>\]

</div>

<span id="Copying-1"></span>

## 7 Copying

<span id="index-copying"></span>

GNU `grep` is licensed under the GNU GPL, which makes it *free
software*.

The “free” in “free software” refers to liberty, not price. As some GNU
project advocates like to point out, think of “free speech” rather than
“free beer”. In short, you have the right (freedom) to run and change
`grep` and distribute it to other people, and—if you want—charge money
for doing either. The important restriction is that you have to grant
your recipients the same rights and impose the same restrictions.

This general method of licensing software is sometimes called *open
source*. The GNU project prefers the term “free software” for reasons
outlined at
<https://www.gnu.org/philosophy/open-source-misses-the-point.html>.

This manual is free documentation in the same sense. The documentation
license is included below. The license for the program is available with
the source code, or at <https://www.gnu.org/licenses/gpl.html>.

-   <a href="#GNU-Free-Documentation-License" accesskey="1">GNU Free
    Documentation License</a>

------------------------------------------------------------------------

<div id="GNU-Free-Documentation-License" class="section">

<div class="header">

Up: <a href="#Copying" accesskey="u" rel="up">Copying</a>  
\[<a href="#SEC_Contents" rel="contents"
title="Table of contents">Contents</a>\]\[<a href="#Index" rel="index" title="Index">Index</a>\]

</div>

<span id="GNU-Free-Documentation-License-1"></span>

### 7.1 GNU Free Documentation License

<div align="center">

Version 1.3, 3 November 2008

</div>

<div class="display">

``` display
Copyright © 2000, 2001, 2002, 2007, 2008 Free Software Foundation, Inc.
https://fsf.org/

Everyone is permitted to copy and distribute verbatim copies
of this license document, but changing it is not allowed.
```

</div>


------------------------------------------------------------------------

</div>

</div>

<div id="Index" class="unnumbered">

<div class="header">

Previous: <a href="#Copying" accesskey="p" rel="prev">Copying</a>, Up:
<a href="#Top" accesskey="u" rel="up">grep</a>  
\[<a href="#SEC_Contents" rel="contents"
title="Table of contents">Contents</a>\]\[<a href="#Index" rel="index" title="Index">Index</a>\]

</div>

<span id="Index-1"></span>

## Index

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<th data-valign="top">Jump to:  </th>
<td><a href="#Index_cp_symbol-1"
class="summary-letter"><strong>*</strong></a>   <a
href="#Index_cp_symbol-2" class="summary-letter"><strong>+</strong></a>
  <a href="#Index_cp_symbol-3"
class="summary-letter"><strong>-</strong></a>   <a
href="#Index_cp_symbol-4" class="summary-letter"><strong>.</strong></a>
  <a href="#Index_cp_symbol-5"
class="summary-letter"><strong>?</strong></a>   <a
href="#Index_cp_symbol-6" class="summary-letter"><strong>_</strong></a>
  <a href="#Index_cp_symbol-7"
class="summary-letter"><strong>{</strong></a>  <br />
<a href="#Index_cp_letter-A"
class="summary-letter"><strong>A</strong></a>   <a
href="#Index_cp_letter-B" class="summary-letter"><strong>B</strong></a>
  <a href="#Index_cp_letter-C"
class="summary-letter"><strong>C</strong></a>   <a
href="#Index_cp_letter-D" class="summary-letter"><strong>D</strong></a>
  <a href="#Index_cp_letter-E"
class="summary-letter"><strong>E</strong></a>   <a
href="#Index_cp_letter-F" class="summary-letter"><strong>F</strong></a>
  <a href="#Index_cp_letter-G"
class="summary-letter"><strong>G</strong></a>   <a
href="#Index_cp_letter-H" class="summary-letter"><strong>H</strong></a>
  <a href="#Index_cp_letter-I"
class="summary-letter"><strong>I</strong></a>   <a
href="#Index_cp_letter-L" class="summary-letter"><strong>L</strong></a>
  <a href="#Index_cp_letter-M"
class="summary-letter"><strong>M</strong></a>   <a
href="#Index_cp_letter-N" class="summary-letter"><strong>N</strong></a>
  <a href="#Index_cp_letter-O"
class="summary-letter"><strong>O</strong></a>   <a
href="#Index_cp_letter-P" class="summary-letter"><strong>P</strong></a>
  <a href="#Index_cp_letter-Q"
class="summary-letter"><strong>Q</strong></a>   <a
href="#Index_cp_letter-R" class="summary-letter"><strong>R</strong></a>
  <a href="#Index_cp_letter-S"
class="summary-letter"><strong>S</strong></a>   <a
href="#Index_cp_letter-T" class="summary-letter"><strong>T</strong></a>
  <a href="#Index_cp_letter-U"
class="summary-letter"><strong>U</strong></a>   <a
href="#Index_cp_letter-V" class="summary-letter"><strong>V</strong></a>
  <a href="#Index_cp_letter-W"
class="summary-letter"><strong>W</strong></a>   <a
href="#Index_cp_letter-X" class="summary-letter"><strong>X</strong></a>
  <a href="#Index_cp_letter-Z"
class="summary-letter"><strong>Z</strong></a>  </td>
</tr>
</tbody>
</table>

<table class="index-cp" data-border="0">
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<th></th>
<td style="text-align: left;">Index Entry</td>
<td> </td>
<td style="text-align: left;">Section</td>
</tr>
<tr class="even">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th id="Index_cp_symbol-1">*</th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002a"><code>*</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Fundamental-Structure">Fundamental Structure</a></td>
</tr>
<tr class="odd">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th id="Index_cp_symbol-2">+</th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002b"><code>+</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Fundamental-Structure">Fundamental Structure</a></td>
</tr>
<tr class="even">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th id="Index_cp_symbol-3">-</th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002d"><code>--</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Other-Options">Other Options</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dafter_002dcontext"><code>--after-context</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Context-Line-Control">Context Line Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dbasic_002dregexp"><code>--basic-regexp</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#grep-Programs">grep Programs</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dbefore_002dcontext"><code>--before-context</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Context-Line-Control">Context Line Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dbinary"><code>--binary</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Other-Options">Other Options</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dbinary_002dfiles"><code>--binary-files</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dbyte_002doffset"><code>--byte-offset</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Output-Line-Prefix-Control">Output Line Prefix Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dcolor"><code>--color</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#General-Output-Control">General Output Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dcolour"><code>--colour</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#General-Output-Control">General Output Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dcontext"><code>--context</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Context-Line-Control">Context Line Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dcount"><code>--count</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#General-Output-Control">General Output Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002ddereference_002drecursive"><code>--dereference-recursive</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002ddevices"><code>--devices</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002ddirectories"><code>--directories</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dexclude"><code>--exclude</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dexclude_002ddir"><code>--exclude-dir</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dexclude_002dfrom"><code>--exclude-from</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dextended_002dregexp"><code>--extended-regexp</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#grep-Programs">grep Programs</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dfile"><code>--file</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Matching-Control">Matching Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dfiles_002dwith_002dmatches"><code>--files-with-matches</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#General-Output-Control">General Output Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dfiles_002dwithout_002dmatch"><code>--files-without-match</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#General-Output-Control">General Output Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dfixed_002dstrings"><code>--fixed-strings</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#grep-Programs">grep Programs</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dgroup_002dseparator"><code>--group-separator</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Context-Line-Control">Context Line Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dgroup_002dseparator-1"><code>--group-separator</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Context-Line-Control">Context Line Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dhelp"><code>--help</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Generic-Program-Information">Generic Program Information</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dignore_002dcase"><code>--ignore-case</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Matching-Control">Matching Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dinclude"><code>--include</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dinitial_002dtab"><code>--initial-tab</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Output-Line-Prefix-Control">Output Line Prefix Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dinvert_002dmatch"><code>--invert-match</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Matching-Control">Matching Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dlabel"><code>--label</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Output-Line-Prefix-Control">Output Line Prefix Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dline_002dbuffered"><code>--line-buffered</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Other-Options">Other Options</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dline_002dnumber"><code>--line-number</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Output-Line-Prefix-Control">Output Line Prefix Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dline_002dregexp"><code>--line-regexp</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Matching-Control">Matching Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dmax_002dcount"><code>--max-count</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#General-Output-Control">General Output Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dno_002dfilename"><code>--no-filename</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Output-Line-Prefix-Control">Output Line Prefix Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dno_002dignore_002dcase"><code>--no-ignore-case</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Matching-Control">Matching Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dno_002dmessages"><code>--no-messages</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#General-Output-Control">General Output Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dnull"><code>--null</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Output-Line-Prefix-Control">Output Line Prefix Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dnull_002ddata"><code>--null-data</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Other-Options">Other Options</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002donly_002dmatching"><code>--only-matching</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#General-Output-Control">General Output Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dperl_002dregexp"><code>--perl-regexp</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#grep-Programs">grep Programs</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dquiet"><code>--quiet</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#General-Output-Control">General Output Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002drecursive"><code>--recursive</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dregexp_003dpatterns"><code>--regexp=patterns</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Matching-Control">Matching Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dsilent"><code>--silent</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#General-Output-Control">General Output Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dtext"><code>--text</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dversion"><code>--version</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Generic-Program-Information">Generic Program Information</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dwith_002dfilename"><code>--with-filename</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Output-Line-Prefix-Control">Output Line Prefix Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002d_002dword_002dregexp"><code>--word-regexp</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Matching-Control">Matching Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002dA"><code>-A</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Context-Line-Control">Context Line Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002da"><code>-a</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002db"><code>-b</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Output-Line-Prefix-Control">Output Line Prefix Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002dB"><code>-B</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Context-Line-Control">Context Line Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002dc"><code>-c</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#General-Output-Control">General Output Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002dC"><code>-C</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Context-Line-Control">Context Line Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002dD"><code>-D</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002dd"><code>-d</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002de"><code>-e</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Matching-Control">Matching Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002dE"><code>-E</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#grep-Programs">grep Programs</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002df"><code>-f</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Matching-Control">Matching Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002dF"><code>-F</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#grep-Programs">grep Programs</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002dG"><code>-G</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#grep-Programs">grep Programs</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002dH"><code>-H</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Output-Line-Prefix-Control">Output Line Prefix Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002dh"><code>-h</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Output-Line-Prefix-Control">Output Line Prefix Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002di"><code>-i</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Matching-Control">Matching Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002dL"><code>-L</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#General-Output-Control">General Output Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002dl"><code>-l</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#General-Output-Control">General Output Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002dm"><code>-m</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#General-Output-Control">General Output Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002dn"><code>-n</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Output-Line-Prefix-Control">Output Line Prefix Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002dnum"><code>-num</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Context-Line-Control">Context Line Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002do"><code>-o</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#General-Output-Control">General Output Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002dP"><code>-P</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#grep-Programs">grep Programs</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002dq"><code>-q</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#General-Output-Control">General Output Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002dr"><code>-r</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002dR"><code>-R</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002ds"><code>-s</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#General-Output-Control">General Output Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002dT"><code>-T</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Output-Line-Prefix-Control">Output Line Prefix Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002dU"><code>-U</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Other-Options">Other Options</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002dV"><code>-V</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Generic-Program-Information">Generic Program Information</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002dv"><code>-v</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Matching-Control">Matching Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002dw"><code>-w</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Matching-Control">Matching Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002dx"><code>-x</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Matching-Control">Matching Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002dy"><code>-y</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Matching-Control">Matching Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002dZ"><code>-Z</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Output-Line-Prefix-Control">Output Line Prefix Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002dz"><code>-z</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Other-Options">Other Options</a></td>
</tr>
<tr class="odd">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th id="Index_cp_symbol-4">.</th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_002e"><code>.</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Fundamental-Structure">Fundamental Structure</a></td>
</tr>
<tr class="even">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th id="Index_cp_symbol-5">?</th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_003f"><code>?</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Fundamental-Structure">Fundamental Structure</a></td>
</tr>
<tr class="odd">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th id="Index_cp_symbol-6">_</th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_005fN_005fGNU_005fnonoption_005fargv_005fflags_005f-environment-variable"><code>_N_GNU_nonoption_argv_flags_ environment variable</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="even">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th id="Index_cp_symbol-7">{</th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_007b_002cm_007d"><code>{,m}</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Fundamental-Structure">Fundamental Structure</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_007bn_002cm_007d"><code>{n,m}</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Fundamental-Structure">Fundamental Structure</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_007bn_002c_007d"><code>{n,}</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Fundamental-Structure">Fundamental Structure</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-_007bn_007d"><code>{n}</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Fundamental-Structure">Fundamental Structure</a></td>
</tr>
<tr class="even">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th id="Index_cp_letter-A">A</th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-after-context">after context</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Context-Line-Control">Context Line Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-alnum-character-class"><code>alnum character class</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-alpha-character-class"><code>alpha character class</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-alphabetic-characters">alphabetic characters</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-alphanumeric-characters">alphanumeric characters</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-anchoring">anchoring</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Anchoring">Anchoring</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-asterisk">asterisk</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Fundamental-Structure">Fundamental Structure</a></td>
</tr>
<tr class="odd">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th id="Index_cp_letter-B">B</th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-back_002dreference">back-reference</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Back_002dreferences-and-Subexpressions">Back-references and
Subexpressions</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-back_002dreferences">back-references</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Performance">Performance</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-backslash">backslash</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#The-Backslash-Character-and-Special-Expressions">The Backslash
Character and Special Expressions</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-basic-regular-expressions">basic regular
expressions</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Basic-vs-Extended">Basic vs Extended</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-before-context">before context</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Context-Line-Control">Context Line Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-binary-files">binary files</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-binary-files-1">binary files</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-binary-I_002fO">binary I/O</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Other-Options">Other Options</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-blank-character-class"><code>blank character class</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-blank-characters">blank characters</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-bn-GREP_005fCOLORS-capability"><code>bn GREP_COLORS capability</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-braces_002c-first-argument-omitted">braces, first argument
omitted</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Fundamental-Structure">Fundamental Structure</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-braces_002c-one-argument">braces, one argument</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Fundamental-Structure">Fundamental Structure</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-braces_002c-second-argument-omitted">braces, second
argument omitted</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Fundamental-Structure">Fundamental Structure</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-braces_002c-two-arguments">braces, two arguments</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Fundamental-Structure">Fundamental Structure</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-bracket-expression">bracket expression</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-Bugs_002c-known">Bugs, known</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Known-Bugs">Known Bugs</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-bugs_002c-reporting">bugs, reporting</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Reporting-Bugs">Reporting Bugs</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-byte-offset">byte offset</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Output-Line-Prefix-Control">Output Line Prefix Control</a></td>
</tr>
<tr class="even">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th id="Index_cp_letter-C">C</th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-case-insensitive-search">case insensitive search</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Matching-Control">Matching Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-case-insensitive-search-1">case insensitive
search</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Performance">Performance</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-changing-name-of-standard-input">changing name of standard
input</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Output-Line-Prefix-Control">Output Line Prefix Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-character-class">character class</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-character-classes">character classes</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-character-encoding">character encoding</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Encoding">Character Encoding</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-character-type">character type</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-classes-of-characters">classes of characters</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-cntrl-character-class"><code>cntrl character class</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-context-lines">context lines</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#General-Output-Control">General Output Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-context-lines-1">context lines</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Context-Line-Control">Context Line Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-context-lines-2">context lines</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Context-Line-Control">Context Line Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-context-lines_002c-after-match">context lines, after
match</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Context-Line-Control">Context Line Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-context-lines_002c-before-match">context lines, before
match</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Context-Line-Control">Context Line Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-control-characters">control characters</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-copying">copying</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Copying">Copying</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-counting-lines">counting lines</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#General-Output-Control">General Output Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-cx-GREP_005fCOLORS-capability"><code>cx GREP_COLORS capability</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="even">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th id="Index_cp_letter-D">D</th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-device-search">device search</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-digit-character-class"><code>digit character class</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-digit-characters">digit characters</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-directory-search">directory search</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-dot">dot</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Fundamental-Structure">Fundamental Structure</a></td>
</tr>
<tr class="odd">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th id="Index_cp_letter-E">E</th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-encoding-error">encoding error</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-environment-variables">environment variables</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-exclude-directories">exclude directories</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-exclude-files">exclude files</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-exclude-files-1">exclude files</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-exit-status">exit status</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Exit-Status">Exit Status</a></td>
</tr>
<tr class="odd">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th id="Index_cp_letter-F">F</th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-FAQ-about-grep-usage">FAQ about <code>grep</code>
usage</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Usage">Usage</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-files-which-don_0027t-match">files which don’t
match</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#General-Output-Control">General Output Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-fn-GREP_005fCOLORS-capability"><code>fn GREP_COLORS capability</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-fn-GREP_005fCOLORS-capability-1"><code>fn GREP_COLORS capability</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="odd">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th id="Index_cp_letter-G">G</th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-graph-character-class"><code>graph character class</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-graphic-characters">graphic characters</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-grep-programs"><code>grep</code> programs</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#grep-Programs">grep Programs</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-GREP_005fCOLOR-environment-variable"><code>GREP_COLOR environment variable</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-GREP_005fCOLORS-environment-variable"><code>GREP_COLORS environment variable</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-group-separator">group separator</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Context-Line-Control">Context Line Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-group-separator-1">group separator</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Context-Line-Control">Context Line Control</a></td>
</tr>
<tr class="even">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th id="Index_cp_letter-H">H</th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-hexadecimal-digits">hexadecimal digits</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-highlight-markers">highlight markers</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-highlight-markers-1">highlight markers</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-highlight_002c-color_002c-colour">highlight, color,
colour</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#General-Output-Control">General Output Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-holes-in-files">holes in files</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Performance">Performance</a></td>
</tr>
<tr class="odd">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th id="Index_cp_letter-I">I</th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-include-files">include files</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-interval-expressions">interval expressions</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Fundamental-Structure">Fundamental Structure</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-interval-expressions-1">interval expressions</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Basic-vs-Extended">Basic vs Extended</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-invert-matching">invert matching</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Matching-Control">Matching Control</a></td>
</tr>
<tr class="odd">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th id="Index_cp_letter-L">L</th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-LANG-environment-variable"><code>LANG environment variable</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-LANG-environment-variable-1"><code>LANG environment variable</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-LANG-environment-variable-2"><code>LANG environment variable</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-LANG-environment-variable-3"><code>LANG environment variable</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-LANGUAGE-environment-variable"><code>LANGUAGE environment variable</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-LANGUAGE-environment-variable-1"><code>LANGUAGE environment variable</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-language-of-messages">language of messages</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-LC_005fALL-environment-variable"><code>LC_ALL environment variable</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-LC_005fALL-environment-variable-1"><code>LC_ALL environment variable</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-LC_005fALL-environment-variable-2"><code>LC_ALL environment variable</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-LC_005fALL-environment-variable-3"><code>LC_ALL environment variable</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-LC_005fCOLLATE-environment-variable"><code>LC_COLLATE environment variable</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-LC_005fCTYPE-environment-variable"><code>LC_CTYPE environment variable</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-LC_005fMESSAGES-environment-variable"><code>LC_MESSAGES environment variable</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-LC_005fMESSAGES-environment-variable-1"><code>LC_MESSAGES environment variable</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-line-buffering">line buffering</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Other-Options">Other Options</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-line-numbering">line numbering</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Output-Line-Prefix-Control">Output Line Prefix Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-ln-GREP_005fCOLORS-capability"><code>ln GREP_COLORS capability</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-locales">locales</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Performance">Performance</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-lower-character-class"><code>lower character class</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-lower_002dcase-letters">lower-case letters</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="even">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th id="Index_cp_letter-M">M</th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-match-expression-at-most-m-times">match expression at most
<var>m</var> times</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Fundamental-Structure">Fundamental Structure</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-match-expression-at-most-once">match expression at most
once</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Fundamental-Structure">Fundamental Structure</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-match-expression-from-n-to-m-times">match expression from
<var>n</var> to <var>m</var> times</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Fundamental-Structure">Fundamental Structure</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-match-expression-n-or-more-times">match expression
<var>n</var> or more times</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Fundamental-Structure">Fundamental Structure</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-match-expression-n-times">match expression <var>n</var>
times</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Fundamental-Structure">Fundamental Structure</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-match-expression-one-or-more-times">match expression one or
more times</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Fundamental-Structure">Fundamental Structure</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-match-expression-zero-or-more-times">match expression zero
or more times</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Fundamental-Structure">Fundamental Structure</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-match-the-whole-line">match the whole line</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Matching-Control">Matching Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-matching-basic-regular-expressions">matching basic regular
expressions</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#grep-Programs">grep Programs</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-matching-extended-regular-expressions">matching extended
regular expressions</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#grep-Programs">grep Programs</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-matching-fixed-strings">matching fixed strings</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#grep-Programs">grep Programs</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-matching-Perl_002dcompatible-regular-expressions">matching
Perl-compatible regular expressions</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#grep-Programs">grep Programs</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-matching-whole-words">matching whole words</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Matching-Control">Matching Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-max_002dcount">max-count</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#General-Output-Control">General Output Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-mc-GREP_005fCOLORS-capability"><code>mc GREP_COLORS capability</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-message-language">message language</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-ms-GREP_005fCOLORS-capability"><code>ms GREP_COLORS capability</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-MS_002dWindows-binary-I_002fO">MS-Windows binary
I/O</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Other-Options">Other Options</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-mt-GREP_005fCOLORS-capability"><code>mt GREP_COLORS capability</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="odd">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th id="Index_cp_letter-N">N</th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-names-of-matching-files">names of matching files</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#General-Output-Control">General Output Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-national-language-support">national language
support</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-national-language-support-1">national language
support</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-ne-GREP_005fCOLORS-capability"><code>ne GREP_COLORS capability</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-NLS">NLS</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-no-filename-prefix">no filename prefix</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Output-Line-Prefix-Control">Output Line Prefix Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-non_002dASCII-matching">non-ASCII matching</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Matching-Non_002dASCII">Matching Non-ASCII</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-non_002dprintable-matching">non-printable
matching</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Matching-Non_002dASCII">Matching Non-ASCII</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-null-character">null character</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-numeric-characters">numeric characters</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="odd">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th id="Index_cp_letter-O">O</th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-only-matching">only matching</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#General-Output-Control">General Output Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-option-delimiter">option delimiter</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Other-Options">Other Options</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-ordinary-characters">ordinary characters</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Fundamental-Structure">Fundamental Structure</a></td>
</tr>
<tr class="even">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th id="Index_cp_letter-P">P</th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-patterns-from-file">patterns from file</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Matching-Control">Matching Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-patterns-option">patterns option</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Matching-Control">Matching Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-performance">performance</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Performance">Performance</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-period">period</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Fundamental-Structure">Fundamental Structure</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-plus-sign">plus sign</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Fundamental-Structure">Fundamental Structure</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-POSIXLY_005fCORRECT-environment-variable"><code>POSIXLY_CORRECT environment variable</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-print-character-class"><code>print character class</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-print-non_002dmatching-lines">print non-matching
lines</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Matching-Control">Matching Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-printable-characters">printable characters</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-punct-character-class"><code>punct character class</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-punctuation-characters">punctuation characters</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="odd">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th id="Index_cp_letter-Q">Q</th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-question-mark">question mark</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Fundamental-Structure">Fundamental Structure</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-quiet_002c-silent">quiet, silent</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#General-Output-Control">General Output Control</a></td>
</tr>
<tr class="odd">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th id="Index_cp_letter-R">R</th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-range-expression">range expression</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-recursive-search">recursive search</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-recursive-search-1">recursive search</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-regular-expressions">regular expressions</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Regular-Expressions">Regular Expressions</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-return-status">return status</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Exit-Status">Exit Status</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-rv-GREP_005fCOLORS-capability"><code>rv GREP_COLORS capability</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="odd">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th id="Index_cp_letter-S">S</th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-searching-directory-trees">searching directory
trees</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-searching-directory-trees-1">searching directory
trees</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-searching-directory-trees-2">searching directory
trees</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-searching-directory-trees-3">searching directory
trees</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-searching-directory-trees-4">searching directory
trees</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-searching-for-patterns">searching for patterns</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Introduction">Introduction</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-sl-GREP_005fCOLORS-capability"><code>sl GREP_COLORS capability</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-space-character-class"><code>space character class</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-space-characters">space characters</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-special-characters">special characters</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Fundamental-Structure">Fundamental Structure</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-subexpression">subexpression</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Back_002dreferences-and-Subexpressions">Back-references and
Subexpressions</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-suppress-binary-data">suppress binary data</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-suppress-error-messages">suppress error messages</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#General-Output-Control">General Output Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-symbolic-links">symbolic links</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-symbolic-links-1">symbolic links</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-symbolic-links-2">symbolic links</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#File-and-Directory-Selection">File and Directory
Selection</a></td>
</tr>
<tr class="odd">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th id="Index_cp_letter-T">T</th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-tab_002daligned-content-lines">tab-aligned content
lines</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Output-Line-Prefix-Control">Output Line Prefix Control</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-translation-of-message-language">translation of message
language</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Environment-Variables">Environment Variables</a></td>
</tr>
<tr class="odd">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th id="Index_cp_letter-U">U</th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-upper-character-class"><code>upper character class</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-upper_002dcase-letters">upper-case letters</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-usage-summary_002c-printing">usage summary,
printing</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Generic-Program-Information">Generic Program Information</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-usage_002c-examples">usage, examples</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Usage">Usage</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-using-grep_002c-Q_0026A">using <code>grep</code>,
Q&amp;A</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Usage">Usage</a></td>
</tr>
<tr class="even">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th id="Index_cp_letter-V">V</th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-variants-of-grep">variants of <code>grep</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#grep-Programs">grep Programs</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-version_002c-printing">version, printing</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Generic-Program-Information">Generic Program Information</a></td>
</tr>
<tr class="even">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th id="Index_cp_letter-W">W</th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-whitespace-characters">whitespace characters</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-with-filename-prefix">with filename prefix</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Output-Line-Prefix-Control">Output Line Prefix Control</a></td>
</tr>
<tr class="even">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th id="Index_cp_letter-X">X</th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-xdigit-character-class"><code>xdigit character class</code></a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-xdigit-class">xdigit class</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Character-Classes-and-Bracket-Expressions">Character Classes and
Bracket Expressions</a></td>
</tr>
<tr class="even">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th id="Index_cp_letter-Z">Z</th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-zero_002dterminated-file-names">zero-terminated file
names</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Output-Line-Prefix-Control">Output Line Prefix Control</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-zero_002dterminated-lines">zero-terminated lines</a>:</td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Other-Options">Other Options</a></td>
</tr>
<tr class="even">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
</tbody>
</table>

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<th data-valign="top">Jump to:  </th>
<td><a href="#Index_cp_symbol-1"
class="summary-letter"><strong>*</strong></a>   <a
href="#Index_cp_symbol-2" class="summary-letter"><strong>+</strong></a>
  <a href="#Index_cp_symbol-3"
class="summary-letter"><strong>-</strong></a>   <a
href="#Index_cp_symbol-4" class="summary-letter"><strong>.</strong></a>
  <a href="#Index_cp_symbol-5"
class="summary-letter"><strong>?</strong></a>   <a
href="#Index_cp_symbol-6" class="summary-letter"><strong>_</strong></a>
  <a href="#Index_cp_symbol-7"
class="summary-letter"><strong>{</strong></a>  <br />
<a href="#Index_cp_letter-A"
class="summary-letter"><strong>A</strong></a>   <a
href="#Index_cp_letter-B" class="summary-letter"><strong>B</strong></a>
  <a href="#Index_cp_letter-C"
class="summary-letter"><strong>C</strong></a>   <a
href="#Index_cp_letter-D" class="summary-letter"><strong>D</strong></a>
  <a href="#Index_cp_letter-E"
class="summary-letter"><strong>E</strong></a>   <a
href="#Index_cp_letter-F" class="summary-letter"><strong>F</strong></a>
  <a href="#Index_cp_letter-G"
class="summary-letter"><strong>G</strong></a>   <a
href="#Index_cp_letter-H" class="summary-letter"><strong>H</strong></a>
  <a href="#Index_cp_letter-I"
class="summary-letter"><strong>I</strong></a>   <a
href="#Index_cp_letter-L" class="summary-letter"><strong>L</strong></a>
  <a href="#Index_cp_letter-M"
class="summary-letter"><strong>M</strong></a>   <a
href="#Index_cp_letter-N" class="summary-letter"><strong>N</strong></a>
  <a href="#Index_cp_letter-O"
class="summary-letter"><strong>O</strong></a>   <a
href="#Index_cp_letter-P" class="summary-letter"><strong>P</strong></a>
  <a href="#Index_cp_letter-Q"
class="summary-letter"><strong>Q</strong></a>   <a
href="#Index_cp_letter-R" class="summary-letter"><strong>R</strong></a>
  <a href="#Index_cp_letter-S"
class="summary-letter"><strong>S</strong></a>   <a
href="#Index_cp_letter-T" class="summary-letter"><strong>T</strong></a>
  <a href="#Index_cp_letter-U"
class="summary-letter"><strong>U</strong></a>   <a
href="#Index_cp_letter-V" class="summary-letter"><strong>V</strong></a>
  <a href="#Index_cp_letter-W"
class="summary-letter"><strong>W</strong></a>   <a
href="#Index_cp_letter-X" class="summary-letter"><strong>X</strong></a>
  <a href="#Index_cp_letter-Z"
class="summary-letter"><strong>Z</strong></a>  </td>
</tr>
</tbody>
</table>

</div>

</div>

<div class="footnote">

------------------------------------------------------------------------

#### Footnotes

##### <a href="#DOCF1" id="FOOT1">(1)</a>

Of course, 7th Edition Unix predated POSIX by several years!

</div>
