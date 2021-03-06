---
title:  "numfmt"
linkTitle::  "numfmt"
weight: 100
description: >-
     numfmt
---

# ‘numfmt’: Reformat numbers

‘numfmt’ reads numbers in various representations and reformats them as
requested. The most common usage is converting numbers to/from *human*
representation (e.g. ‘4G’ ↦ ‘4,000,000,000’).

``` 
 numfmt [OPTION]... [NUMBER]
```

‘numfmt’ converts each NUMBER on the command-line according to the
specified options (see below). If no NUMBERs are given, it reads numbers
from standard input. ‘numfmt’ can optionally extract numbers from
specific columns, maintaining proper line padding and alignment.

An exit status of zero indicates success, and a nonzero value indicates
failure.

See ‘--invalid’ for additional information regarding exit status.

## General options

The program accepts the following options. Also see \*note Common
options::.

‘--debug’ Print (to standard error) warning messages about possible
erroneous usage.

‘-d D’ ‘--delimiter=D’ Use the character D as input field separator
(default: whitespace). *Note*: Using non-default delimiter turns off
automatic padding.

‘--field=FIELDS’ Convert the number in input field FIELDS (default: 1).
FIELDS supports ‘cut’ style field ranges:

``` 
      N    N'th field, counted from 1
      N-   from N'th field, to end of line
      N-M  from N'th to M'th field (inclusive)
      -M   from first to M'th field (inclusive)
      -    all fields
```

‘--format=FORMAT’ Use printf-style floating FORMAT string. The FORMAT
string must contain one ‘%f’ directive, optionally with ‘'’, ‘-’, ‘0’,
width or precision modifiers. The ‘'’ modifier will enable ‘--grouping’,
the ‘-’ modifier will enable left-aligned ‘--padding’ and the width
modifier will enable right-aligned ‘--padding’. The ‘0’ width modifier
(without the ‘-’ modifier) will generate leading zeros on the number, up
to the specified width. A precision specification like ‘%.1f’ will
override the precision determined from the input data or set due to
‘--to’ option auto scaling.

‘--from=UNIT’ Auto-scales input numbers according to UNIT. See UNITS
below. The default is no scaling, meaning suffixes (e.g. ‘M’, ‘G’) will
trigger an error.

‘--from-unit=N’ Specify the input unit size (instead of the default 1).
Use this option when the input numbers represent other units (e.g. if
the input number ‘10’ represents 10 units of 512 bytes, use
‘--from-unit=512’). Suffixes are handled as with ‘--from=auto’.

‘--grouping’ Group digits in output numbers according to the current
locale’s grouping rules (e.g *Thousands Separator* character, commonly
‘.’ (dot) or ‘,’ comma). This option has no effect in ‘POSIX/C’
locale.

‘--header\[=N\]’ Print the first N (default: 1) lines without any
conversion.

‘--invalid=MODE’ The default action on input errors is to exit
immediately with status code 2. ‘--invalid=‘abort’’ explicitly specifies
this default mode. With a MODE of ‘fail’, print a warning for *each*
conversion error, and exit with status 2. With a MODE of ‘warn’, exit
with status 0, even in the presence of conversion errors, and with a
MODE of ‘ignore’ do not even print diagnostics.

‘--padding=N’ Pad the output numbers to N characters, by adding spaces.
If N is a positive number, numbers will be right-aligned. If N is a
negative number, numbers will be left-aligned. By default, numbers are
automatically aligned based on the input line’s width (only with the
default delimiter).

‘--round=METHOD’ When converting number representations, round the
number according to METHOD, which can be ‘up’, ‘down’, ‘from-zero’ (the
default), ‘towards-zero’, ‘nearest’.

‘--suffix=SUFFIX’ Add ‘SUFFIX’ to the output numbers, and accept
optional ‘SUFFIX’ in input numbers.

‘--to=UNIT’ Auto-scales output numbers according to UNIT. See *Units*
below. The default is no scaling, meaning all the digits of the number
are printed.

