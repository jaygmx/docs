---
title:  "arch"
linkTitle::  "arch"
weight: 100
description: >-
     arch
---

# ‘arch’: Print machine hardware name

‘arch’ prints the machine hardware name, and is equivalent to ‘uname
-m’.
Synopsis:

```bash
 arch [OPTION]
```

The program accepts the \*note Common options:: only.

‘arch’ is not installed by default, so portable scripts should not rely
on its existence.

An exit status of zero indicates success, and a nonzero value indicates
failure.
