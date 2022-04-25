---
title:  "chmod"
linkTitle::  "chmod"
weight: 100
description: >-
     chmod
---

# ‘chmod’: Change access permissions

‘chmod’ changes the access permissions of the named files.
Synopsis:

``` 
 chmod [OPTION]... {MODE | --reference=REF_FILE} FILE...
```

‘chmod’ never changes the permissions of symbolic links, since the
‘chmod’ system call cannot change their permissions. This is not a
problem since the permissions of symbolic links are never used. However,
for each symbolic link listed on the command line, ‘chmod’ changes the
permissions of the pointed-to file. In contrast, ‘chmod’ ignores
symbolic links encountered during recursive directory traversals.

Only a process whose effective user ID matches the user ID of the file,
or a process with appropriate privileges, is permitted to change the
file mode bits of a file.

A successful use of ‘chmod’ clears the set-group-ID bit of a regular
file if the file’s group ID does not match the user’s effective group ID
or one of the user’s supplementary group IDs, unless the user has
appropriate privileges. Additional restrictions may cause the
set-user-ID and set-group-ID bits of MODE or REF\_FILE to be ignored.
This behavior depends on the policy and functionality of the underlying
‘chmod’ system call. When in doubt, check the underlying system
behavior.

If used, MODE specifies the new file mode bits. For details, see the
section on \*note File permissions::. If you really want MODE to have a
leading ‘-’, you should use ‘--’ first, e.g., ‘chmod -- -w file’.
Typically, though, ‘chmod a-w file’ is preferable, and ‘chmod -w file’
(without the ‘--’) complains if it behaves differently from what ‘chmod
a-w file’ would do.

The program accepts the following options. Also see \*note Common
options::.

‘-c’ ‘--changes’ Verbosely describe the action for each FILE whose
permissions actually changes.

‘-f’ ‘--silent’ ‘--quiet’ Do not print error messages about files whose
permissions cannot be changed.

‘--preserve-root’ Fail upon any attempt to recursively change the root
directory, ‘/’. Without ‘--recursive’, this option has no effect. \*Note
Treating / specially::.

‘--no-preserve-root’ Cancel the effect of any preceding
‘--preserve-root’ option. \*Note Treating / specially::.

‘-v’ ‘--verbose’ Verbosely describe the action or non-action taken for
every FILE.

‘--reference=REF\_FILE’ Change the mode of each FILE to be the same as
that of REF\_FILE. \*Note File permissions::. If REF\_FILE is a symbolic
link, do not use the mode of the symbolic link, but rather that of the
file it refers to.

‘-R’ ‘--recursive’ Recursively change permissions of directories and
their contents.

An exit status of zero indicates success, and a nonzero value indicates
failure.
