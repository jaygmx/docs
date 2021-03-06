---
title:  "du"
linkTitle::  "du"
weight: 100
description: >-
     du
---

# ‘du’: Estimate file space usage

‘du’ reports the amount of disk space used by the set of specified files
and for each subdirectory (of directory arguments).
Synopsis:

``` 
 du [OPTION]... [FILE]...
```

With no arguments, ‘du’ reports the disk space for the current
directory. Normally the disk space is printed in units of 1024 bytes,
but this can be overridden (\*note Block size::). Non-integer quantities
are rounded up to the next higher unit.

If two or more hard links point to the same file, only one of the hard
links is counted. The FILE argument order affects which links are
counted, and changing the argument order may change the numbers and
entries that ‘du’ outputs.

The program accepts the following options. Also see \*note Common
options::.

‘-0’ ‘--null’ Output a zero byte (ASCII NUL) at the end of each line,
rather than a newline. This option enables other programs to parse the
output even when that output would contain data with embedded newlines.

‘-a’ ‘--all’ Show counts for all files, not just directories.

‘--apparent-size’ Print apparent sizes, rather than disk usage. The
apparent size of a file is the number of bytes reported by ‘wc -c’ on
regular files, or more generally, ‘ls -l --block-size=1’ or ‘stat
--format=%s’. For example, a file containing the word ‘zoo’ with no
newline would, of course, have an apparent size of 3. Such a small file
may require anywhere from 0 to 16 KiB or more of disk space, depending
on the type and configuration of the file system on which the file
resides. However, a sparse file created with this command:

``` 
      dd bs=1 seek=2GiB if=/dev/null of=big

 has an apparent size of 2 GiB, yet on most modern systems, it
 actually uses almost no disk space.
```

‘-B SIZE’ ‘--block-size=SIZE’ Scale sizes by SIZE before printing them
(\*note Block size::). For example, ‘-BG’ prints sizes in units of
1,073,741,824 bytes.

‘-b’ ‘--bytes’ Equivalent to ‘--apparent-size --block-size=1’.

‘-c’ ‘--total’ Print a grand total of all arguments after all arguments
have been processed. This can be used to find out the total disk usage
of a given set of files or directories.

‘-D’ ‘--dereference-args’ Dereference symbolic links that are command
line arguments. Does not affect other symbolic links. This is helpful
for finding out the disk usage of directories, such as ‘/usr/tmp’, which
are often symbolic links.

‘-d DEPTH’ ‘--max-depth=DEPTH’ Show the total for each directory (and
file if –all) that is at most MAX\_DEPTH levels down from the root of
the hierarchy. The root is at level 0, so ‘du --max-depth=0’ is
equivalent to ‘du -s’.

‘--files0-from=FILE’ Disallow processing files named on the command
line, and instead process those named in file FILE; each name being
terminated by a zero byte (ASCII NUL). This is useful when the list of
file names is so long that it may exceed a command line length
limitation. In such cases, running ‘du’ via ‘xargs’ is undesirable
because it splits the list into pieces and makes ‘du’ print with the
‘--total’ (‘-c’) option for each sublist rather than for the entire
list. One way to produce a list of ASCII NUL terminated file names is
with GNU ‘find’, using its ‘-print0’ predicate. If FILE is ‘-’ then the
ASCII NUL terminated file names are read from standard input.

‘-H’ Equivalent to ‘--dereference-args’ (‘-D’).

‘-h’ ‘--human-readable’ Append a size letter to each size, such as ‘M’
for mebibytes. Powers of 1024 are used, not 1000; ‘M’ stands for
1,048,576 bytes. This option is equivalent to
‘--block-size=human-readable’. Use the ‘--si’ option if you prefer
powers of 1000.

‘--inodes’ List inode usage information instead of block usage. This
option is useful for finding directories which contain many files, and
therefore eat up most of the inodes space of a file system (see ‘df’,
option ‘--inodes’). It can well be combined with the options ‘-a’, ‘-c’,
‘-h’, ‘-l’, ‘-s’, ‘-S’, ‘-t’ and ‘-x’; however, passing other options
regarding the block size, for example ‘-b’, ‘-m’ and ‘--apparent-size’,
is ignored.

‘-k’ Print sizes in 1024-byte blocks, overriding the default block size
(\*note Block size::). This option is equivalent to ‘--block-size=1K’.

‘-L’ ‘--dereference’ Dereference symbolic links (show the disk space
used by the file or directory that the link points to instead of the
space used by the link).

‘-l’ ‘--count-links’ Count the size of all files, even if they have
appeared already (as a hard link).

‘-m’ Print sizes in 1,048,576-byte blocks, overriding the default block
size (\*note Block size::). This option is equivalent to
‘--block-size=1M’.

‘-P’ ‘--no-dereference’ For each symbolic links encountered by ‘du’,
consider the disk space used by the symbolic link.

‘-S’ ‘--separate-dirs’ Normally, in the output of ‘du’ (when not using
‘--summarize’), the size listed next to a directory name, D,
represents the sum of sizes of all entries beneath D as well as the size
of D itself. With ‘--separate-dirs’, the size reported for a directory
name, D, will exclude the size of any subdirectories.

