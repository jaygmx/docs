---
title:  "tty"
linkTitle::  "tty"
weight: 100
description: >-
     tty
---

# ‘tty’: Print file name of terminal on standard input

‘tty’ prints the file name of the terminal connected to its standard
input. It prints ‘not a tty’ if standard input is not a terminal.
Synopsis:

``` 
 tty [OPTION]...
```

The program accepts the following option. Also see \*note Common
options::.

‘-s’ ‘--silent’ ‘--quiet’ Print nothing; only return an exit status.

Exit status:

``` 
 0 if standard input is a terminal
 1 if standard input is a non-terminal file
 2 if given incorrect arguments
 3 if a write error occurs
```
