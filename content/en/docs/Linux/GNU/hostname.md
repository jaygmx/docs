---
title:  "hostname"
linkTitle::  "hostname"
weight: 100
description: >-
     hostname
---

# ‘hostname’: Print or set system name

With no arguments, ‘hostname’ prints the name of the current host
system. With one argument, it sets the current host name to the
specified string. You must have appropriate privileges to set the host
name.
Synopsis:

``` 
 hostname [NAME]
```

The only options are ‘--help’ and ‘--version’. \*Note Common options::.

‘hostname’ is not installed by default, and other packages also supply a
‘hostname’ command, so portable scripts should not rely on its existence
or on the exact behavior documented above.

An exit status of zero indicates success, and a nonzero value indicates
failure.
