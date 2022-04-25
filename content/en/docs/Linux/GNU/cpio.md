---
title:  "cpio"
linkTitle::  "cpio"
weight: 100
description: >-
     GNU cpio
---

# GNU CPIO

### 2.13.90 6 January 2021

**by Robert Carleton and Sergey Poznyakoff**  

This manual documents GNU cpio (version 2.13.90, 6 January 2021).

Copyright © 1995, 2001–2002, 2004, 2010, 2014–2015, 2017, 2020–2021 Free
Software Foundation, Inc.

  

> Permission is granted to copy, distribute and/or modify this document
> under the terms of the GNU Free Documentation License, Version 1.2 or
> any later version published by the Free Software Foundation; with no
> Invariant Sections, with the Front-Cover texts being “A GNU Manual”,
> and with the Back-Cover Texts as in (a) below. A copy of the license
> is included in the section entitled “GNU Free Documentation License”.
>
> \(a\) The FSF’s Back-Cover Text is: “You have freedom to copy and
> modify this GNU Manual, like GNU software. Copies published by the
> Free Software Foundation raise funds for GNU development.”

  
  

Published by the Free Software Foundation  
51 Franklin Street, Fifth Floor,  
Boston, MA 02110-1301, USA  

------------------------------------------------------------------------

<span id="Top"></span>