‘--si’ Append an SI-style abbreviation to each size, such as ‘M’ for
megabytes. Powers of 1000 are used, not 1024; ‘M’ stands for 1,000,000
bytes. This option is equivalent to ‘--block-size=si’. Use the ‘-h’ or
‘--human-readable’ option if you prefer powers of 1024.

‘-s’ ‘--summarize’ Display only a total for each argument.

‘-t SIZE’ ‘--threshold=SIZE’ Exclude entries based on a given SIZE. The
SIZE refers to used blocks in normal mode (\*note Block size::), or
inodes count in conjunction with the ‘--inodes’ option.

``` 
 If SIZE is positive, then ‘du’ will only print entries with a size
 greater than or equal to that.

 If SIZE is negative, then ‘du’ will only print entries with a size
 smaller than or equal to that.

 Although GNU ‘find’ can be used to find files of a certain size,
 ‘du’’s ‘--threshold’ option can be used to also filter directories
 based on a given size.

 Please note that the ‘--threshold’ option can be combined with the
 ‘--apparent-size’ option, and in this case would elide entries
 based on its apparent size.

 Please note that the ‘--threshold’ option can be combined with the
 ‘--inodes’ option, and in this case would elide entries based on
 its inodes count.

 Here’s how you would use ‘--threshold’ to find directories with a
 size greater than or equal to 200 megabytes:

      du --threshold=200MB

 Here’s how you would use ‘--threshold’ to find directories and
 files - note the ‘-a’ - with an apparent size smaller than or equal
 to 500 bytes:

      du -a -t -500 --apparent-size

 Here’s how you would use ‘--threshold’ to find directories on the
 root file system with more than 20000 inodes used in the directory
 tree below:

      du --inodes -x --threshold=20000 /
```

‘--time’ Show the most recent modification timestamp (mtime) of any file
in the directory, or any of its subdirectories. \*Note File
timestamps::.

‘--time=ctime’ ‘--time=status’ ‘--time=use’ Show the most recent status
change timestamp (ctime) of any file in the directory, or any of its
subdirectories. \*Note File timestamps::.

‘--time=atime’ ‘--time=access’ Show the most recent access timestamp
(atime) of any file in the directory, or any of its subdirectories.
\*Note File timestamps::.

‘--time-style=STYLE’ List timestamps in style STYLE. This option has an
effect only if the ‘--time’ option is also specified. The STYLE should
be one of the following:

``` 
 ‘+FORMAT’
      List timestamps using FORMAT, where FORMAT is interpreted like
      the format argument of ‘date’ (*note date invocation::).  For
      example, ‘--time-style="+%Y-%m-%d %H:%M:%S"’ causes ‘du’ to
      list timestamps like ‘2002-03-30 23:45:56’.  As with ‘date’,
      FORMAT’s interpretation is affected by the ‘LC_TIME’ locale
      category.

 ‘full-iso’
      List timestamps in full using ISO 8601-like date, time, and
      time zone components with nanosecond precision, e.g.,
      ‘2002-03-30 23:45:56.477817180 -0700’.  This style is
      equivalent to ‘+%Y-%m-%d %H:%M:%S.%N %z’.

 ‘long-iso’
      List ISO 8601 date and time components with minute precision,
      e.g., ‘2002-03-30 23:45’.  These timestamps are shorter than
      ‘full-iso’ timestamps, and are usually good enough for
      everyday work.  This style is equivalent to ‘+%Y-%m-%d %H:%M’.

 ‘iso’
      List ISO 8601 dates for timestamps, e.g., ‘2002-03-30’.  This
      style is equivalent to ‘+%Y-%m-%d’.

 You can specify the default value of the ‘--time-style’ option with
 the environment variable ‘TIME_STYLE’; if ‘TIME_STYLE’ is not set
 the default style is ‘long-iso’.  For compatibility with ‘ls’, if
 ‘TIME_STYLE’ begins with ‘+’ and contains a newline, the newline
 and any later characters are ignored; if ‘TIME_STYLE’ begins with
 ‘posix-’ the ‘posix-’ is ignored; and if ‘TIME_STYLE’ is ‘locale’
 it is ignored.
```

‘-X FILE’ ‘--exclude-from=FILE’ Like ‘--exclude’, except take the
patterns to exclude from FILE, one per line. If FILE is ‘-’, take the
patterns from standard input.

‘--exclude=PATTERN’ When recursing, skip subdirectories or files
matching PATTERN. For example, ‘du --exclude='\*.o'’ excludes files
whose names end in ‘.o’.

‘-x’ ‘--one-file-system’ Skip directories that are on different file
systems from the one that the argument being processed is on.

On BSD systems, ‘du’ reports sizes that are half the correct values for
files that are NFS-mounted from HP-UX systems. On HP-UX systems, it
reports sizes that are twice the correct values for files that are
NFS-mounted from BSD systems. This is due to a flaw in HP-UX; it also
affects the HP-UX ‘du’ program.

An exit status of zero indicates success, and a nonzero value indicates
failure.
