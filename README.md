# getopt

Portable, complete and bug-free impementation of `getopt(3)`, `getopt_long(3)`,
`getopt_long_only(3)` and `getsubopt(3)`. Written from scratch and 100% compatible with
GNU (glibc) implementation.

### Why

There are many other implementations floating around. But they usually fall into three
categories:

1. Big libc or POSIX library hard to adapt into your code.
2. Incomplete implementation with only subset of features and some obscure
   incompatibilities.
3. Both of above.

So my aim is to provide feature-complete, bug-free and easy to use `getopt(3)` and
`getopt_long(3)`.

### Features

- all POSIX features and extras, including argument permutation, `optreset`, `optind=0`,
  `:`, `-`, `+`, `W;`, `POSIXLY_CORRECT`, etc.
- passes all compatibility tests I know of
- compact C99 code compiles with different compilers/OS (Windows included)
- No run-time dependencies, only `fprintf` and `getenv` required and both can be
  eliminated by compile-time definitions
- usable either as drop-in replacement of system implementation or "prefixed" user
  library
- few optional compile-time adjustments to ease integration with your code

### Using

- Simply link with `getopt.c`
- If specific prefix needs to be added (e.g., `foobar_getopt()`) then do `#define
  GETOPT_PREFIX foobar_` before compiling `getopt.c` and before including `getopt.h` in
  your source code

### Adjust in compile-time

This is fully optional. The following symbols can be defined while compiling `getopt.c`:

- `POSIXLY_CORRECT`: force POSIX compatibility in regard to argument permutation
    - `#undef POSIXLY_CORRECT`  -- check environment variable first (like glibc); this is
      the default
    - `#define POSIXLY_CORRECT 0` -- ignore the environment and allow argument
      permutation, except when leading `+` is found in option string
    - `#define POSIXLY_CORRECT 1` (or simply `#define POSIXLY_CORRECT`) -- never permute
      arguments (leading `-` in option string still works)
- `GETOPT_PRINT`: set to varargs function to output error messages; default is
  `fprintf(stderr, __VA_ARGS__)`
