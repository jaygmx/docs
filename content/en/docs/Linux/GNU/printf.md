---
title:  "printf"
linkTitle::  "printf"
weight: 100
description: >-
     printf
---

# ‘printf’: Format and print data

‘printf’ does formatted printing of text.
Synopsis:

``` 
 printf FORMAT [ARGUMENT]...
```

‘printf’ prints the FORMAT string, interpreting ‘%’ directives and ‘\\’
escapes to format numeric and string arguments in a way that is mostly
similar to the C ‘printf’ function. \*Note ‘printf’ format directives:
(libc)Output Conversion Syntax, for details. The differences are listed
below.

Due to shell aliases and built-in ‘printf’ functions, using an unadorned
‘printf’ interactively or in a script may get you different
functionality than that described here. Invoke it via ‘env’ (i.e., ‘env
printf ...’) to avoid interference from the shell.

• The FORMAT argument is reused as necessary to convert all the given
ARGUMENTs. For example, the command ‘printf %s a b’ outputs ‘ab’.

• Missing ARGUMENTs are treated as null strings or as zeros, depending
on whether the context expects a string or a number. For example, the
command ‘printf %sx%d’ prints ‘x0’.

• An additional escape, ‘\\c’, causes ‘printf’ to produce no further
output. For example, the command ‘printf 'A%sC\\cD%sF' B E’ prints
‘ABC’.

• The hexadecimal escape sequence ‘\\xHH’ has at most two digits, as
opposed to C where it can have an unlimited number of digits. For
example, the command ‘printf '\\x07e'’ prints two bytes, whereas the C
statement ‘printf ("\\x07e")’ prints just one.

• An additional directive ‘%b’, prints its argument string with ‘\\’
escapes interpreted in the same way as in the FORMAT string, except that
octal escapes are of the form ‘\\0OOO’ where OOO is 0 to 3 octal digits.
If ‘\\OOO’ is nine-bit value, ignore the ninth bit. If a precision is
also given, it limits the number of bytes printed from the converted
string.

• An additional directive ‘%q’, prints its argument string in a format
that can be reused as input by most shells. Non-printable characters are
escaped with the POSIX proposed ‘$''’ syntax, and shell metacharacters
are quoted appropriately. This is an equivalent format to ‘ls
--quoting=shell-escape’ output.

• Numeric arguments must be single C constants, possibly with leading
‘+’ or ‘-’. For example, ‘printf %.4d -3’ outputs ‘-0003’.

• If the leading character of a numeric argument is ‘"’ or ‘'’ then its
value is the numeric value of the immediately following character. Any
remaining characters are silently ignored if the ‘POSIXLY\_CORRECT’
environment variable is set; otherwise, a warning is printed. For
example, ‘printf "%d" "'a"’ outputs ‘97’ on hosts that use the ASCII
character set, since ‘a’ has the numeric value 97 in ASCII.

A floating-point argument must use a period before any fractional
digits, but is printed according to the ‘LC\_NUMERIC’ category of the
current locale. For example, in a locale whose radix character is a
comma, the command ‘printf %g 3.14’ outputs ‘3,14’ whereas the command
‘printf %g 3,14’ is an error. \*Note Floating point::.

‘printf’ interprets ‘\\OOO’ in FORMAT as an octal number (if OOO is 1 to
3 octal digits) specifying a byte to print, and ‘\\xHH’ as a hexadecimal
number (if HH is 1 to 2 hex digits) specifying a character to print.
Note however that when ‘\\OOO’ specifies a number larger than 255,
‘printf’ ignores the ninth bit. For example, ‘printf '\\400'’ is
equivalent to ‘printf '\\0'’.

‘printf’ interprets two character syntaxes introduced in ISO C 99: ‘\\u’
for 16-bit Unicode (ISO/IEC 10646) characters, specified as four
hexadecimal digits HHHH, and ‘\\U’ for 32-bit Unicode characters,
specified as eight hexadecimal digits HHHHHHHH. ‘printf’ outputs the
Unicode characters according to the ‘LC\_CTYPE’ locale. Unicode
characters in the ranges U+0000...U+009F, U+D800...U+DFFF cannot be
specified by this syntax, except for U+0024 ($), U+0040 (@), and U+0060
()̀.

The processing of ‘\\u’ and ‘\\U’ requires a full-featured ‘iconv’
facility. It is activated on systems with glibc 2.2 (or newer), or when
‘libiconv’ is installed prior to this package. Otherwise ‘\\u’ and
‘\\U’ will print as-is.

The only options are a lone ‘--help’ or ‘--version’. \*Note Common
options::. Options must precede operands.

The Unicode character syntaxes are useful for writing strings in a
locale independent way. For example, a string containing the Euro
currency symbol

``` 
 $ env printf '\u20AC 14.95'
```

will be output correctly in all locales supporting the Euro symbol
(ISO-8859-15, UTF-8, and others). Similarly, a Chinese string

``` 
 $ env printf '\u4e2d\u6587'
```

will be output correctly in all Chinese locales (GB2312, BIG5, UTF-8,
etc).

Note that in these examples, the ‘printf’ command has been invoked via
‘env’ to ensure that we run the program found via your shell’s search
path, and not a shell alias or a built-in function.

For larger strings, you don’t need to look up the hexadecimal code
values of each character one by one. ASCII characters mixed with \\u
escape sequences is also known as the JAVA source file encoding. You can
use GNU recode 3.5c (or newer) to convert strings to this encoding. Here
is how to convert a piece of text into a shell script which will output
this text in a locale-independent way:

``` 
 $ LC_CTYPE=zh_CN.big5 /usr/local/bin/printf \
     '\u4e2d\u6587\n' > sample.txt
 $ recode BIG5..JAVA < sample.txt \
     | sed -e "s|^|/usr/local/bin/printf '|" -e "s|$|\\\\n'|" \
     > sample.sh
```

An exit status of zero indicates success, and a nonzero value indicates
failure.
