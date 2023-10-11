---
title:      "ruby predefined global variables"
date:       2023-09-14T19:05:19-04:00
tags:       ["ruby"]
identifier: "20230914T190519"
---

Here is a list of some commonly-used predefined global variables in
Ruby:

1. **`$!`**: Last exception object raised.
2. **`$@`**: Backtrace of the last exception.
3. **`$_`**: The string most recently read by `gets` or `readline` in the current scope.
4. **`$.`**: The line number of the last line read by the interpreter.
5. **`$&`**: The entire matched string for the last successful pattern match.
6. **`$~`**: The equivalent of `$~` is a special variable that holds the `MatchData` object of the last regular expression match.
7. **`$1`, `$2`, ...**: These contain text matching the first, second, etc., parenthetical groups of the last regular expression match.
8. **`$+`**: Contains the last parenthetical match.
9. **`$*`**: Command line arguments given for the script. Deprecated in Ruby 1.9.
10. **`$$`**: The process number of the Ruby running this script.
11. **`$?`**: The status of the last executed child process.
12. **`$:` or `$LOAD_PATH`**: An array of locations to look for Ruby scripts and binary extensions when using `require`.
13. **`$" or $LOADED_FEATURES`**: An array of the module names loaded by `require`.
14. **`$0`**: Contains the name of the script being executed.
15. **`$stdin`**: The current standard input.
16. **`$stdout`**: The current standard output. **STDOUT** is a
    constant representing standard output.
17. **`$stderr`**: The current standard error output.
18. **`$;` or `$-F`**: The default separator pattern used by `String#split`.
19. **`$,`**: The output field separator for the `print` and `IO#write`.
20. **`$/` or `$-0`**: The input record separator (`\n` by default).
21. **`$\`**: The output record separator for the `print` and `IO#write`.
22. **`$<`**: An object that provides access to the concatenation of the contents of all the files listed as command-line arguments.
23. **`$>`**: The default output for `print`, `printf`, and `write`.
24. **`$SAFE`**: The thread-local safe level, which enables tainting checks and restricts eval and system calls.

Please note that the use of some of these predefined global variables
is considered unidiomatic or outdated in modern Ruby, but they are
still available for use. Always be cautious when using global
variables, as they can make code harder to understand and maintain. 