‘--to-unit=N’ Specify the output unit size (instead of the default 1).
Use this option when the output numbers represent other units (e.g. to
represent ‘4,000,000’ bytes in blocks of 1KB, use ‘--to=si
--to-unit=1000’). Suffixes are handled as with ‘--from=auto’.

‘-z’ ‘--zero-terminated’ Delimit items with a zero byte rather than a
newline (ASCII LF). I.e., treat input as items separated by ASCII NUL
and terminate output items with ASCII NUL. This option can be useful in
conjunction with ‘perl -0’ or ‘find -print0’ and ‘xargs -0’ which do the
same in order to reliably handle arbitrary file names (even those
containing blanks or other special characters). Note with ‘-z’ the
newline character is treated as a field separator.

## Possible UNITs:

The following are the possible UNIT options with ‘--from=UNITS’ and
‘--to=UNITS’:

NONE No scaling is performed. For input numbers, no suffixes are
accepted, and any trailing characters following the number will trigger
an error. For output numbers, all digits of the numbers will be printed.

SI Auto-scale numbers according to the *International System of Units
(SI)* standard. For input numbers, accept one of the following suffixes.
For output numbers, values larger than 1000 will be rounded, and printed
with one of the following suffixes:

``` 
      ‘K’  =>  1000^1 = 10^3 (Kilo)
      ‘M’  =>  1000^2 = 10^6 (Mega)
      ‘G’  =>  1000^3 = 10^9 (Giga)
      ‘T’  =>  1000^4 = 10^{12} (Tera)
      ‘P’  =>  1000^5 = 10^{15} (Peta)
      ‘E’  =>  1000^6 = 10^{18} (Exa)
      ‘Z’  =>  1000^7 = 10^{21} (Zetta)
      ‘Y’  =>  1000^8 = 10^{24} (Yotta)
```

IEC Auto-scale numbers according to the *International Electrotechnical
Commission (IEC)* standard. For input numbers, accept one of the
following suffixes. For output numbers, values larger than 1024 will be
rounded, and printed with one of the following suffixes:

``` 
      ‘K’  =>  1024^1 = 2^{10} (Kibi)
      ‘M’  =>  1024^2 = 2^{20} (Mebi)
      ‘G’  =>  1024^3 = 2^{30} (Gibi)
      ‘T’  =>  1024^4 = 2^{40} (Tebi)
      ‘P’  =>  1024^5 = 2^{50} (Pebi)
      ‘E’  =>  1024^6 = 2^{60} (Exbi)
      ‘Z’  =>  1024^7 = 2^{70} (Zebi)
      ‘Y’  =>  1024^8 = 2^{80} (Yobi)

 The ‘iec’ option uses a single letter suffix (e.g.  ‘G’), which is
 not fully standard, as the _iec_ standard recommends a two-letter
 symbol (e.g ‘Gi’) - but in practice, this method common.  Compare
 with the ‘iec-i’ option.
```

IEC-I Auto-scale numbers according to the *International
Electrotechnical Commission (IEC)* standard. For input numbers, accept
one of the following suffixes. For output numbers, values larger than
1024 will be rounded, and printed with one of the following suffixes:

``` 
      ‘Ki’  =>  1024^1 = 2^{10} (Kibi)
      ‘Mi’  =>  1024^2 = 2^{20} (Mebi)
      ‘Gi’  =>  1024^3 = 2^{30} (Gibi)
      ‘Ti’  =>  1024^4 = 2^{40} (Tebi)
      ‘Pi’  =>  1024^5 = 2^{50} (Pebi)
      ‘Ei’  =>  1024^6 = 2^{60} (Exbi)
      ‘Zi’  =>  1024^7 = 2^{70} (Zebi)
      ‘Yi’  =>  1024^8 = 2^{80} (Yobi)

 The ‘iec-i’ option uses a two-letter suffix symbol (e.g.  ‘Gi’), as
 the _iec_ standard recommends, but this is not always common in
 practice.  Compare with the ‘iec’ option.
```

