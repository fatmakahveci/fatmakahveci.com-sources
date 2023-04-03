---
title: Exceptions
description: Exceptions
summary: "Updated by Fatma, Mar 28, 2023."
date: 28-03-2023
categories:
  - "Coding"
tags:
  - "Python"
  - "coding"
  - "algorithms"
  - "data structures"
---

- Exceptions are errors detected during execution.
- They are objects that are raised (or thrown) by code that encounters an unexpected circumstance.
- Most exceptions are not handled by programs.
- The last line of the error message indicates what happened.
- All exceptions must be instances of a class that derives from `BaseException`. `try-except` handles any exception classes derived from that class.

BaseException

 +-- `SystemExit` is raised by `sys.exit()`.
 +-- `KeyboardInterrupt` is raised when the user hits the interrupt key (normally ctrl+c or del). During execution, a check for interrupts is made regularly.
 +-- `GeneratorExit` is raised when a generator or coroutine is closed.
 +-- Exception
  +-- `StopIteration` is raised by next() and iterator's __next__() to signal there are no further items produced by the iterator.
      +-- `StopAsyncIteration` is raised by __anext__() method of an asynchronous iterator object to stop the iteration.
      +-- `ArithmeticError`
      |    +-- `FloatingPointError` is not used currently.
      |    +-- `OverflowError` is raised when the result of an arithmetic operation is too large to be represented.
      |    +-- `ZeroDivisionError` is raised when the second argument of a division or modulo operation is zero.
      +-- `AssertionError` is raised when an assert statement fails.
      +-- `AttributeError` is raised when an attribute reference or assignment fails.
      +-- `BufferError` is raised when a buffer-related operation cannot be performed.
      +-- `EOFError` is raised when the input() function hits an EOF condition without reading any data.
      +-- `ImportError` is raised when the import statement has trouble trying to load a module.
      |    +-- `ModuleNotFoundError` is raised when a module could not be located.
      +-- `LookupError` is raised when a key or index used on a mapping or sequence is invalid.
      |    +-- `IndexError` is raised when a sequence subscript is out of range.
      |    +-- `KeyError` is raised when a mapping key is not found in the set of existing keys.
      +-- `MemoryError` is raised when an operation runs out of memory.
      +-- `NameError` is raised when a local or global name is not found.
      |    +-- `UnboundLocalError` is raised when a reference is made to a local variable in a function or method, but no value has been bound to that variable.
      +-- `OSError` is raised when a system function returns a system-related error.
      |    +-- `BlockingIOError` is raised when an operation would block an object set for a non-blocking operation.
      |    +-- `ChildProcessError` is raised when an operation on a child process failed.
      |    +-- `ConnectionError`
      |    |    +-- `BrokenPipeError` is raised when trying to write on a pipe while the other end has been closed, or trying to write on a socket which has been shut down for writing.
      |    |    +-- `ConnectionAbortedError` is raised when a connection attempt is aborted by the peer.
      |    |    +-- `ConnectionRefusedError` is raised when a connection attempt is refused by the peer.
      |    |    +-- `ConnectionResetError` is raised when a connection is reset by the peer.
      |    +-- `FileExistsError` is raised when trying to create a file or directory which already exists.
      |    +-- `FileNotFoundError` is raised when a file or directory is requested but doesn't exist.
      |    +-- `InterruptedError` is raised when a system call is interrupted by an incoming signal.
      |    +-- `IsADirectoryError` is raised when a file operation is requested on a directory.
      |    +-- `NotADirectoryError` is raised when a directory operation is requested on something which is not a directory.
      |    +-- `PermissionError` is raised when trying to run an operation without adequate access rights.
      |    +-- `ProcessLookupError` is raised when a given process doesn't exist.
      |    +-- `TimeoutError` is raised when a system function timed out at the system level.
      +-- `ReferenceError` is raised when a weak reference proxy is used to access an attribute of the referent after it has been garbage collected.
      +-- `RuntimeError` is raised when an error is detected that doesn't fall in any of the other categories.
      |    +-- `NotImplementedError` should be raised in user-defined base classes by abstract methods when they require derived classes to override the method, or while the class is being developed to indicate that the real implementation still needs to be added.
      |    +-- `RecursionError` is raised when the interpreter detects the maximum recursion depth.
      +-- `SyntaxError` is raised when the parser encounters a syntax error.
      |    +-- `IndentationError` is raised for incorrect indentation.
      |         +-- `TabError` is raised for inconsistent use of tabs and spaces.
      +-- `SystemError` is raised when the interpreter finds an internal error, but the situation doesn't look so serious to cause it to abandon all hope.
      +-- `TypeError` is raised when an operation or function is applied to an object of an inappropriate type.
      +-- `ValueError` is raised when an operation or function receives an argument that has the right type but an inappropriate value.
      |    +-- `UnicodeError` is raised when a Unicode-related encoding or decoding error occurs.
      |         +-- `UnicodeDecodeError` is raised when a Unicode-related error occurs during decoding.
      |         +-- `UnicodeEncodeError` is raised when a Unicode-related error occurs during encoding.
      |         +-- `UnicodeTranslateError` is raised when a Unicode-related error occurs during translating.
      +-- `Warning`
           +-- `DeprecationWarning`
           +-- `PendingDeprecationWarning`
           +-- `RuntimeWarning`
           +-- `SyntaxWarning`
           +-- `UserWarning`
           +-- `FutureWarning`
           +-- `ImportWarning`
           +-- `UnicodeWarning`
           +-- `BytesWarning`
           +-- `ResourceWarning`

[Ref 1](https://realpython.com/python-exceptions/), [Ref 2](https://docs.python.org/3/library/exceptions.html), [Ref 3](https://docs.python.org/3/tutorial/errors.html)

---

## Exception handling

- If an exception occurs which does not match the exception named in the except clause, it is passed on to outer try statements; if no handler is found, it is an unhandled exception and execution stops with a message.

- A try statement may have more than one except clause to specify handlers for different exceptions.
  - i.e.,
    - except OSError as err:
    - except (RuntimeError, TypeError, NameError):

- `except:` may omit the exception name to serve as a wildcard.

- `else` is optional for try...except statement.
    try:
        ...
        except OSError:
        ...
    else:

[Ref](https://docs.python.org/3/tutorial/errors.html#tut-userexceptions)

---

## Exception chaining

```python
try:
  ...
except IOerror as exc:
  raise RuntimeError('...') from exc
```

[Ref](https://docs.python.org/3/tutorial/errors.html#tut-userexceptions)

---

## Raising exceptions

- It allows us to force a specified exception to occur.
- i.e., raise NameError('HiThere')

[Ref](https://docs.python.org/3/tutorial/errors.html#tut-userexceptions)

---

## User-defined exceptions

- Exceptions should typically be derived from the Exception class.

[Ref](https://docs.python.org/3/tutorial/errors.html#tut-userexceptions)

---

## Broken Pipe Error

- A subclass of ConnectionError, raised when trying to write on a pipe while the other end has been closed, or trying to write on a socket which has been shut down for writing.

---

## Errors

There are (at least) two distinguishable kinds of errors:

  1. Syntax errors
  2. Exceptions

[Ref1: colorful terminal](https://github.com/onelivesleft/PrettyErrors), [Ref2](https://docs.python.org/3/tutorial/errors.html#tut-userexceptions)

---

## Syntax errors

- a.k.a. parsing errors
- File name and line number are printed so you know where to look in case the input came from a script.

---
