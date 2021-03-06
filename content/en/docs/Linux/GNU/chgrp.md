---
title:  "chgrp"
linkTitle::  "chgrp"
weight: 100
description: >-
     chgrp
---

# ‘chgrp’: Change group ownership

‘chgrp’ changes the group ownership of each given FILE to GROUP (which
can be either a group name or a numeric group ID) or to the group of an
existing reference file. \*Note chown invocation::.
Synopsis:

``` 
 chgrp [OPTION]... {GROUP | --reference=REF_FILE} FILE...
```

If GROUP is intended to represent a numeric group ID, then you may
specify it with a leading ‘+’. \*Note Disambiguating names and IDs::.

It is system dependent whether a user can change the group to an
arbitrary one, or the more portable behavior of being restricted to
setting a group of which the user is a member.

The program accepts the following options. Also see \*note Common
options::.

‘-c’ ‘--changes’ Verbosely describe the action for each FILE whose group
actually changes.

‘-f’ ‘--silent’ ‘--quiet’ Do not print error messages about files whose
group cannot be changed.

‘--dereference’ Do not act on symbolic links themselves but rather on
what they point to. This is the default when not operating recursively.

``` 
 Combining this dereferencing option with the ‘--recursive’ option
 may create a security risk: During the traversal of the directory
 tree, an attacker may be able to introduce a symlink to an
 arbitrary target; when the tool reaches that, the operation will be
 performed on the target of that symlink, possibly allowing the
 attacker to escalate privileges.
```

‘-h’ ‘--no-dereference’ Act on symbolic links themselves instead of what
they point to. This mode relies on the ‘lchown’ system call. On systems
that do not provide the ‘lchown’ system call, ‘chgrp’ fails when a file
specified on the command line is a symbolic link. By default, no
diagnostic is issued for symbolic links encountered during a recursive
traversal, but see ‘--verbose’.

‘--preserve-root’ Fail upon any attempt to recursively change the root
directory, ‘/’. Without ‘--recursive’, this option has no effect. \*Note
Treating / specially::.

‘--no-preserve-root’ Cancel the effect of any preceding
‘--preserve-root’ option. \*Note Treating / specially::.

‘--reference=REF\_FILE’ Change the group of each FILE to be the same as
that of REF\_FILE. If REF\_FILE is a symbolic link, do not use the group
of the symbolic link, but rather that of the file it refers to.

‘-v’ ‘--verbose’ Output a diagnostic for every file processed. If a
symbolic link is encountered during a recursive traversal on a system
without the ‘lchown’ system call, and ‘--no-dereference’ is in effect,
then issue a diagnostic saying neither the symbolic link nor its
referent is being changed.

‘-R’ ‘--recursive’ Recursively change the group ownership of directories
and their contents.

‘-H’ If ‘--recursive’ (‘-R’) is specified and a command line argument is
a symbolic link to a directory, traverse it. \*Note Traversing
symlinks::.

‘-L’ In a recursive traversal, traverse every symbolic link to a
directory that is encountered.

``` 
 Combining this dereferencing option with the ‘--recursive’ option
 may create a security risk: During the traversal of the directory
 tree, an attacker may be able to introduce a symlink to an
 arbitrary target; when the tool reaches that, the operation will be
 performed on the target of that symlink, possibly allowing the
 attacker to escalate privileges.

 *Note Traversing symlinks::.
```

‘-P’ Do not traverse any symbolic links. This is the default if none of
‘-H’, ‘-L’, or ‘-P’ is specified. \*Note Traversing symlinks::.

An exit status of zero indicates success, and a nonzero value indicates
failure.

Examples:

``` 
 # Change the group of /u to "staff".
 chgrp staff /u

 # Change the group of /u and subfiles to "staff".
 chgrp -hR staff /u
```