AUTO ‘auto’ can only be used with ‘--from’. With this method, numbers
with ‘K’,‘M’,‘G’,‘T’,‘P’,‘E’,‘Z’,‘Y’ suffixes are interpreted as *SI*
values, and numbers with ‘Ki’, ‘Mi’,‘Gi’,‘Ti’,‘Pi’,‘Ei’,‘Zi’,‘Yi’
suffixes are interpreted as *IEC* values.

## Examples of using ‘numfmt’

Converting a single number from/to *human* representation: $ numfmt
--to=si 500000 500K

``` 
 $ numfmt --to=iec 500000
 489K

 $ numfmt --to=iec-i 500000
 489Ki

 $ numfmt --from=si 1M
 1000000

 $ numfmt --from=iec 1M
 1048576

 # with '--from=auto', M=Mega, Mi=Mebi
 $ numfmt --from=auto 1M
 1000000
 $ numfmt --from=auto 1Mi
 1048576
```

Converting from ‘SI’ to ‘IEC’ scales (e.g. when a harddisk capacity is
advertised as ‘1TB’, while checking the drive’s capacity gives lower
values):

``` 
 $ numfmt --from=si --to=iec 1T
 932G
```

Converting a single field from an input file / piped input (these
contrived examples are for demonstration purposes only, as both ‘ls’ and
‘df’ support the ‘--human-readable’ option to output sizes in
human-readable format):

``` 
 # Third field (file size) will be shown in SI representation
 $ ls -log | numfmt --field 3 --header --to=si | head -n4
 -rw-r--r--  1     94K Aug 23  2011 ABOUT-NLS
 -rw-r--r--  1    3.7K Jan  7 16:15 AUTHORS
 -rw-r--r--  1     36K Jun  1  2011 COPYING
 -rw-r--r--  1       0 Jan  7 15:15 ChangeLog

 # Second field (size) will be shown in IEC representation
 $ df --block-size=1 | numfmt --field 2 --header --to=iec | head -n4
 File system   1B-blocks        Used  Available Use% Mounted on
 rootfs             132G   104741408   26554036  80% /
 tmpfs              794M        7580     804960   1% /run/shm
 /dev/sdb1          694G   651424756   46074696  94% /home
```

Output can be tweaked using ‘--padding’ or ‘--format’:

``` 
 # Pad to 10 characters, right-aligned
 $ du -s * | numfmt --to=si --padding=10
       2.5K config.log
        108 config.status
       1.7K configure
         20 configure.ac

 # Pad to 10 characters, left-aligned
 $ du -s * | numfmt --to=si --padding=-10
 2.5K       config.log
 108        config.status
 1.7K       configure
 20         configure.ac

 # Pad to 10 characters, left-aligned, using 'format'
 $ du -s * | numfmt --to=si --format="%10f"
       2.5K config.log
        108 config.status
       1.7K configure
         20 configure.ac

 # Pad to 10 characters, left-aligned, using 'format'
 $ du -s * | numfmt --to=si --padding="%-10f"
 2.5K       config.log
 108        config.status
 1.7K       configure
 20         configure.ac
```

With locales that support grouping digits, using ‘--grouping’ or
‘--format’ enables grouping. In ‘POSIX’ locale, grouping is silently
ignored:

``` 
 $ LC_ALL=C numfmt --from=iec --grouping 2G
 2147483648

 $ LC_ALL=en_US.utf8 numfmt --from=iec --grouping 2G
 2,147,483,648

 $ LC_ALL=ta_IN numfmt --from=iec --grouping 2G
 2,14,74,83,648

 $ LC_ALL=C ./src/numfmt --from=iec --format="==%'15f==" 2G
 ==     2147483648==

 $ LC_ALL=en_US.utf8 ./src/numfmt --from=iec --format="==%'15f==" 2G
 ==  2,147,483,648==

 $ LC_ALL=en_US.utf8 ./src/numfmt --from=iec --format="==%'-15f==" 2G
 ==2,147,483,648  ==

 $ LC_ALL=ta_IN ./src/numfmt --from=iec --format="==%'15f==" 2G
 == 2,14,74,83,648==
```
