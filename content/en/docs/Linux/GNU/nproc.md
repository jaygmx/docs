---
title:  "nproc"
linkTitle::  "nproc"
weight: 100
description: >-
     nproc
---

# ‘nproc’: Print the number of available processors

Print the number of processing units available to the current process,
which may be less than the number of online processors. If this
information is not accessible, then print the number of processors
installed. If the ‘OMP\_NUM\_THREADS’ or ‘OMP\_THREAD\_LIMIT’
environment variables are set, then they will determine the minimum and
maximum returned value respectively. The result is guaranteed to be
greater than zero.
Synopsis:

``` 
 nproc [OPTION]
```

The program accepts the following options. Also see \*note Common
options::.

‘--all’ Print the number of installed processors on the system, which
may be greater than the number online or available to the current
process. The ‘OMP\_NUM\_THREADS’ or ‘OMP\_THREAD\_LIMIT’ environment
variables are not honored in this case.

‘--ignore=NUMBER’ If possible, exclude this NUMBER of processing units.

An exit status of zero indicates success, and a nonzero value indicates
failure.
