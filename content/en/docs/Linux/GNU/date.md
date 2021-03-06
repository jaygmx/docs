---
title:  "date"
linkTitle::  "date"
weight: 100
description: >-
     date
---

# ‘date’: Print or set system date and time

Synopses:

``` 
 date [OPTION]... [+FORMAT]
 date [-u|--utc|--universal] [ MMDDhhmm[[CC]YY][.ss] ]
```

Invoking ‘date’ with no FORMAT argument is equivalent to invoking it
with a default format that depends on the ‘LC\_TIME’ locale category. In
the default C locale, this format is ‘'+%a %b %e %H:%M:%S %Z %Y'’, so
the output looks like ‘Thu Mar 3 13:47:51 PST 2005’.

Normally, ‘date’ uses the time zone rules indicated by the ‘TZ’
environment variable, or the system default rules if ‘TZ’ is not set.
\*Note Specifying the Time Zone with ‘TZ’: (libc)TZ Variable.

If given an argument that starts with a ‘+’, ‘date’ prints the current
date and time (or the date and time specified by the ‘--date’ option,
see below) in the format defined by that argument, which is similar to
that of the ‘strftime’ function. Except for conversion specifiers, which
start with ‘%’, characters in the format string are printed unchanged.
The conversion specifiers are described below.

An exit status of zero indicates success, and a nonzero value indicates
failure.

  - Menu:

  - Time conversion specifiers:: %\[HIklMNpPrRsSTXzZ\]

  - Date conversion specifiers:: %\[aAbBcCdDeFgGhjmuUVwWxyY\]

  - Literal conversion specifiers:: %\[%nt\]

  - Padding and other flags:: Pad with zeros, spaces, etc.

  - Setting the time:: Changing the system clock.

  - Options for date:: Instead of the current time.

  - Date input formats:: Specifying date strings.

  - Examples of date:: Examples.

## Time conversion specifiers

‘date’ conversion specifiers related to times.

‘%H’ hour (‘00’...‘23’) ‘%I’ hour (‘01’...‘12’) ‘%k’ hour, space padded
(‘ 0’...‘23’); equivalent to ‘%\_H’. This is a GNU extension. ‘%l’ hour,
space padded (‘ 1’...‘12’); equivalent to ‘%\_I’. This is a GNU
extension. ‘%M’ minute (‘00’...‘59’) ‘%N’ nanoseconds
(‘000000000’...‘999999999’). This is a GNU extension. ‘%p’
locale’s equivalent of either ‘AM’ or ‘PM’; blank in many locales.
Noon is treated as ‘PM’ and midnight as ‘AM’. ‘%P’ like ‘%p’, except
lower case. This is a GNU extension. ‘%r’ locale’s 12-hour clock time
(e.g., ‘11:11:04 PM’) ‘%R’ 24-hour hour and minute. Same as ‘%H:%M’.
‘%s’ seconds since the epoch, i.e., since 1970-01-01 00:00:00 UTC.
Leap seconds are not counted unless leap second support is available.
\*Note %s-examples::, for examples. This is a GNU extension. ‘%S’ second
(‘00’...‘60’). This may be ‘60’ if leap seconds are supported. ‘%T’
24-hour hour, minute, and second. Same as ‘%H:%M:%S’. ‘%X’ locale’s time
representation (e.g., ‘23:13:48’) ‘%z’ Four-digit numeric time zone,
e.g., ‘-0600’ or ‘+0530’, or ‘-0000’ if no time zone is determinable.
This value reflects the numeric time zone appropriate for the current
time, using the time zone rules specified by the ‘TZ’ environment
variable. A time zone is not determinable if its numeric offset is zero
and its abbreviation begins with ‘-’. The time (and optionally, the time
zone rules) can be overridden by the ‘--date’ option. ‘%:z’ Numeric time
zone with ‘:’, e.g., ‘-06:00’ or ‘+05:30’), or ‘-00:00’ if no time zone
is determinable. This is a GNU extension. ‘%::z’ Numeric time zone to
the nearest second with ‘:’ (e.g., ‘-06:00:00’ or ‘+05:30:00’), or
‘-00:00:00’ if no time zone is determinable. This is a GNU extension.
‘%:::z’ Numeric time zone with ‘:’ using the minimum necessary
precision (e.g., ‘-06’, ‘+05:30’, or ‘-04:56:02’), or ‘-00’ if no time
zone is determinable. This is a GNU extension. ‘%Z’ alphabetic time zone
abbreviation (e.g., ‘EDT’), or nothing if no time zone is determinable.
See ‘%z’ for how it is determined.

## Date conversion specifiers

‘date’ conversion specifiers related to dates.

