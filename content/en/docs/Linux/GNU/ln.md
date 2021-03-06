---
title:  "ln"
linkTitle::  "ln"
weight: 100
description: >-
     ln
---

# ‘ln’: Make links between files

‘ln’ makes links between files. By default, it makes hard links; with
the ‘-s’ option, it makes symbolic (or “soft”) links. Synopses:

``` 
 ln [OPTION]... [-T] TARGET LINKNAME
 ln [OPTION]... TARGET
 ln [OPTION]... TARGET... DIRECTORY
 ln [OPTION]... -t DIRECTORY TARGET...
```

• If two file names are given, ‘ln’ creates a link to the first file
from the second.

• If one TARGET is given, ‘ln’ creates a link to that file in the
current directory.

• If the ‘--target-directory’ (‘-t’) option is given, or failing that if
the last file is a directory and the ‘--no-target-directory’ (‘-T’)
option is not given, ‘ln’ creates a link to each TARGET file in the
specified directory, using the TARGETs’ names.

Normally ‘ln’ does not replace existing files. Use the ‘--force’ (‘-f’)
option to replace them unconditionally, the ‘--interactive’ (‘-i’)
option to replace them conditionally, and the ‘--backup’ (‘-b’) option
to rename them. Unless the ‘--backup’ (‘-b’) option is used there is no
brief moment when the destination does not exist; this is an extension
to POSIX.

A “hard link” is another name for an existing file; the link and the
original are indistinguishable. Technically speaking, they share the
same inode, and the inode contains all the information about a
file—indeed, it is not incorrect to say that the inode *is* the file.
Most systems prohibit making a hard link to a directory; on those where
it is allowed, only the super-user can do so (and with caution, since
creating a cycle will cause problems to many other utilities). Hard
links cannot cross file system boundaries. (These restrictions are not
mandated by POSIX, however.)

“Symbolic links” (“symlinks” for short), on the other hand, are a
special file type (which not all kernels support: System V release 3
(and older) systems lack symlinks) in which the link file actually
refers to a different file, by name. When most operations (opening,
reading, writing, and so on) are passed the symbolic link file, the
kernel automatically “dereferences” the link and operates on the target
of the link. But some operations (e.g., removing) work on the link file
itself, rather than on its target. The owner and group of a symlink are
not significant to file access performed through the link, but do have
implications on deleting a symbolic link from a directory with the
restricted deletion bit set. On the GNU system, the mode of a symlink
has no significance and cannot be changed, but on some BSD systems, the
mode can be changed and will affect whether the symlink will be
traversed in file name resolution. \*Note (libc)Symbolic Links::.

Symbolic links can contain arbitrary strings; a “dangling symlink”
occurs when the string in the symlink does not resolve to a file. There
are no restrictions against creating dangling symbolic links. There are
trade-offs to using absolute or relative symlinks. An absolute symlink
always points to the same file, even if the directory containing the
link is moved. However, if the symlink is visible from more than one
machine (such as on a networked file system), the file pointed to might
not always be the same. A relative symbolic link is resolved in relation
to the directory that contains the link, and is often useful in
referring to files on the same device without regards to what name that
device is mounted on when accessed via networked machines.

When creating a relative symlink in a different location than the
current directory, the resolution of the symlink will be different than
the resolution of the same string from the current directory. Therefore,
many users prefer to first change directories to the location where the
relative symlink will be created, so that tab-completion or other file
resolution will find the same target as what will be placed in the
symlink.

The program accepts the following options. Also see \*note Common
options::.

‘-b’ ‘--backup\[=METHOD\]’ \*Note Backup options::. Make a backup of
each file that would otherwise be overwritten or removed.

‘-d’ ‘-F’ ‘--directory’ Allow users with appropriate privileges to
attempt to make hard links to directories. However, note that this will
probably fail due to system restrictions, even for the super-user.

‘-f’ ‘--force’ Remove existing destination files.

‘-i’ ‘--interactive’ Prompt whether to remove existing destination
files.

‘-L’ ‘--logical’ If ‘-s’ is not in effect, and the source file is a
symbolic link, create the hard link to the file referred to by the
symbolic link, rather than the symbolic link itself.

‘-n’ ‘--no-dereference’ Do not treat the last operand specially when it
is a symbolic link to a directory. Instead, treat it as if it were a
normal file.

``` 
 When the destination is an actual directory (not a symlink to one),
 there is no ambiguity.  The link is created in that directory.  But
 when the specified destination is a symlink to a directory, there
 are two ways to treat the user’s request.  ‘ln’ can treat the
 destination just as it would a normal directory and create the link
 in it.  On the other hand, the destination can be viewed as a
 non-directory—as the symlink itself.  In that case, ‘ln’ must
 delete or backup that symlink before creating the new link.  The
 default is to treat a destination that is a symlink to a directory
 just like a directory.

 This option is weaker than the ‘--no-target-directory’ (‘-T’)
 option, so it has no effect if both options are given.
```

‘-P’ ‘--physical’ If ‘-s’ is not in effect, and the source file is a
symbolic link, create the hard link to the symbolic link itself. On
platforms where this is not supported by the kernel, this option creates
a symbolic link with identical contents; since symbolic link contents
cannot be edited, any file name resolution performed through either link
will be the same as if a hard link had been created.

‘-r’ ‘--relative’ Make symbolic links relative to the link location.

``` 
 Example:

      ln -srv /a/file /tmp
      '/tmp/file' -> '../a/file'

 Relative symbolic links are generated based on their canonicalized
 containing directory, and canonicalized targets.  I.e., all
 symbolic links in these file names will be resolved.  *Note
 realpath invocation::, which gives greater control over relative
 file name generation, as demonstrated in the following example:

      ln--relative() {
        test "$1" = --no-symlinks && { nosym=$1; shift; }
        target="$1";
        test -d "$2" && link="$2/." || link="$2"
        rtarget="$(realpath $nosym -m "$target" \
                    --relative-to "$(dirname "$link")")"
        ln -s -v "$rtarget" "$link"
      }
```

‘-s’ ‘--symbolic’ Make symbolic links instead of hard links. This option
merely produces an error message on systems that do not support symbolic
links.

‘-S SUFFIX’ ‘--suffix=SUFFIX’ Append SUFFIX to each backup file made
with ‘-b’. \*Note Backup options::.

‘-t DIRECTORY’ ‘--target-directory=DIRECTORY’ Specify the destination
DIRECTORY. \*Note Target directory::.

‘-T’ ‘--no-target-directory’ Do not treat the last operand specially
when it is a directory or a symbolic link to a directory. \*Note Target
directory::.

‘-v’ ‘--verbose’ Print the name of each file after linking it
successfully.

If ‘-L’ and ‘-P’ are both given, the last one takes precedence. If ‘-s’
is also given, ‘-L’ and ‘-P’ are silently ignored. If neither option is
given, then this implementation defaults to ‘-P’ if the system ‘link’
supports hard links to symbolic links (such as the GNU system), and ‘-L’
if ‘link’ follows symbolic links (such as on BSD).

An exit status of zero indicates success, and a nonzero value indicates
failure.

Examples:

``` 
 Bad Example:

 # Create link ../a pointing to a in that directory.
 # Not really useful because it points to itself.
 ln -s a ..

 Better Example:

 # Change to the target before creating symlinks to avoid being confused.
 cd ..
 ln -s adir/a .

 Bad Example:

 # Hard coded file names don't move well.
 ln -s $(pwd)/a /some/dir/

 Better Example:

 # Relative file names survive directory moves and also
 # work across networked file systems.
 ln -s afile anotherfile
 ln -s ../adir/afile yetanotherfile
```