|          |                                                           |     |                                                   |                                     |                                      |
|:---------|:----------------------------------------------------------|:----|:--------------------------------------------------|:------------------------------------|:-------------------------------------|
| \[ \< \] | \[ [\>](#Introduction "Next section in reading order") \] |     | \[[Contents](#SEC_Contents "Table of contents")\] | \[[Index](#Concept-Index "Index")\] | \[ [?](#SEC_About "About (help)") \] |

<span id="GNU-CPIO"></span>

# GNU CPIO

This manual documents GNU cpio (version 2.13.90, 6 January 2021).

Copyright © 1995, 2001–2002, 2004, 2010, 2014–2015, 2017, 2020–2021 Free
Software Foundation, Inc.

  

> Permission is granted to copy, distribute and/or modify this document
> under the terms of the GNU Free Documentation License, Version 1.2 or
> any later version published by the Free Software Foundation; with no
> Invariant Sections, with the Front-Cover texts being “A GNU Manual”,
> and with the Back-Cover Texts as in (a) below. A copy of the license
> is included in the section entitled “GNU Free Documentation License”.
>
> \(a\) The FSF’s Back-Cover Text is: “You have freedom to copy and
> modify this GNU Manual, like GNU software. Copies published by the
> Free Software Foundation raise funds for GNU development.”

<table class="menu" data-border="0" data-cellspacing="0">
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<th style="text-align: left;" data-valign="top"><a
href="#Introduction">1 Introduction</a></th>
<td>  </td>
<td style="text-align: left;" data-valign="top"></td>
</tr>
<tr class="even">
<th style="text-align: left;" data-valign="top"><a href="#Tutorial">2
Tutorial</a></th>
<td>  </td>
<td style="text-align: left;" data-valign="top">Getting started.</td>
</tr>
<tr class="odd">
<th style="text-align: left;" data-valign="top"><a
href="#Invoking-cpio">3 Invoking cpio</a></th>
<td>  </td>
<td style="text-align: left;" data-valign="top">How to invoke
<code>cpio</code>.</td>
</tr>
<tr class="even">
<th style="text-align: left;" data-valign="top"><a href="#Media">4
Magnetic Media</a></th>
<td>  </td>
<td style="text-align: left;" data-valign="top">Using tapes and other
archive media.</td>
</tr>
<tr class="odd">
<th style="text-align: left;" data-valign="top"><a href="#Reports">5
Reporting bugs or suggestions</a></th>
<td>  </td>
<td style="text-align: left;" data-valign="top"></td>
</tr>
<tr class="even">
<th style="text-align: left;" data-valign="top"><a
href="#Concept-Index">Concept Index</a></th>
<td>  </td>
<td style="text-align: left;" data-valign="top">Concept index.</td>
</tr>
<tr class="odd">
<th style="text-align: left;" data-valign="top"><pre
class="menu-comment"><code> — The Detailed Node Listing —

Invoking cpio
</code></pre></th>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th style="text-align: left;" data-valign="top"><a
href="#Copy_002dout-mode">3.1 Copy-out mode</a></th>
<td>  </td>
<td style="text-align: left;" data-valign="top"></td>
</tr>
<tr class="odd">
<th style="text-align: left;" data-valign="top"><a
href="#Copy_002din-mode">3.2 Copy-in mode</a></th>
<td>  </td>
<td style="text-align: left;" data-valign="top"></td>
</tr>
<tr class="even">
<th style="text-align: left;" data-valign="top"><a
href="#Copy_002dpass-mode">3.3 Copy-pass mode</a></th>
<td>  </td>
<td style="text-align: left;" data-valign="top"></td>
</tr>
<tr class="odd">
<th style="text-align: left;" data-valign="top"><a href="#Options">3.4
Options</a></th>
<td>  </td>
<td style="text-align: left;" data-valign="top"></td>
</tr>
<tr class="even">
<th style="text-align: left;" data-valign="top"><pre
class="menu-comment"><code></code></pre></th>
<td></td>
<td style="text-align: left;"></td>
</tr>
</tbody>
</table>

------------------------------------------------------------------------

<span id="Introduction"></span>

|                                                                    |                                                      |                               |                                                       |                                        |     |     |     |     |                                           |                                                   |                                     |                                      |
|:-------------------------------------------------------------------|:-----------------------------------------------------|:------------------------------|:------------------------------------------------------|:---------------------------------------|:----|:----|:----|:----|:------------------------------------------|:--------------------------------------------------|:------------------------------------|:-------------------------------------|
| \[ [\<\<](#Top "Beginning of this chapter or previous chapter") \] | \[ [\<](#Top "Previous section in reading order") \] | \[ [Up](#Top "Up section") \] | \[ [\>](#Tutorial "Next section in reading order") \] | \[ [\>\>](#Tutorial "Next chapter") \] |     |     |     |     | \[[Top](#Top "Cover (top) of document")\] | \[[Contents](#SEC_Contents "Table of contents")\] | \[[Index](#Concept-Index "Index")\] | \[ [?](#SEC_About "About (help)") \] |

<span id="Introduction-1"></span>

# 1 Introduction

GNU `cpio` copies files into or out of a `cpio` or `tar` archive, The
archive can be another file on the disk, a magnetic tape, or a pipe.

GNU `cpio` supports the following archive formats: binary, old ASCII,
new ASCII, crc, HPUX binary, HPUX old ASCII, old tar, and POSIX.1 tar.
The tar format is provided for compatibility with the `tar` program. By
default, `cpio` creates binary format archives, for compatibility with
older `cpio` programs. When extracting from archives, `cpio`
automatically recognizes which kind of archive it is reading and can
read archives created on machines with a different byte-order.

------------------------------------------------------------------------

<span id="Tutorial"></span>

|                                                                             |                                                               |                               |                                                            |                                             |     |     |     |     |                                           |                                                   |                                     |                                      |
|:----------------------------------------------------------------------------|:--------------------------------------------------------------|:------------------------------|:-----------------------------------------------------------|:--------------------------------------------|:----|:----|:----|:----|:------------------------------------------|:--------------------------------------------------|:------------------------------------|:-------------------------------------|
| \[ [\<\<](#Introduction "Beginning of this chapter or previous chapter") \] | \[ [\<](#Introduction "Previous section in reading order") \] | \[ [Up](#Top "Up section") \] | \[ [\>](#Invoking-cpio "Next section in reading order") \] | \[ [\>\>](#Invoking-cpio "Next chapter") \] |     |     |     |     | \[[Top](#Top "Cover (top) of document")\] | \[[Contents](#SEC_Contents "Table of contents")\] | \[[Index](#Concept-Index "Index")\] | \[ [?](#SEC_About "About (help)") \] |

<span id="Tutorial-1"></span>

# 2 Tutorial

<span id="index-creating-a-cpio-archive"></span> <span
id="index-extracting-a-cpio-archive"></span> <span
id="index-copying-directory-structures"></span> <span
id="index-passing-directory-structures"></span>

GNU `cpio` performs three primary functions. Copying files to an
archive, Extracting files from an archive, and passing files to another
directory tree. An archive can be a file on disk, one or more floppy
disks, or one or more tapes.

When creating an archive, `cpio` takes the list of files to be processed
from the standard input, and then sends the archive to the standard
output, or to the device defined by the ‘`-F`’ option. See section
[Copy-out mode](#Copy_002dout-mode). Usually `find` or `ls` is used to
provide this list to the standard input. In the following example you
can see the possibilities for archiving the contents of a single
directory.

<div class="example">

<table class="cartouche" data-border="1">
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><pre class="example"><code>% ls | cpio -ov &gt; directory.cpio</code></pre></td>
</tr>
</tbody>
</table>

</div>

The ‘`-o`’ option creates the archive, and the ‘`-v`’ option prints the
names of the files archived as they are added. Notice that the options
can be put together after a single ‘`-`’ or can be placed separately on
the command line. The ‘`>`’ redirects the `cpio` output to the file
‘directory.cpio’.

If you wanted to archive an entire directory tree, the `find` command
can provide the file list to `cpio`:

<div class="example">

<table class="cartouche" data-border="1">
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><pre class="example"><code>% find . -print -depth | cpio -ov &gt; tree.cpio</code></pre></td>
</tr>
</tbody>
</table>

</div>

This will take all the files in the current directory, the directories
below and place them in the archive ‘tree.cpio’. Again the ‘`-o`’
creates an archive, and the ‘`-v`’ option shows you the name of the
files as they are archived. See section [Copy-out
mode](#Copy_002dout-mode). Using the ‘`.`’ in the `find` statement will
give you more flexibility when doing restores, as it will save file
names with a relative path vice a hard wired, absolute path. The
‘`-depth`’ option forces `find` to print of the entries in a directory
before printing the directory itself. This limits the effects of
restrictive directory permissions by printing the directory entries in a
directory before the directory name itself.

Extracting an archive requires a bit more thought. First of all, by
default `cpio` extracts the files with exactly the same name as stored
in the archive. That means that if the archive contains absolute paths,
you will extract files to their absolute locations no matter what
directory you’re in when running the command. You can instruct `cpio` to
remove leading slashes using the ‘`--no-absolute-filenames`’ option.
Nevertheless, the good practice is to always test the archive using
`cpio -t` prior to extracting it.

Furthermore, `cpio` will not create directories by default. Another
characteristic, is it will not overwrite existing files unless you tell
it to.

<div class="example">

<table class="cartouche" data-border="1">
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><pre class="example"><code>% cpio -iv &lt; directory.cpio</code></pre></td>
</tr>
</tbody>
</table>

</div>

This will retrieve the files archived in the file ‘directory.cpio’ and
restore them to their locations. The ‘`-i`’ option extracts the archive
and the ‘`-v`’ shows the file names as they are extracted. If you are
dealing with an archived directory tree, you need to use the ‘`-d`’
option to create directories as necessary, something like:

<div class="example">

<table class="cartouche" data-border="1">
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><pre class="example"><code>% cpio -idv &lt; tree.cpio</code></pre></td>
</tr>
</tbody>
</table>

</div>

This will take the contents of the archive ‘tree.cpio’ and extract it.
If you try to extract the files on top of files of the same name that
already exist (and have the same or later modification time) `cpio` will
not extract the file unless told to do so by the ‘`-u`’ option. See
section [Copy-in mode](#Copy_002din-mode).

In copy-pass mode, `cpio` copies files from one directory tree to
another, combining the copy-out and copy-in steps without actually using
an archive. It reads the list of files to copy from the standard input;
the directory into which it will copy them is given as a non-option
argument. See section [Copy-pass mode](#Copy_002dpass-mode).

<div class="example">

<table class="cartouche" data-border="1">
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><pre class="example"><code>% find . -depth -print0 | cpio --null -pvd new-dir</code></pre></td>
</tr>
</tbody>
</table>

</div>

The example shows copying the files of the present directory, and
sub-directories to a new directory called new-dir. Some new options are
the ‘`-print0`’ available with GNU `find`, combined with the ‘`--null`’
option of `cpio`. These two options act together to send file names
between `find` and `cpio`, even if special characters are embedded in
the file names. Another is ‘`-p`’, which tells `cpio` to pass the files
it finds to the directory ‘new-dir’.

------------------------------------------------------------------------

<span id="Invoking-cpio"></span>

|                                                                         |                                                           |                               |                                                                |                                     |     |     |     |     |                                           |                                                   |                                     |                                      |
|:------------------------------------------------------------------------|:----------------------------------------------------------|:------------------------------|:---------------------------------------------------------------|:------------------------------------|:----|:----|:----|:----|:------------------------------------------|:--------------------------------------------------|:------------------------------------|:-------------------------------------|
| \[ [\<\<](#Tutorial "Beginning of this chapter or previous chapter") \] | \[ [\<](#Tutorial "Previous section in reading order") \] | \[ [Up](#Top "Up section") \] | \[ [\>](#Copy_002dout-mode "Next section in reading order") \] | \[ [\>\>](#Media "Next chapter") \] |     |     |     |     | \[[Top](#Top "Cover (top) of document")\] | \[[Contents](#SEC_Contents "Table of contents")\] | \[[Index](#Concept-Index "Index")\] | \[ [?](#SEC_About "About (help)") \] |

<span id="Invoking-cpio-1"></span>

# 3 Invoking cpio

<span id="index-invoking-cpio"></span> <span
id="index-command-line-options"></span>

|                                           |     |     |
|:------------------------------------------|-----|:----|
| [3.1 Copy-out mode](#Copy_002dout-mode)   |     |     |
| [3.2 Copy-in mode](#Copy_002din-mode)     |     |     |
| [3.3 Copy-pass mode](#Copy_002dpass-mode) |     |     |
| [3.4 Options](#Options)                   |     |     |

------------------------------------------------------------------------

<span id="Copy_002dout-mode"></span>

|                                                                              |                                                                |                                         |                                                               |                                     |     |     |     |     |                                           |                                                   |                                     |                                      |
|:-----------------------------------------------------------------------------|:---------------------------------------------------------------|:----------------------------------------|:--------------------------------------------------------------|:------------------------------------|:----|:----|:----|:----|:------------------------------------------|:--------------------------------------------------|:------------------------------------|:-------------------------------------|
| \[ [\<\<](#Invoking-cpio "Beginning of this chapter or previous chapter") \] | \[ [\<](#Invoking-cpio "Previous section in reading order") \] | \[ [Up](#Invoking-cpio "Up section") \] | \[ [\>](#Copy_002din-mode "Next section in reading order") \] | \[ [\>\>](#Media "Next chapter") \] |     |     |     |     | \[[Top](#Top "Cover (top) of document")\] | \[[Contents](#SEC_Contents "Table of contents")\] | \[[Index](#Concept-Index "Index")\] | \[ [?](#SEC_About "About (help)") \] |

<span id="Copy_002dout-mode-1"></span>

## 3.1 Copy-out mode

<span id="copy_002dout"></span> <span id="index-copy_002dout"></span>
<span id="index-archive-creation"></span> <span
id="index-create-archive"></span> In copy-out mode, `cpio` copies files
into an archive. It reads a list of filenames, one per line, on the
standard input, and writes the archive onto the standard output. A
typical way to generate the list of filenames is with the `find`
command; you should give `find` the ‘`-depth`’ option to minimize
problems with permissions on directories that are unreadable.

Copy-out mode is requested by the ‘`-o`’ (‘`--create`’) command line
option, e.g.:

<div class="example">

<table class="cartouche" data-border="1">
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><pre class="example"><code>% find | cpio -o &gt; directory.cpio</code></pre></td>
</tr>
</tbody>
</table>

</div>

The following options can be used in copy-out mode:

‘`-0`’  
‘`--null`’  
Filenames in the list are delimited by ASCII null characters instead of
newlines.

‘`-A`’  
‘`--append`’  
Append to an existing archive.

‘`-a`’  
‘`--reset-access-time`’  
Reset the access times of files after reading them.

‘`--absolute-filenames`’  
Do not strip file system prefix components from the file names. This is
the default.

‘`--no-absolute-filenames`’  
Strip file system prefix components from the file names before storing
them to the archive.

‘`--block-size=block-size`’  
Sets the I/O block size to `block-size` \* 512 bytes.

‘`-B`’  
Set the I/O block size to 5120 bytes.

‘`-c`’  
Use the old portable (ASCII) archive format.

‘`-C number`’  
‘`--io-size=number`’  
Set the I/O block size to the given `number` of bytes.

‘`-D dir`’  
‘`--directory=dir`’  
Change to directory `dir`

‘`--force-local`’  
Treat the archive file as local, even if its name contains colons.

‘`-F [[user@]host:]archive-file`’  
‘`-O [[user@]host:]archive-file`’  
‘`--file=[[user@]host:]archive-file`’  
Use the supplied `archive-file` instead of standard input. Optional
`user` and `host` specify the user and host names in case of a remote
archive.

‘`-H format`’  
‘`--format=format`’  
Use given archive format. See [format](#format), for a list of available
formats.

‘`-L`’  
‘`--dereference`’  
Dereference symbolic links (copy the files that they point to instead of
copying the links).

‘`-M string`’  
‘`--message=string`’  
Print `string` when the end of a volume of the backup media is reached.

‘`--quiet`’  
Do not print the number of blocks copied.

‘`--rsh-command=command`’  
Use `command` instead of `rsh` to access remote archives.

‘`-R`’  
‘`--owner=[user][:.][group]`’  
Set the ownership of all files created to the specified `user` and/or
`group`. See [owner](#owner).

‘`-v`’  
‘`--verbose`’  
Verbosely list the files processed.

‘`-V`’  
‘`--dot`’  
Print a ‘`.`’ for each file processed.

‘`-W`’  
‘`--warning=flag`’  
Control warning display. Argument is one of ‘`none`’, ‘`truncate`’,
‘`no-truncate`’ or ‘`all`’. See [warning](#warning), for a detailed
discussion of these.

------------------------------------------------------------------------

<span id="Copy_002din-mode"></span>

|                                                                              |                                                                    |                                         |                                                                 |                                     |     |     |     |     |                                           |                                                   |                                     |                                      |
|:-----------------------------------------------------------------------------|:-------------------------------------------------------------------|:----------------------------------------|:----------------------------------------------------------------|:------------------------------------|:----|:----|:----|:----|:------------------------------------------|:--------------------------------------------------|:------------------------------------|:-------------------------------------|
| \[ [\<\<](#Invoking-cpio "Beginning of this chapter or previous chapter") \] | \[ [\<](#Copy_002dout-mode "Previous section in reading order") \] | \[ [Up](#Invoking-cpio "Up section") \] | \[ [\>](#Copy_002dpass-mode "Next section in reading order") \] | \[ [\>\>](#Media "Next chapter") \] |     |     |     |     | \[[Top](#Top "Cover (top) of document")\] | \[[Contents](#SEC_Contents "Table of contents")\] | \[[Index](#Concept-Index "Index")\] | \[ [?](#SEC_About "About (help)") \] |

<span id="Copy_002din-mode-1"></span>

## 3.2 Copy-in mode

<span id="copy_002din"></span> <span id="index-copy_002din"></span>
<span id="index-archive-extraction"></span> <span
id="index-extract-files-from-an-archive"></span> In copy-in mode, `cpio`
copies files from an archive into the filesystem or lists the archive
contents. It reads the archive from the standard input. Any non-option
command line arguments are shell globbing patterns; only files in the
archive whose names match one or more of those patterns are copied from
the archive. Unlike in the shell, an initial ‘`.`’ in a filename does
match a wildcard at the start of a pattern, and a ‘`/`’ in a filename
can match wildcards. If no patterns are given, all files are extracted.

The copy-in mode is requested by the ‘`-i`’ (‘`--extract`’) command line
option.

The following options can be used in copy-in mode:

‘`--absolute-filenames`’  
Do not strip file system prefix components from the file names. This is
the default.

‘`--no-absolute-filenames`’  
Create all files relative to the current directory.

‘`--block-size=block-size`’  
Sets the I/O block size to `block-size` \* 512 bytes.

‘`-b`’  
‘`--swap`’  
Swap both halfwords of words and bytes of halfwords in the data.
Equivalent to ‘`-sS`’.

‘`-B`’  
Set the I/O block size to 5120 bytes.

‘`-c`’  
Use the old portable (ASCII) archive format.

‘`-C number`’  
‘`--io-size=number`’  
Set the I/O block size to the given `number` of bytes.

‘`-D dir`’  
‘`--directory=dir`’  
Change to directory `dir`

‘`-d`’  
‘`--make-directories`’  
Create leading directories where needed.

‘`-E file`’  
‘`--pattern-file=file`’  
Read additional patterns specifying filenames to extract or list from
`file`.

‘`-f`’  
‘`--nonmatching`’  
Only copy files that do not match any of the given patterns.

‘`--force-local`’  
Treat the archive file as local, even if its name contains colons.

‘`-F [[user@]host:]archive-file`’  
‘`-I [[user@]host:]archive-file`’  
‘`--file=[[user@]host:]archive-file`’  
Use the supplied `archive-file` instead of standard input. Optional
`user` and `host` specify the user and host names in case of a remote
archive.

‘`-H format`’  
‘`--format=format`’  
Use given archive format. See [format](#format), for a list of available
formats.

‘`-m`’  
‘`--preserve-modification-time`’  
Retain previous file modification times when creating files.

‘`-M string`’  
‘`--message=string`’  
Print `string` when the end of a volume of the backup media is reached.

‘`--no-preserve-owner`’  
Do not change the ownership of the files.

‘`-n`’  
‘`--numeric-uid-gid`’  
In the verbose table of contents listing, show numeric UID and GID
values.

‘`--only-verify-crc`’  
When reading a CRC format archive, only verify the CRC’s of each file in
the archive, don’t actually extract the files

‘`--quiet`’  
Do not print the number of blocks copied.

‘`--rsh-command=command`’  
Use `command` instead of `rsh` to access remote archives.

‘`-r`’  
‘`--rename`’  
Interactively rename files

‘`--sparse`’  
Write files with large blocks of zeros as sparse files.

‘`-s`’  
‘`--swap-bytes`’  
Swap the bytes of each halfword in the files

‘`-S`’  
‘`--swap-halfwords`’  
Swap the halfwords of each word (4 bytes) in the files

‘`--to-stdout`’  
Extract files to standard output.

‘`-u`’  
‘`--unconditional`’  
Replace all files unconditionally.

‘`-v`’  
‘`--verbose`’  
Verbosely list the files processed.

‘`-V`’  
‘`--dot`’  
Print a ‘`.`’ for each file processed.

‘`-W`’  
‘`--warning=flag`’  
Control warning display. Argument is one of ‘`none`’, ‘`truncate`’,
‘`no-truncate`’ or ‘`all`’. See [warning](#warning), for a detailed
discussion of these.

------------------------------------------------------------------------

<span id="Copy_002dpass-mode"></span>

|                                                                              |                                                                   |                                         |                                                      |                                     |     |     |     |     |                                           |                                                   |                                     |                                      |
|:-----------------------------------------------------------------------------|:------------------------------------------------------------------|:----------------------------------------|:-----------------------------------------------------|:------------------------------------|:----|:----|:----|:----|:------------------------------------------|:--------------------------------------------------|:------------------------------------|:-------------------------------------|
| \[ [\<\<](#Invoking-cpio "Beginning of this chapter or previous chapter") \] | \[ [\<](#Copy_002din-mode "Previous section in reading order") \] | \[ [Up](#Invoking-cpio "Up section") \] | \[ [\>](#Options "Next section in reading order") \] | \[ [\>\>](#Media "Next chapter") \] |     |     |     |     | \[[Top](#Top "Cover (top) of document")\] | \[[Contents](#SEC_Contents "Table of contents")\] | \[[Index](#Concept-Index "Index")\] | \[ [?](#SEC_About "About (help)") \] |

<span id="Copy_002dpass-mode-1"></span>

## 3.3 Copy-pass mode

<span id="copy_002dpass"></span> <span id="index-copy_002dpass"></span>
<span id="index-copy-files-between-filesystems"></span>

In copy-pass mode, `cpio` copies files from one directory tree to
another, combining the copy-out and copy-in steps without actually using
an archive. It reads the list of files to copy from the standard input;
the directory into which it will copy them is given as a non-option
argument.

This mode is requested by the ‘`-p`’ (‘`--pass-through`’) command line
option.

The following options are valid in copy-out mode:

‘`-0`’  
‘`--null`’  
Filenames in the list are delimited by ASCII null characters instead of
newlines.

‘`-a`’  
‘`--reset-access-time`’  
Reset the access times of files after reading them.

‘`-b`’  
‘`--swap`’  
Swap both halfwords of words and bytes of halfwords in the data.
Equivalent to ‘`-sS`’.

‘`--block-size=block-size`’  
Sets the I/O block size to `block-size` \* 512 bytes.

‘`-B`’  
Set the I/O block size to 5120 bytes.

‘`-c`’  
Use the old portable (ASCII) archive format.

‘`-C number`’  
‘`--io-size=number`’  
Set the I/O block size to the given `number` of bytes.

‘`-d`’  
‘`--make-directories`’  
Create leading directories where needed.

‘`--device-independent`’  
‘`--reproducible`’  
Create reproducible archives. This is equivalent to
‘`--ignore-devno --renumber-inodes`’.

‘`-D dir`’  
‘`--directory=dir`’  
Change to directory `dir`

‘`-E file`’  
‘`--pattern-file=file`’  
Read additional patterns specifying filenames to extract or list from
`file`.

‘`-f`’  
‘`--nonmatching`’  
Only copy files that do not match any of the given patterns.

‘`-F [[user@]host:]archive-file`’  
‘`-O [[user@]host:]archive-file`’  
‘`--file=[[user@]host:]archive-file`’  
Use the supplied `archive-file` instead of standard input. Optional
`user` and `host` specify the user and host names in case of a remote
archive.

‘`--force-local`’  
Treat the archive file as local, even if its name contains colons.

‘`-H format`’  
‘`--format=format`’  
Use given archive format. See [format](#format), for a list of available
formats.

‘`--ignore-devno`’  
Store 0 in the device number field of each archive member, instead of
the actual device number.

‘`-l`’  
‘`--link`’  
Link files instead of copying them, when possible.

‘`-L`’  
‘`--dereference`’  
Dereference symbolic links (copy the files that they point to instead of
copying the links).

‘`-m`’  
‘`--preserve-modification-time`’  
Retain previous file modification times when creating files.

‘`-M string`’  
‘`--message=string`’  
Print `string` when the end of a volume of the backup media is reached.

‘`-n`’  
‘`--numeric-uid-gid`’  
In the verbose table of contents listing, show numeric UID and GID
values.

‘`--no-preserve-owner`’  
Do not change the ownership of the files.

‘`--only-verify-crc`’  
When reading a CRC format archive, only verify the CRC’s of each file in
the archive, don’t actually extract the files

‘`--quiet`’  
Do not print the number of blocks copied.

‘`--rsh-command=command`’  
Use `command` instead of `rsh` to access remote archives.

‘`-r`’  
‘`--rename`’  
Interactively rename files

‘`--renumber-inodes`’  
Renumber inodes when storing them in the archive.

‘`-R`’  
‘`--owner=[user][:.][group]`’  
Set the ownership of all files created to the specified `user` and/or
`group`. See [owner](#owner).

‘`-s`’  
‘`--swap-bytes`’  
Swap the bytes of each halfword in the files

‘`--sparse`’  
Write files with large blocks of zeros as sparse files.

‘`-S`’  
‘`--swap-halfwords`’  
Swap the halfwords of each word (4 bytes) in the files

‘`--to-stdout`’  
Extract files to standard output.

‘`-u`’  
‘`--unconditional`’  
Replace all files unconditionally.

‘`-v`’  
‘`--verbose`’  
Verbosely list the files processed.

‘`-V`’  
‘`--dot`’  
Print a ‘`.`’ for each file processed.

‘`-W`’  
‘`--warning=flag`’  
Control warning display. Argument is one of ‘`none`’, ‘`truncate`’,
‘`no-truncate`’ or ‘`all`’. See [warning](#warning), for a detailed
discussion of these.

------------------------------------------------------------------------

<span id="Options"></span>

|                                                                              |                                                                     |                                         |                                                    |                                     |     |     |     |     |                                           |                                                   |                                     |                                      |
|:-----------------------------------------------------------------------------|:--------------------------------------------------------------------|:----------------------------------------|:---------------------------------------------------|:------------------------------------|:----|:----|:----|:----|:------------------------------------------|:--------------------------------------------------|:------------------------------------|:-------------------------------------|
| \[ [\<\<](#Invoking-cpio "Beginning of this chapter or previous chapter") \] | \[ [\<](#Copy_002dpass-mode "Previous section in reading order") \] | \[ [Up](#Invoking-cpio "Up section") \] | \[ [\>](#Media "Next section in reading order") \] | \[ [\>\>](#Media "Next chapter") \] |     |     |     |     | \[[Top](#Top "Cover (top) of document")\] | \[[Contents](#SEC_Contents "Table of contents")\] | \[[Index](#Concept-Index "Index")\] | \[ [?](#SEC_About "About (help)") \] |

<span id="Options-1"></span>

## 3.4 Options

This section summarizes all available command line options. References
in square brackets after each option indicate `cpio` modes in which this
option is valid.

`-0`  
`--null`  
\[[copy-in](#copy_002din),[copy-out](#copy_002dout),[copy-pass](#copy_002dpass)\]  
Read a list of filenames terminated by a null character, instead of a
newline, so that files whose names contain newlines can be archived. GNU
`find` is one way to produce a list of null-terminated filenames. This
option may be used in copy-out and copy-pass modes.

`-a`  
`--reset-access-time`  
\[[copy-out](#copy_002dout),[copy-pass](#copy_002dpass)\]  
Reset the access times of files after reading them, so that it does not
look like they have just been read.

`-A`  
`--append`  
\[[copy-out](#copy_002dout)\]  
Append to an existing archive. Only works in copy-out mode. The archive
must be a disk file specified with the ‘`-O`’ or ‘`-F`’ (‘`--file`’)
option.

`-b`  
`--swap`  
\[[copy-in](#copy_002din)\]  
Swap both halfwords of words and bytes of halfwords in the data.
Equivalent to ‘`-sS`’. This option may be used in copy-in mode. Use this
option to convert 32-bit integers between big-endian and little-endian
machines.

`-B`  
\[[copy-in](#copy_002din),[copy-out](#copy_002dout),[copy-pass](#copy_002dpass)\]  
Set the I/O block size to 5120 bytes. Initially the block size is 512
bytes.

`--block-size=block-size`  
\[[copy-in](#copy_002din),[copy-out](#copy_002dout),[copy-pass](#copy_002dpass)\]  
Set the I/O block size to `block-size` \* 512 bytes.

`-c`  
\[[copy-in](#copy_002din),[copy-out](#copy_002dout),[copy-pass](#copy_002dpass)\]  
Use the old portable (ASCII) archive format.

`-C io-size`  
`--io-size=io-size`  
\[[copy-in](#copy_002din),[copy-out](#copy_002dout),[copy-pass](#copy_002dpass)\]  
Set the I/O block size to `io-size` bytes.

`-d`  
`--make-directories`  
\[[copy-in](#copy_002din),[copy-pass](#copy_002dpass)\]  
Create leading directories where needed.

`-D dir`  
`--directory=dir`  
\[[copy-in](#copy_002din),[copy-out](#copy_002dout),[copy-pass](#copy_002dpass)\]  
Change to the directory `dir` before starting the operation. This can be
used, for example, to extract an archive contents in a different
directory:

<div class="example">

``` example
$ cpio -i -D /usr/local < archive
```

</div>

or to copy-pass files from one directory to another:

<div class="example">

``` example
$ cpio -D /usr/bin -p /usr/local/bin < filelist
```

</div>

The ‘`-D`’ option does not affect file names supplied as arguments to
another command line options, such as ‘`-F`’ or ‘`-E`’. For example, the
following invocation:

<div class="example">

``` example
cpio -D /tmp/foo -d -i -F arc
```

</div>

instructs `cpio` to open the archive file ‘arc’ in the current working
directory, then change to the directory ‘/tmp/foo’ and extract files to
that directory. If ‘/tmp/foo’ does not exist, it will be created first
(the ‘`-d`’ option) and then changed to.

`-E file`  
`--pattern-file=file`  
\[[copy-in](#copy_002din)\]  
Read additional patterns specifying filenames to extract or list from
`file`. The lines of `file` are treated as if they had been non-option
arguments to `cpio`. This option is used in copy-in mode,

`-f`  
`--nonmatching`  
\[[copy-in](#copy_002din)\]  
Only copy files that do not match any of the given patterns.

`-F archive`  
`--file=archive`  
\[[copy-in](#copy_002din),[copy-out](#copy_002dout)\]  
Archive filename to use instead of standard input or output. To use a
tape drive on another machine as the archive, use a filename that starts
with ‘`hostname:`’, where `hostname` is the name or IP address of the
machine. The hostname can be preceded by a username and an ‘`@`’ to
access the remote tape drive as that user, if you have permission to do
so (typically an entry in that user’s ‘\~/.rhosts’ file).

`--force-local`  
\[[copy-in](#copy_002din),[copy-out](#copy_002dout)\]  
With ‘`-F`’, ‘`-I`’, or ‘`-O`’, take the archive file name to be a local
file even if it contains a colon, which would ordinarily indicate a
remote host name.

<span id="format"></span>

`-H format`  
`--format=format`  
\[[copy-in](#copy_002din),[copy-out](#copy_002dout),[copy-pass](#copy_002dpass)\]  
Use archive format `format`. The valid formats are listed below with
file size limits for individual files in parentheses; the same names are
also recognized in all-caps. The default in copy-in mode is to
automatically detect the archive format, and in copy-out mode is
‘`bin`’.

‘`bin`’  
The obsolete binary format. (2147483647 bytes)

‘`odc`’  
The old (POSIX.1) portable format. (8589934591 bytes)

‘`newc`’  
The new (SVR4) portable format, which supports file systems having more
than 65536 i-nodes. (4294967295 bytes)

‘`crc`’  
The new (SVR4) portable format with a checksum added.

‘`tar`’  
The old tar format. (8589934591 bytes)

‘`ustar`’  
The POSIX.1 tar format. Also recognizes GNU `tar` archives, which are
similar but not identical. (8589934591 bytes)

‘`hpbin`’  
The obsolete binary format used by HPUX’s `cpio` (which stores device
files differently).

‘`hpodc`’  
The portable format used by HPUX’s `cpio` (which stores device files
differently).

`-i`  
`--extract`  
Run in copy-in mode. See section [Copy-in mode](#Copy_002din-mode).

`-I archive`  
\[[copy-in](#copy_002din)\]  
Archive filename to use instead of standard input. To use a tape drive
on another machine as the archive, use a filename that starts with
‘`hostname:`’, where `hostname` is the name or IP address of the remote
host. The hostname can be preceded by a username and an ‘`@`’ to access
the remote tape drive as that user, if you have permission to do so
(typically an entry in that user’s ‘\~/.rhosts’ file).

`-l`  
`--link`  
\[[copy-pass](#copy_002dpass)\]  
Link files instead of copying them, when possible.

`-L`  
`--dereference`  
\[[copy-in](#copy_002din),[copy-pass](#copy_002dpass)\]  
Copy the file that a symbolic link points to, rather than the symbolic
link itself.

`-m`  
`--preserve-modification-time`  
\[[copy-in](#copy_002din),[copy-pass](#copy_002dpass)\]  
Retain previous file modification times when creating files.

`-M message`  
`--message=message`  
\[[copy-in](#copy_002din),[copy-out](#copy_002dout)\]  
Print `message` when the end of a volume of the backup media (such as a
tape or a floppy disk) is reached, to prompt the user to insert a new
volume. If `message` contains the string ‘`%d`’, it is replaced by the
current volume number (starting at 1).

`-n`  
`--numeric-uid-gid`  
\[[copy-in](#copy_002din)\]  
Show numeric UID and GID instead of translating them into names when
using the ‘`--verbose`’ option.

`--no-absolute-filenames`  
\[[copy-in](#copy_002din),[copy-out](#copy_002dout)\]  
Create all files relative to the current directory in copy-in mode, even
if they have an absolute file name in the archive.

`--no-preserve-owner`  
\[[copy-in](#copy_002din),[copy-pass](#copy_002dpass)\]  
Do not change the ownership of the files; leave them owned by the user
extracting them. This is the default for non-root users, so that users
on System V don’t inadvertantly give away files. This option can be used
in copy-in mode and copy-pass mode

`-o`  
`--create`  
Run in copy-out mode. See section [Copy-out mode](#Copy_002dout-mode).

`-O archive`  
\[[copy-out](#copy_002dout)\]  
Archive filename to use instead of standard output. To use a tape drive
on another machine as the archive, use a filename that starts with
‘`hostname:`’, where `hostname` is the name or IP address of the
machine. The hostname can be preceded by a username and an ‘`@`’ to
access the remote tape drive as that user, if you have permission to do
so (typically an entry in that user’s ‘\~/.rhosts’ file).

`--only-verify-crc`  
\[[copy-in](#copy_002din)\]  
Verify the CRC’s of each file in the archive, when reading a CRC format
archive. Don’t actually extract the files.

`-p`  
`--pass-through`  
Run in copy-pass mode. See section [Copy-pass
mode](#Copy_002dpass-mode).

`--quiet`  
\[[copy-in](#copy_002din),[copy-out](#copy_002dout),[copy-pass](#copy_002dpass)\]  
Do not print the number of blocks copied.

`-r`  
`--rename`  
\[[copy-in](#copy_002din)\]  
Interactively rename files.

<span id="owner"></span>

`-R owner`  
`--owner owner`  
\[[copy-in](#copy_002din),[copy-out](#copy_002dout),[copy-pass](#copy_002dpass)\]  
In copy-in and copy-pass mode, set the ownership of all files created to
the specified `owner` (this operation is allowed only for the
super-user). In copy-out mode, store the supplied owner information in
the archive.

The argument can be either the user name or the user name and group
name, separated by a dot or a colon, or the group name, preceeded by a
dot or a colon, as shown in the examples below:

<div class="smallexample">

``` smallexample
cpio --owner smith
cpio --owner smith:
cpio --owner smith:users
cpio --owner :users
```

</div>

The argument parts are first looked up in the system user and group
databases, correspondingly. If any of them is not found there, it is
treated as numeric UID or GID, provided that it consists of decimal
digits only.

To avoid the lookup and ensure that arguments are treated as numeric
values, prefix them with a plus sign, e.g.:

<div class="smallexample">

``` smallexample
cpio --owner +0
cpio --owner +0:
cpio --owner +0:+0
cpio --owner :+0
```

</div>

If the group is omitted but the ‘`:`’ or ‘`.`’ separator is given, as in
the second example. the given user’s login group will be used.

`--rsh-command=command`  
\[[copy-in](#copy_002din),[copy-out](#copy_002dout),[copy-pass](#copy_002dpass)\]  
Notifies `cpio` that is should use `command` to communicate with remote
devices.

`-s`  
`--swap-bytes`  
\[[copy-in](#copy_002din)\]  
Swap the bytes of each halfword (pair of bytes) in the files. This
option can be used in copy-in mode.

`-S`  
`--swap-halfwords`  
\[[copy-in](#copy_002din)\]  
Swap the halfwords of each word (4 bytes) in the files. This option may
be used in copy-in mode.

`--sparse`  
\[[copy-in](#copy_002din),[copy-pass](#copy_002dpass)\]  
Write files with large blocks of zeros as sparse files. This option is
used in copy-in and copy-pass modes.

`-t`  
`--list`  
\[[copy-in](#copy_002din)\]  
Print a table of contents of the input. Can be used alone, as a mode
designator, in which case ‘`-i`’ is implied.

`--to-stdout`  
\[[copy-in](#copy_002din)\]  
Extract files to standard output. This option may be used in copy-in
mode.

`-u`  
`--unconditional`  
\[[copy-in](#copy_002din),[copy-pass](#copy_002dpass)\]  
Replace all files, without asking whether to replace existing newer
files with older files.

`-v`  
`--verbose`  
\[[copy-in](#copy_002din),[copy-out](#copy_002dout),[copy-pass](#copy_002dpass)\]  
List the files processed, or with ‘`-t`’, give an `ls -l` style table of
contents listing. In a verbose table of contents of a ustar archive,
user and group names in the archive that do not exist on the local
system are replaced by the names that correspond locally to the numeric
UID and GID stored in the archive.

`-V`  
`--dot`  
\[[copy-in](#copy_002din),[copy-out](#copy_002dout),[copy-pass](#copy_002dpass)\]  
Print a ‘`.`’ for each file processed.

`--version`  
Print the `cpio` program version number and exit.

<span id="warning"></span>

`-W`  
`--warning=flag`  
\[[copy-in](#copy_002din),[copy-out](#copy_002dout),[copy-pass](#copy_002dpass)\]  
Control warning display. The argument is one of the following:

none  
Disable all warnings.

all  
Enable all warnings.

truncate  
Warn about truncation of file header fields.

no-truncate  
Disable truncation warnings.

------------------------------------------------------------------------

<span id="Media"></span>

|                                                                              |                                                          |                               |                                                      |                                       |     |     |     |     |                                           |                                                   |                                     |                                      |
|:-----------------------------------------------------------------------------|:---------------------------------------------------------|:------------------------------|:-----------------------------------------------------|:--------------------------------------|:----|:----|:----|:----|:------------------------------------------|:--------------------------------------------------|:------------------------------------|:-------------------------------------|
| \[ [\<\<](#Invoking-cpio "Beginning of this chapter or previous chapter") \] | \[ [\<](#Options "Previous section in reading order") \] | \[ [Up](#Top "Up section") \] | \[ [\>](#Reports "Next section in reading order") \] | \[ [\>\>](#Reports "Next chapter") \] |     |     |     |     | \[[Top](#Top "Cover (top) of document")\] | \[[Contents](#SEC_Contents "Table of contents")\] | \[[Index](#Concept-Index "Index")\] | \[ [?](#SEC_About "About (help)") \] |

<span id="Magnetic-Media"></span>

# 4 Magnetic Media

<span id="index-magnetic-media"></span>

Archives are usually written on removable media–tape cartridges, mag
tapes, or floppy disks.

The amount of data a tape or disk holds depends not only on its size,
but also on how it is formatted. A 2400 foot long reel of mag tape holds
40 megabytes of data when formated at 1600 bits per inch. The physically
smaller EXABYTE tape cartridge holds 2.3 gigabytes.

Magnetic media are re-usable–once the archive on a tape is no longer
needed, the archive can be erased and the tape or disk used over. Media
quality does deteriorate with use, however. Most tapes or disks should
be disgarded when they begin to produce data errors.

Magnetic media are written and erased using magnetic fields, and should
be protected from such fields to avoid damage to stored data. Sticking a
floppy disk to a filing cabinet using a magnet is probably not a good
idea.

------------------------------------------------------------------------

<span id="Reports"></span>

|                                                                      |                                                        |                               |                                                            |                                             |     |     |     |     |                                           |                                                   |                                     |                                      |
|:---------------------------------------------------------------------|:-------------------------------------------------------|:------------------------------|:-----------------------------------------------------------|:--------------------------------------------|:----|:----|:----|:----|:------------------------------------------|:--------------------------------------------------|:------------------------------------|:-------------------------------------|
| \[ [\<\<](#Media "Beginning of this chapter or previous chapter") \] | \[ [\<](#Media "Previous section in reading order") \] | \[ [Up](#Top "Up section") \] | \[ [\>](#Concept-Index "Next section in reading order") \] | \[ [\>\>](#Concept-Index "Next chapter") \] |     |     |     |     | \[[Top](#Top "Cover (top) of document")\] | \[[Contents](#SEC_Contents "Table of contents")\] | \[[Index](#Concept-Index "Index")\] | \[ [?](#SEC_About "About (help)") \] |

<span id="Reporting-bugs-or-suggestions"></span>

# 5 Reporting bugs or suggestions

It is possible you will encounter a bug in `cpio`. If this happens, we
would like to hear about it. As the purpose of bug reporting is to
improve software, please be sure to include maximum information when
reporting a bug. The information needed is:

-   Version of the package you are using.
-   Compilation options used when configuring the package.
-   Conditions under which the bug appears.

Send your report to <bug-cpio@gnu.org>. This is a public mailing list;
all correspondence sent to it is archived and is available at
<https://lists.gnu.org/archive/html/bug-cpio>. Your bug report will be
visible there, too. The list is not limited to bug reports, in fact it
is dedicated to any kind of technical discussions regarding GNU `cpio`.
If you wish to subscribe to it, visit
<https://lists.gnu.org/mailman/listinfo/bug-cpio>.

------------------------------------------------------------------------

<span id="Concept-Index"></span>

|                                                                        |                                                          |                               |          |            |     |     |     |     |                                           |                                                   |                                     |                                      |
|:-----------------------------------------------------------------------|:---------------------------------------------------------|:------------------------------|:---------|:-----------|:----|:----|:----|:----|:------------------------------------------|:--------------------------------------------------|:------------------------------------|:-------------------------------------|
| \[ [\<\<](#Reports "Beginning of this chapter or previous chapter") \] | \[ [\<](#Reports "Previous section in reading order") \] | \[ [Up](#Top "Up section") \] | \[ \> \] | \[ \>\> \] |     |     |     |     | \[[Top](#Top "Cover (top) of document")\] | \[[Contents](#SEC_Contents "Table of contents")\] | \[[Index](#Concept-Index "Index")\] | \[ [?](#SEC_About "About (help)") \] |

<span id="Concept-Index-1"></span>

# Concept Index

|            |                                                                                        |
|------------|----------------------------------------------------------------------------------------|
| Jump to:   | <a href="#Concept-Index-1_cp_letter-A"                                                 
              class="summary-letter"><strong>A</strong></a>   <a href="#Concept-Index-1_cp_letter-C"  
              class="summary-letter"><strong>C</strong></a>   <a href="#Concept-Index-1_cp_letter-E"  
              class="summary-letter"><strong>E</strong></a>   <a href="#Concept-Index-1_cp_letter-I"  
              class="summary-letter"><strong>I</strong></a>   <a href="#Concept-Index-1_cp_letter-M"  
              class="summary-letter"><strong>M</strong></a>   <a href="#Concept-Index-1_cp_letter-P"  
              class="summary-letter"><strong>P</strong></a>                                           |

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
<th><span id="Concept-Index-1_cp_letter-A">A</span></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-archive-creation">archive creation</a></td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Copy_002dout-mode">3.1 Copy-out mode</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-archive-extraction">archive extraction</a></td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Copy_002din-mode">3.2 Copy-in mode</a></td>
</tr>
<tr class="even">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th><span id="Concept-Index-1_cp_letter-C">C</span></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-command-line-options">command line options</a></td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Invoking-cpio">3 Invoking cpio</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-copy-files-between-filesystems">copy files between
filesystems</a></td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Copy_002dpass-mode">3.3 Copy-pass mode</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-copy_002din">copy-in</a></td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Copy_002din-mode">3.2 Copy-in mode</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-copy_002dout">copy-out</a></td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Copy_002dout-mode">3.1 Copy-out mode</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-copy_002dpass">copy-pass</a></td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Copy_002dpass-mode">3.3 Copy-pass mode</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-copying-directory-structures">copying directory
structures</a></td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a href="#Tutorial">2
Tutorial</a></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-create-archive">create archive</a></td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Copy_002dout-mode">3.1 Copy-out mode</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-creating-a-cpio-archive">creating a cpio archive</a></td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a href="#Tutorial">2
Tutorial</a></td>
</tr>
<tr class="even">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th><span id="Concept-Index-1_cp_letter-E">E</span></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-extract-files-from-an-archive">extract files from an
archive</a></td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Copy_002din-mode">3.2 Copy-in mode</a></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-extracting-a-cpio-archive">extracting a cpio
archive</a></td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a href="#Tutorial">2
Tutorial</a></td>
</tr>
<tr class="even">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th><span id="Concept-Index-1_cp_letter-I">I</span></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-invoking-cpio">invoking cpio</a></td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a
href="#Invoking-cpio">3 Invoking cpio</a></td>
</tr>
<tr class="odd">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th><span id="Concept-Index-1_cp_letter-M">M</span></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-magnetic-media">magnetic media</a></td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a href="#Media">4
Magnetic Media</a></td>
</tr>
<tr class="even">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<th><span id="Concept-Index-1_cp_letter-P">P</span></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<th></th>
<td style="text-align: left;" data-valign="top"><a
href="#index-passing-directory-structures">passing directory
structures</a></td>
<td> </td>
<td style="text-align: left;" data-valign="top"><a href="#Tutorial">2
Tutorial</a></td>
</tr>
<tr class="odd">
<th><hr /></th>
<td style="text-align: left;"></td>
<td></td>
<td style="text-align: left;"></td>
</tr>
</tbody>
</table>

|            |                                                                                        |
|------------|----------------------------------------------------------------------------------------|
| Jump to:   | <a href="#Concept-Index-1_cp_letter-A"                                                 
              class="summary-letter"><strong>A</strong></a>   <a href="#Concept-Index-1_cp_letter-C"  
              class="summary-letter"><strong>C</strong></a>   <a href="#Concept-Index-1_cp_letter-E"  
              class="summary-letter"><strong>E</strong></a>   <a href="#Concept-Index-1_cp_letter-I"  
              class="summary-letter"><strong>I</strong></a>   <a href="#Concept-Index-1_cp_letter-M"  
              class="summary-letter"><strong>M</strong></a>   <a href="#Concept-Index-1_cp_letter-P"  
              class="summary-letter"><strong>P</strong></a>                                           |

------------------------------------------------------------------------

<span id="SEC_Contents"></span>

|                                           |                                                   |                                     |                                      |
|:------------------------------------------|:--------------------------------------------------|:------------------------------------|:-------------------------------------|
| \[[Top](#Top "Cover (top) of document")\] | \[[Contents](#SEC_Contents "Table of contents")\] | \[[Index](#Concept-Index "Index")\] | \[ [?](#SEC_About "About (help)") \] |

# Table of Contents

<div class="contents">

-   <a href="#Introduction" id="toc-Introduction-1">1 Introduction</a>
-   <a href="#Tutorial" id="toc-Tutorial-1">2 Tutorial</a>
-   <a href="#Invoking-cpio" id="toc-Invoking-cpio-1">3 Invoking cpio</a>
    -   <a href="#Copy_002dout-mode" id="toc-Copy_002dout-mode-1">3.1 Copy-out
        mode</a>
    -   <a href="#Copy_002din-mode" id="toc-Copy_002din-mode-1">3.2 Copy-in
        mode</a>
    -   <a href="#Copy_002dpass-mode" id="toc-Copy_002dpass-mode-1">3.3
        Copy-pass mode</a>
    -   <a href="#Options" id="toc-Options-1">3.4 Options</a>
-   <a href="#Media" id="toc-Magnetic-Media">4 Magnetic Media</a>
-   <a href="#Reports" id="toc-Reporting-bugs-or-suggestions">5 Reporting
    bugs or suggestions</a>
-   <a href="#Concept-Index" id="toc-Concept-Index-1">Concept Index</a>

</div>

------------------------------------------------------------------------

<span id="SEC_About"></span>

|                                           |                                                   |                                     |                                      |
|:------------------------------------------|:--------------------------------------------------|:------------------------------------|:-------------------------------------|
| \[[Top](#Top "Cover (top) of document")\] | \[[Contents](#SEC_Contents "Table of contents")\] | \[[Index](#Concept-Index "Index")\] | \[ [?](#SEC_About "About (help)") \] |

# About This Document

This document was generated on *March 24, 2021* using [*texi2html
5.0*](http://www.nongnu.org/texi2html/).

The buttons in the navigation panels have the following meaning:

|    Button    |    Name     | Go to                                         | From 1.2.3 go to |
|:------------:|:-----------:|-----------------------------------------------|------------------|
|  \[ \<\< \]  |  FastBack   | Beginning of this chapter or previous chapter | 1                |
|   \[ \< \]   |    Back     | Previous section in reading order             | 1.2.2            |
|   \[ Up \]   |     Up      | Up section                                    | 1.2              |
|   \[ \> \]   |   Forward   | Next section in reading order                 | 1.2.4            |
|  \[ \>\> \]  | FastForward | Next chapter                                  | 2                |
|   \[Top\]    |     Top     | Cover (top) of document                       |                  |
| \[Contents\] |  Contents   | Table of contents                             |                  |
|  \[Index\]   |    Index    | Index                                         |                  |
|   \[ ? \]    |    About    | About (help)                                  |                  |

where the **Example** assumes that the current position is at
**Subsubsection One-Two-Three** of a document of the following
structure:

-   1\. Section One
    -   1.1 Subsection One-One
        -   ...
    -   1.2 Subsection One-Two
        -   1.2.1 Subsubsection One-Two-One
        -   1.2.2 Subsubsection One-Two-Two
        -   1.2.3 Subsubsection One-Two-Three     **\<== Current
            Position**
        -   1.2.4 Subsubsection One-Two-Four
    -   1.3 Subsection One-Three
        -   ...
    -   1.4 Subsection One-Four

------------------------------------------------------------------------

This document was generated on *March 24, 2021* using [*texi2html
5.0*](http://www.nongnu.org/texi2html/).  