‘%a’ locale’s abbreviated weekday name (e.g., ‘Sun’) ‘%A’ locale’s full
weekday name, variable length (e.g., ‘Sunday’) ‘%b’ locale’s abbreviated
month name (e.g., ‘Jan’) ‘%B’ locale’s full month name, variable length
(e.g., ‘January’) ‘%c’ locale’s date and time (e.g., ‘Thu Mar 3 23:05:25
2005’) ‘%C’ century. This is like ‘%Y’, except the last two digits are
omitted. For example, it is ‘20’ if ‘%Y’ is ‘2000’, and is ‘-0’ if ‘%Y’
is ‘-001’. It is normally at least two characters, but it may be more.
‘%d’ day of month (e.g., ‘01’) ‘%D’ date; same as ‘%m/%d/%y’ ‘%e’ day
of month, space padded; same as ‘%\_d’ ‘%F’ full date in ISO 8601
format; same as ‘%Y-%m-%d’. This is a good choice for a date format, as
it is standard and is easy to sort in the usual case where years are in
the range 0000...9999. ‘%g’ year corresponding to the ISO week number,
but without the century (range ‘00’ through ‘99’). This has the same
format and value as ‘%y’, except that if the ISO week number (see ‘%V’)
belongs to the previous or next year, that year is used instead. ‘%G’
year corresponding to the ISO week number. This has the same format and
value as ‘%Y’, except that if the ISO week number (see ‘%V’) belongs to
the previous or next year, that year is used instead. It is normally
useful only if ‘%V’ is also used; for example, the format ‘%G-%m-%d’ is
probably a mistake, since it combines the ISO week number year with the
conventional month and day. ‘%h’ same as ‘%b’ ‘%j’ day of year
(‘001’...‘366’) ‘%m’ month (‘01’...‘12’) ‘%q’ quarter of year
(‘1’...‘4’) ‘%u’ day of week (‘1’...‘7’) with ‘1’ corresponding to
Monday ‘%U’ week number of year, with Sunday as the first day of the
week (‘00’...‘53’). Days in a new year preceding the first Sunday are in
week zero. ‘%V’ ISO week number, that is, the week number of year, with
Monday as the first day of the week (‘01’...‘53’). If the week
containing January 1 has four or more days in the new year, then it is
considered week 1; otherwise, it is week 53 of the previous year, and
the next week is week 1. (See the ISO 8601 standard.) ‘%w’ day of week
(‘0’...‘6’) with 0 corresponding to Sunday ‘%W’ week number of year,
with Monday as first day of week (‘00’...‘53’). Days in a new year
preceding the first Monday are in week zero. ‘%x’ locale’s date
representation (e.g., ‘12/31/99’) ‘%y’ last two digits of year
(‘00’...‘99’) ‘%Y’ year. This is normally at least four
characters, but it may be more. Year ‘0000’ precedes year ‘0001’, and
year ‘-001’ precedes year ‘0000’.

## Literal conversion specifiers

‘date’ conversion specifiers that produce literal strings.

‘%%’ a literal % ‘%n’ a newline ‘%t’ a horizontal tab

## Padding and other flags

Unless otherwise specified, ‘date’ normally pads numeric fields with
zeros, so that, for example, numeric months are always output as two
digits. Seconds since the epoch are not padded, though, since there is
no natural width for them.

As a GNU extension, ‘date’ recognizes any of the following optional
flags after the ‘%’:

‘-’ (hyphen) Do not pad the field; useful if the output is intended for
human consumption. ‘\_’ (underscore) Pad with spaces; useful if you need
a fixed number of characters in the output, but zeros are too
distracting. ‘0’ (zero) Pad with zeros even if the conversion specifier
would normally pad with spaces. ‘^’ Use upper case characters if
possible. ‘\#’ Use opposite case characters if possible. A field that is
normally upper case becomes lower case, and vice versa.

Here are some examples of padding:

``` 
 date +%d/%m -d "Feb 1"
 ⇒ 01/02
 date +%-d/%-m -d "Feb 1"
 ⇒ 1/2
 date +%_d/%_m -d "Feb 1"
 ⇒  1/ 2
```

As a GNU extension, you can specify the field width (after any flag, if
present) as a decimal number. If the natural size of the output of the
field has less than the specified number of characters, the result is
written right adjusted and padded to the given size. For example, ‘%9B’
prints the right adjusted month name in a field of width 9.

An optional modifier can follow the optional flag and width
specification. The modifiers are:

‘E’ Use the locale’s alternate representation for date and time. This
modifier applies to the ‘%c’, ‘%C’, ‘%x’, ‘%X’, ‘%y’ and ‘%Y’ conversion
specifiers. In a Japanese locale, for example, ‘%Ex’ might yield a date
format based on the Japanese Emperors’ reigns.

‘O’ Use the locale’s alternate numeric symbols for numbers. This
modifier applies only to numeric conversion specifiers.

If the format supports the modifier but no alternate representation is
available, it is ignored.

