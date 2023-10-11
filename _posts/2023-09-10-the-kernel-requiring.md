---
title:      "the kernel requiring"
date:       2023-09-10T12:36:06-04:00
tags:       ["files", "ruby"]
identifier: "20230910T123606"
---

`Kernel#require` loads a ruby feature. It returns true if the file
was successfully loaded or false if it could not be loaded.

It searches through the file system in many ways. If the filename is
not an absolute path and does not start with the relative directory
operators `./` or `../`, the file is searched for in the library
directories listed in $LOAD_PATH (`$:`).

If the file extension is `*.rb` it's loaded as a source file,
otherwise, it's loaded as a so-called ruby extension.

The absolute path of the loaded feature is added to $LOADED_FEATURES
(`$"`). A feature will not be loaded if it's already in `$"`.

Any constants or globals within the loaded source file will be available
in the calling program's global namespace
