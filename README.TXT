xassert is a set of C/C++ custom assertion macros. To use them, include stdlib.h
or cstdlib followed by xassert.h and call ASSERT, DASSERT, XASSERT or
set_assert_handler from your code.

ASSERT takes one argument and is a macro that will always check the expression
passed to it. If the expression evaluates to false, it will run the assertion
handler. If the assertion handler returns true, it will halt the program by
calling abort(3).

DASSERT is a macro that does the same except that it will be a no-op if NDEBUG
is defined, like standard assert(3). The assert expression will only be
evaluated in debug environments.

XASSERT is a macro similar to ASSERT but it takes an extra argument that should
be a diagnostic message to be printed when the assertion fails.

set_assert_handler() is a function that allows users to pick their own assertion
handler different from the default provided one. Assertion handlers should
conform to the following prototype:

int (*f)(const char *expr, const char *file, int line, const char *msg);

expr is the expression to be asserted. file and line are the file name and line
number where the assertion is being checked, respectively. msg is a string with
a diagnostic message, which may be the null pointer.

The default assertion handler will print the expression, line number, file name
and optional diagnostic message to standard error and return true so the program
is aborted. The value returned from set_assert_handler() is the old assertion
handler function in case it needs to be restored.

set_assert_handler() is NOT reentrant.

All this code is released to the public domain under the terms of the CC0
license. Please, see the COPYING.TXT file for more details.