## Setting the time

If given an argument that does not start with ‘+’, ‘date’ sets the
system clock to the date and time specified by that argument (as
described below). You must have appropriate privileges to set the system
clock. Note for changes to persist across a reboot, the hardware clock
may need to be updated from the system clock, which might not happen
automatically on your system.

The argument must consist entirely of digits, which have the following
meaning:

‘MM’ month ‘DD’ day within month ‘hh’ hour ‘mm’ minute ‘CC’ first two
digits of year (optional) ‘YY’ last two digits of year (optional) ‘ss’
second (optional)

Note, the ‘--date’ and ‘--set’ options may not be used with an argument
in the above format. The ‘--universal’ option may be used with such an
argument to indicate that the specified date and time are relative to
Universal Time rather than to the local time zone.

## Options for ‘date’

The program accepts the following options. Also see \*note Common
options::.

‘-d DATESTR’ ‘--date=DATESTR’ Display the date and time specified in
DATESTR instead of the current date and time. DATESTR can be in almost
any common format. It can contain month names, time zones, ‘am’ and
‘pm’, ‘yesterday’, etc. For example, ‘--date="2004-02-27
14:19:13.489392193 +0530"’ specifies the instant of time that is
489,392,193 nanoseconds after February 27, 2004 at 2:19:13 PM in a time
zone that is 5 hours and 30 minutes east of UTC. Note: input currently
must be in locale independent format. E.g., the LC\_TIME=C below is
needed to print back the correct date in many locales: date -d
"$(LC\_TIME=C date)" \*Note Date input formats::.

‘--debug’ Annotate the parsed date, display the effective time zone, and
warn about potential misuse.

‘-f DATEFILE’ ‘--file=DATEFILE’ Parse each line in DATEFILE as with ‘-d’
and display the resulting date and time. If DATEFILE is ‘-’, use
standard input. This is useful when you have many dates to process,
because the system overhead of starting up the ‘date’ executable many
times can be considerable.

‘-I\[TIMESPEC\]’ ‘--iso-8601\[=TIMESPEC\]’ Display the date using an ISO
8601 format, ‘%Y-%m-%d’.

``` 
 The argument TIMESPEC specifies the number of additional terms of
 the time to include.  It can be one of the following:
 ‘auto’
      Print just the date.  This is the default if TIMESPEC is
      omitted.

 ‘hours’
      Append the hour of the day to the date.

 ‘minutes’
      Append the hours and minutes.

 ‘seconds’
      Append the hours, minutes and seconds.

 ‘ns’
      Append the hours, minutes, seconds and nanoseconds.

 If showing any time terms, then include the time zone using the
 format ‘%:z’.  This format is always suitable as input for the
 ‘--date’ (‘-d’) and ‘--file’ (‘-f’) options, regardless of the
 current locale.
```

‘-r FILE’ ‘--reference=FILE’ Display the date and time of the last
modification of FILE, instead of the current date and time.

‘-R’ ‘--rfc-email’ Display the date and time using the format ‘%a, %d %b
%Y %H:%M:%S %z’, evaluated in the C locale so abbreviations are always
in English. For example:

``` 
      Fri, 09 Sep 2005 13:51:39 -0700

 This format conforms to Internet RFCs 5322
 (https://tools.ietf.org/search/rfc5322), 822
 (https://tools.ietf.org/search/rfc2822) and 822
 (https://tools.ietf.org/search/rfc822), the current and previous
 standards for Internet email.  For compatibility with older
 versions of ‘date’, ‘--rfc-2822’ and ‘--rfc-822’ are aliases for
 ‘--rfc-email’.
```

