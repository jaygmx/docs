---
title:  "false"
linkTitle::  "false"
weight: 100
description: >-
     false
---

# ‘false’: Do nothing, unsuccessfully

‘false’ does nothing except return an exit status of 1, meaning
“failure”. It can be used as a place holder in shell scripts where
an unsuccessful command is needed. In most modern shells, ‘false’ is a
built-in command, so when you use ‘false’ in a script, you’re probably
using the built-in command, not the one documented here.

‘false’ honors the ‘--help’ and ‘--version’ options.

This version of ‘false’ is implemented as a C program, and is thus more
secure and faster than a shell script implementation, and may safely be
used as a dummy shell for the purpose of disabling accounts.

Note that ‘false’ (unlike all other programs documented herein) exits
unsuccessfully, even when invoked with ‘--help’ or ‘--version’.

Portable programs should not assume that the exit status of ‘false’ is
1, as it is greater than 1 on some non-GNU hosts.