‘--rfc-3339=TIMESPEC’ Display the date using a format specified by
Internet RFC 3339 (https://tools.ietf.org/search/rfc3339). This is like
‘--iso-8601’, except that a space rather than a ‘T’ separates dates
from times. This format is always suitable as input for the ‘--date’
(‘-d’) and ‘--file’ (‘-f’) options, regardless of the current locale.

``` 
 The argument TIMESPEC specifies how much of the time to include.
 It can be one of the following:

 ‘date’
      Print just the full-date, e.g., ‘2005-09-14’.  This is
      equivalent to the format ‘%Y-%m-%d’.

 ‘seconds’
      Print the full-date and full-time separated by a space, e.g.,
      ‘2005-09-14 00:56:06+05:30’.  The output ends with a numeric
      time-offset; here the ‘+05:30’ means that local time is five
      hours and thirty minutes east of UTC.  This is equivalent to
      the format ‘%Y-%m-%d %H:%M:%S%:z’.

 ‘ns’
      Like ‘seconds’, but also print nanoseconds, e.g., ‘2005-09-14
      00:56:06.998458565+05:30’.  This is equivalent to the format
      ‘%Y-%m-%d %H:%M:%S.%N%:z’.
```

‘-s DATESTR’ ‘--set=DATESTR’ Set the date and time to DATESTR. See ‘-d’
above. See also \*note Setting the time::.

‘-u’ ‘--utc’ ‘--universal’ Use Universal Time by operating as if the
‘TZ’ environment variable were set to the string ‘UTC0’. UTC stands
for Coordinated Universal Time, established in 1960. Universal Time is
often called “Greenwich Mean Time” (GMT) for historical reasons.
Typically, systems ignore leap seconds and thus implement an
approximation to UTC rather than true UTC.

29 Date input formats

-----

First, a quote:

``` 
 Our units of temporal measurement, from seconds on up to months,
 are so complicated, asymmetrical and disjunctive so as to make
 coherent mental reckoning in time all but impossible.  Indeed, had
 some tyrannical god contrived to enslave our minds to time, to make
 it all but impossible for us to escape subjection to sodden
 routines and unpleasant surprises, he could hardly have done better
 than handing down our present system.  It is like a set of
 trapezoidal building blocks, with no vertical or horizontal
 surfaces, like a language in which the simplest thought demands
 ornate constructions, useless particles and lengthy
 circumlocutions.  Unlike the more successful patterns of language
 and science, which enable us to face experience boldly or at least
 level-headedly, our system of temporal calculation silently and
 persistently encourages our terror of time.

 ... It is as though architects had to measure length in feet, width
 in meters and height in ells; as though basic instruction manuals
 demanded a knowledge of five different languages.  It is no wonder
 then that we often look into our own immediate past or future, last
 Tuesday or a week from Sunday, with feelings of helpless confusion.
 ...

 —Robert Grudin, ‘Time and the Art of Living’.
```

This section describes the textual date representations that GNU
programs accept. These are the strings you, as a user, can supply as
arguments to the various programs. The C interface (via the
‘parse\_datetime’ function) is not described here.

  - Menu:

  - General date syntax:: Common rules.

  - Calendar date items:: 19 Dec 1994.

  - Time of day items:: 9:20pm.

  - Time zone items:: EST, PDT, UTC, ...

  - Combined date and time of day items::
    1972-09-24T20:02:00,000000-0500.

  - Day of week items:: Monday and others.

  - Relative items in date strings:: next tuesday, 2 years ago.

  - Pure numbers in date strings:: 19931219, 1440.

  - Seconds since the Epoch:: @1078100502.

  - Specifying time zone rules:: TZ="America/New\_York", TZ="UTC0".

  - Authors of parse\_datetime:: Bellovin, Eggert, Salz, Berets, et al.

# General date syntax

A “date” is a string, possibly empty, containing many items separated by
whitespace. The whitespace may be omitted when no ambiguity arises. The
empty string means the beginning of today (i.e., midnight). Order of the
items is immaterial. A date string may contain many flavors of items:

• calendar date items • time of day items • time zone items • combined
date and time of day items • day of the week items • relative items •
pure numbers.

We describe each of these item types in turn, below.

A few ordinal numbers may be written out in words in some contexts. This
is most useful for specifying day of the week items or relative items
(see below). Among the most commonly used ordinal numbers, the word
‘last’ stands for -1, ‘this’ stands for 0, and ‘first’ and ‘next’ both
stand for 1. Because the word ‘second’ stands for the unit of time there
is no way to write the ordinal number 2, but for convenience ‘third’
stands for 3, ‘fourth’ for 4, ‘fifth’ for 5, ‘sixth’ for 6, ‘seventh’
for 7, ‘eighth’ for 8, ‘ninth’ for 9, ‘tenth’ for 10, ‘eleventh’ for 11
and ‘twelfth’ for 12.

When a month is written this way, it is still considered to be written
numerically, instead of being “spelled in full”; this changes the
allowed strings.

In the current implementation, only English is supported for words and
abbreviations like ‘AM’, ‘DST’, ‘EST’, ‘first’, ‘January’, ‘Sunday’,
‘tomorrow’, and ‘year’.

The output of the ‘date’ command is not always acceptable as a date
string, not only because of the language problem, but also because there
is no standard meaning for time zone items like ‘IST’. When using ‘date’
to generate a date string intended to be parsed later, specify a date
format that is independent of language and that does not use time zone
items other than ‘UTC’ and ‘Z’. Here are some ways to do this:

``` 
 $ LC_ALL=C TZ=UTC0 date
 Mon Mar  1 00:21:42 UTC 2004
 $ TZ=UTC0 date +'%Y-%m-%d %H:%M:%SZ'
 2004-03-01 00:21:42Z
 $ date --rfc-3339=ns  # --rfc-3339 is a GNU extension.
 2004-02-29 16:21:42.692722128-08:00
 $ date --rfc-2822  # a GNU extension
 Sun, 29 Feb 2004 16:21:42 -0800
 $ date +'%Y-%m-%d %H:%M:%S %z'  # %z is a GNU extension.
 2004-02-29 16:21:42 -0800
 $ date +'@%s.%N'  # %s and %N are GNU extensions.
 @1078100502.692722128
```

Alphabetic case is completely ignored in dates. Comments may be
introduced between round parentheses, as long as included parentheses
are properly nested. Hyphens not followed by a digit are currently
ignored. Leading zeros on numbers are ignored.

Invalid dates like ‘2005-02-29’ or times like ‘24:00’ are rejected. In
the typical case of a host that does not support leap seconds, a time
like ‘23:59:60’ is rejected even if it corresponds to a valid leap
second.

# Calendar date items

A “calendar date item” specifies a day of the year. It is specified
differently, depending on whether the month is specified numerically or
literally. All these strings specify the same calendar date:

``` 
 1972-09-24     # ISO 8601.
 72-9-24        # Assume 19xx for 69 through 99,
                # 20xx for 00 through 68.
 72-09-24       # Leading zeros are ignored.
 9/24/72        # Common U.S. writing.
 24 September 1972
 24 Sept 72     # September has a special abbreviation.
 24 Sep 72      # Three-letter abbreviations always allowed.
 Sep 24, 1972
 24-sep-72
 24sep72
```

The year can also be omitted. In this case, the last specified year is
used, or the current year if none. For example:

``` 
 9/24
 sep 24
```

Here are the rules.

For numeric months, the ISO 8601 format ‘YEAR-MONTH-DAY’ is allowed,
where YEAR is any positive number, MONTH is a number between 01 and 12,
and DAY is a number between 01 and 31. A leading zero must be present if
a number is less than ten. If YEAR is 68 or smaller, then 2000 is added
to it; otherwise, if YEAR is less than 100, then 1900 is added to it.
The construct ‘MONTH/DAY/YEAR’, popular in the United States, is
accepted. Also ‘MONTH/DAY’, omitting the year.

Literal months may be spelled out in full: ‘January’, ‘February’,
‘March’, ‘April’, ‘May’, ‘June’, ‘July’, ‘August’, ‘September’,
‘October’, ‘November’ or ‘December’. Literal months may be abbreviated
to their first three letters, possibly followed by an abbreviating dot.
It is also permitted to write ‘Sept’ instead of ‘September’.

When months are written literally, the calendar date may be given as any
of the following:

``` 
 DAY MONTH YEAR
 DAY MONTH
 MONTH DAY YEAR
 DAY-MONTH-YEAR
```

Or, omitting the year:

``` 
 MONTH DAY
```

# Time of day items

A “time of day item” in date strings specifies the time on a given day.
Here are some examples, all of which represent the same time:

``` 
 20:02:00.000000
 20:02
 8:02pm
 20:02-0500      # In EST (U.S. Eastern Standard Time).
```

More generally, the time of day may be given as ‘HOUR:MINUTE:SECOND’,
where HOUR is a number between 0 and 23, MINUTE is a number between 0
and 59, and SECOND is a number between 0 and 59 possibly followed by ‘.’
or ‘,’ and a fraction containing one or more digits. Alternatively,
‘:SECOND’ can be omitted, in which case it is taken to be zero. On the
rare hosts that support leap seconds, SECOND may be 60.

If the time is followed by ‘am’ or ‘pm’ (or ‘a.m.’ or ‘p.m.’), HOUR is
restricted to run from 1 to 12, and ‘:MINUTE’ may be omitted (taken to
be zero). ‘am’ indicates the first half of the day, ‘pm’ indicates the
second half of the day. In this notation, 12 is the predecessor of 1:
midnight is ‘12am’ while noon is ‘12pm’. (This is the zero-oriented
interpretation of ‘12am’ and ‘12pm’, as opposed to the old tradition
derived from Latin which uses ‘12m’ for noon and ‘12pm’ for midnight.)

The time may alternatively be followed by a time zone correction,
expressed as ‘SHHMM’, where S is ‘+’ or ‘-’, HH is a number of zone
hours and MM is a number of zone minutes. The zone minutes term, MM, may
be omitted, in which case the one- or two-digit correction is
interpreted as a number of hours. You can also separate HH from MM with
a colon. When a time zone correction is given this way, it forces
interpretation of the time relative to Coordinated Universal Time (UTC),
overriding any previous specification for the time zone or the local
time zone. For example, ‘+0530’ and ‘+05:30’ both stand for the time
zone 5.5 hours ahead of UTC (e.g., India). This is the best way to
specify a time zone correction by fractional parts of an hour. The
maximum zone correction is 24 hours.

Either ‘am’/‘pm’ or a time zone correction may be specified, but not
both.

# Time zone items

A “time zone item” specifies an international time zone, indicated by a
small set of letters, e.g., ‘UTC’ or ‘Z’ for Coordinated Universal Time.
Any included periods are ignored. By following a non-daylight-saving
time zone by the string ‘DST’ in a separate word (that is, separated by
some white space), the corresponding daylight saving time zone may be
specified. Alternatively, a non-daylight-saving time zone can be
followed by a time zone correction, to add the two values. This is
normally done only for ‘UTC’; for example, ‘UTC+05:30’ is equivalent to
‘+05:30’.

Time zone items other than ‘UTC’ and ‘Z’ are obsolescent and are not
recommended, because they are ambiguous; for example, ‘EST’ has a
different meaning in Australia than in the United States. Instead, it’s
better to use unambiguous numeric time zone corrections like ‘-0500’, as
described in the previous section.

If neither a time zone item nor a time zone correction is supplied,
timestamps are interpreted using the rules of the default time zone
(\*note Specifying time zone rules::).

# Combined date and time of day items

The ISO 8601 date and time of day extended format consists of an ISO
8601 date, a ‘T’ character separator, and an ISO 8601 time of day. This
format is also recognized if the ‘T’ is replaced by a space.

In this format, the time of day should use 24-hour notation. Fractional
seconds are allowed, with either comma or period preceding the fraction.
ISO 8601 fractional minutes and hours are not supported. Typically,
hosts support nanosecond timestamp resolution; excess precision is
silently discarded.

Here are some examples:

``` 
 2012-09-24T20:02:00.052-05:00
 2012-12-31T23:59:59,999999999+11:00
 1970-01-01 00:00Z
```

# Day of week items

The explicit mention of a day of the week will forward the date (only if
necessary) to reach that day of the week in the future.

Days of the week may be spelled out in full: ‘Sunday’, ‘Monday’,
‘Tuesday’, ‘Wednesday’, ‘Thursday’, ‘Friday’ or ‘Saturday’. Days may
be abbreviated to their first three letters, optionally followed by a
period. The special abbreviations ‘Tues’ for ‘Tuesday’, ‘Wednes’ for
‘Wednesday’ and ‘Thur’ or ‘Thurs’ for ‘Thursday’ are also allowed.

A number may precede a day of the week item to move forward
supplementary weeks. It is best used in expression like ‘third monday’.
In this context, ‘last DAY’ or ‘next DAY’ is also acceptable; they move
one week before or after the day that DAY by itself would represent.

A comma following a day of the week item is ignored.

# Relative items in date strings

“Relative items” adjust a date (or the current date if none) forward or
backward. The effects of relative items accumulate. Here are some
examples:

``` 
 1 year
 1 year ago
 3 years
 2 days
```

The unit of time displacement may be selected by the string ‘year’ or
‘month’ for moving by whole years or months. These are fuzzy units, as
years and months are not all of equal duration. More precise units are
‘fortnight’ which is worth 14 days, ‘week’ worth 7 days, ‘day’ worth
24 hours, ‘hour’ worth 60 minutes, ‘minute’ or ‘min’ worth 60 seconds,
and ‘second’ or ‘sec’ worth one second. An ‘s’ suffix on these units is
accepted and ignored.

The unit of time may be preceded by a multiplier, given as an optionally
signed number. Unsigned numbers are taken as positively signed. No
number at all implies 1 for a multiplier. Following a relative item by
the string ‘ago’ is equivalent to preceding the unit by a multiplier
with value -1.

The string ‘tomorrow’ is worth one day in the future (equivalent to
‘day’), the string ‘yesterday’ is worth one day in the past
(equivalent to ‘day ago’).

The strings ‘now’ or ‘today’ are relative items corresponding to
zero-valued time displacement, these strings come from the fact a
zero-valued time displacement represents the current time when not
otherwise changed by previous items. They may be used to stress other
items, like in ‘12:00 today’. The string ‘this’ also has the meaning of
a zero-valued time displacement, but is preferred in date strings like
‘this thursday’.

When a relative item causes the resulting date to cross a boundary where
the clocks were adjusted, typically for daylight saving time, the
resulting date and time are adjusted accordingly.

The fuzz in units can cause problems with relative items. For example,
‘2003-07-31 -1 month’ might evaluate to 2003-07-01, because 2003-06-31
is an invalid date. To determine the previous month more reliably, you
can ask for the month before the 15th of the current month. For example:

``` 
 $ date -R
 Thu, 31 Jul 2003 13:02:39 -0700
 $ date --date='-1 month' +'Last month was %B?'
 Last month was July?
 $ date --date="$(date +%Y-%m-15) -1 month" +'Last month was %B!'
 Last month was June!
```

Also, take care when manipulating dates around clock changes such as
daylight saving leaps. In a few cases these have added or subtracted as
much as 24 hours from the clock, so it is often wise to adopt universal
time by setting the ‘TZ’ environment variable to ‘UTC0’ before embarking
on calendrical calculations.

# Pure numbers in date strings

The precise interpretation of a pure decimal number depends on the
context in the date string.

If the decimal number is of the form YYYYMMDD and no other calendar date
item (\*note Calendar date items::) appears before it in the date
string, then YYYY is read as the year, MM as the month number and DD as
the day of the month, for the specified calendar date.

If the decimal number is of the form HHMM and no other time of day item
appears before it in the date string, then HH is read as the hour of the
day and MM as the minute of the hour, for the specified time of day. MM
can also be omitted.

If both a calendar date and a time of day appear to the left of a number
in the date string, but no relative item, then the number overrides the
year.

# Seconds since the Epoch

If you precede a number with ‘@’, it represents an internal timestamp as
a count of seconds. The number can contain an internal decimal point
(either ‘.’ or ‘,’); any excess precision not supported by the internal
representation is truncated toward minus infinity. Such a number cannot
be combined with any other date item, as it specifies a complete
timestamp.

Internally, computer times are represented as a count of seconds since
an epoch—a well-defined point of time. On GNU and POSIX systems, the
epoch is 1970-01-01 00:00:00 UTC, so ‘@0’ represents this time, ‘@1’
represents 1970-01-01 00:00:01 UTC, and so forth. GNU and most other
POSIX-compliant systems support such times as an extension to POSIX,
using negative counts, so that ‘@-1’ represents 1969-12-31 23:59:59 UTC.

Traditional Unix systems count seconds with 32-bit two’s-complement
integers and can represent times from 1901-12-13 20:45:52 through
2038-01-19 03:14:07 UTC. More modern systems use 64-bit counts of
seconds with nanosecond subcounts, and can represent all the times in
the known lifetime of the universe to a resolution of 1 nanosecond.

On most hosts, these counts ignore the presence of leap seconds. For
example, on most hosts ‘@915148799’ represents 1998-12-31 23:59:59 UTC,
‘@915148800’ represents 1999-01-01 00:00:00 UTC, and there is no way
to represent the intervening leap second 1998-12-31 23:59:60 UTC.

# Specifying time zone rules

Normally, dates are interpreted using the rules of the current time
zone, which in turn are specified by the ‘TZ’ environment variable, or
by a system default if ‘TZ’ is not set. To specify a different set of
default time zone rules that apply just to one date, start the date with
a string of the form ‘TZ="RULE"’. The two quote characters (‘"’) must be
present in the date, and any quotes or backslashes within RULE must be
escaped by a backslash.

For example, with the GNU ‘date’ command you can answer the question
“What time is it in New York when a Paris clock shows 6:30am on
October 31, 2004?” by using a date beginning with ‘TZ="Europe/Paris"’ as
shown in the following shell transcript:

``` 
 $ export TZ="America/New_York"
 $ date --date='TZ="Europe/Paris" 2004-10-31 06:30'
 Sun Oct 31 01:30:00 EDT 2004
```

In this example, the ‘--date’ operand begins with its own ‘TZ’ setting,
so the rest of that operand is processed according to ‘Europe/Paris’
rules, treating the string ‘2004-10-31 06:30’ as if it were in Paris.
However, since the output of the ‘date’ command is processed according
to the overall time zone rules, it uses New York time. (Paris was
normally six hours ahead of New York in 2004, but this example refers to
a brief Halloween period when the gap was five hours.)

A ‘TZ’ value is a rule that typically names a location in the ‘tz’
database (http://www.twinsun.com/tz/tz-link.htm). A recent catalog of
location names appears in the TWiki Date and Time Gateway
(http://twiki.org/cgi-bin/xtra/tzdate). A few non-GNU hosts require a
colon before a location name in a ‘TZ’ setting, e.g.,
‘TZ=":America/New\_York"’.

The ‘tz’ database includes a wide variety of locations ranging from
‘Arctic/Longyearbyen’ to ‘Antarctica/South\_Pole’, but if you are at
sea and have your own private time zone, or if you are using a non-GNU
host that does not support the ‘tz’ database, you may need to use a
POSIX rule instead. Simple POSIX rules like ‘UTC0’ specify a time zone
without daylight saving time; other rules can specify simple daylight
saving regimes. \*Note Specifying the Time Zone with ‘TZ’: (libc)TZ
Variable.

# Authors of ‘parse\_datetime’

‘parse\_datetime’ started life as ‘getdate’, as originally implemented
by Steven M. Bellovin (<smb@research.att.com>) while at the University
of North Carolina at Chapel Hill. The code was later tweaked by a couple
of people on Usenet, then completely overhauled by Rich $alz
(<rsalz@bbn.com>) and Jim Berets (<jberets@bbn.com>) in August, 1990.
Various revisions for the GNU system were made by David MacKenzie, Jim
Meyering, Paul Eggert and others, including renaming it to ‘get\_date’
to avoid a conflict with the alternative Posix function ‘getdate’, and a
later rename to ‘parse\_datetime’. The Posix function ‘getdate’ can
parse more locale-specific dates using ‘strptime’, but relies on an
environment variable and external file, and lacks the thread-safety of
‘parse\_datetime’.

This chapter was originally produced by François Pinard
(<pinard@iro.umontreal.ca>) from the ‘parse\_datetime.y’ source code,
and then edited by K. Berry (<kb@cs.umb.edu>).

## Examples of ‘date’

Here are a few examples. Also see the documentation for the ‘-d’ option
in the previous section.

• To print the date of the day before yesterday:

``` 
      date --date='2 days ago'
```

• To print the date of the day three months and one day hence:

``` 
      date --date='3 months 1 day'
```

• To print the day of year of Christmas in the current year:

``` 
      date --date='25 Dec' +%j
```

• To print the current full month name and the day of the month:

``` 
      date '+%B %d'

 But this may not be what you want because for the first nine days
 of the month, the ‘%d’ expands to a zero-padded two-digit field,
 for example ‘date -d 1may '+%B %d'’ will print ‘May 01’.
```

• To print a date without the leading zero for one-digit days of the
month, you can use the (GNU extension) ‘-’ flag to suppress the padding
altogether:

``` 
      date -d 1may '+%B %-d'
```

• To print the current date and time in the format required by many
non-GNU versions of ‘date’ when setting the system clock:

``` 
      date +%m%d%H%M%Y.%S
```

• To set the system clock forward by two minutes:

``` 
      date --set='+2 minutes'
```

• To print the date in Internet RFC 5322 format, use ‘date --rfc-email’.
Here is some example output:

``` 
      Fri, 09 Sep 2005 13:51:39 -0700
```

• To convert a date string to the number of seconds since the epoch
(which is 1970-01-01 00:00:00 UTC), use the ‘--date’ option with the
‘%s’ format. That can be useful in sorting and/or graphing and/or
comparing data by date. The following command outputs the number of the
seconds since the epoch for the time two minutes after the epoch:

``` 
      date --date='1970-01-01 00:02:00 +0000' +%s
      120

 If you do not specify time zone information in the date string,
 ‘date’ uses your computer’s idea of the time zone when interpreting
 the string.  For example, if your computer’s time zone is that of
 Cambridge, Massachusetts, which was then 5 hours (i.e., 18,000
 seconds) behind UTC:

      # local time zone used
      date --date='1970-01-01 00:02:00' +%s
      18120
```

• If you’re sorting or graphing dated data, your raw date values may be
represented as seconds since the epoch. But few people can look at the
date ‘946684800’ and casually note “Oh, that’s the first second of the
year 2000 in Greenwich, England.”

``` 
      date --date='2000-01-01 UTC' +%s
      946684800

 An alternative is to use the ‘--utc’ (‘-u’) option.  Then you may
 omit ‘UTC’ from the date string.  Although this produces the same
 result for ‘%s’ and many other format sequences, with a time zone
 offset different from zero, it would give a different result for
 zone-dependent formats like ‘%z’.

      date -u --date=2000-01-01 +%s
      946684800

 To convert such an unwieldy number of seconds back to a more
 readable form, use a command like this:

      # local time zone used
      date -d '1970-01-01 UTC 946684800 seconds' +"%Y-%m-%d %T %z"
      1999-12-31 19:00:00 -0500

 Or if you do not mind depending on the ‘@’ feature present since
 coreutils 5.3.0, you could shorten this to:

      date -d @946684800 +"%F %T %z"
      1999-12-31 19:00:00 -0500

 Often it is better to output UTC-relative date and time:

      date -u -d '1970-01-01 946684800 seconds' +"%Y-%m-%d %T %z"
      2000-01-01 00:00:00 +0000
```

• Typically the seconds count omits leap seconds, but some systems are
exceptions. Because leap seconds are not predictable, the mapping
between the seconds count and a future timestamp is not reliable on the
atypical systems that include leap seconds in their counts.

``` 
 Here is how the two kinds of systems handle the leap second at
 2012-06-30 23:59:60 UTC:

      # Typical systems ignore leap seconds:
      date --date='2012-06-30 23:59:59 +0000' +%s
      1341100799
      date --date='2012-06-30 23:59:60 +0000' +%s
      date: invalid date '2012-06-30 23:59:60 +0000'
      date --date='2012-07-01 00:00:00 +0000' +%s
      1341100800

      # Atypical systems count leap seconds:
      date --date='2012-06-30 23:59:59 +0000' +%s
      1341100823
      date --date='2012-06-30 23:59:60 +0000' +%s
      1341100824
      date --date='2012-07-01 00:00:00 +0000' +%s
      1341100825
```
