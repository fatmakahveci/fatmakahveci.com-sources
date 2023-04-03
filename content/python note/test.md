---
title: Text
description: Text
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
## Tests

### 1. Unit testing

- It checks that a small piece of code, like a function or class, is expected in isolation from the rest of the system.
- It could break during refactoring or an implementation change.

#### What makes a good unit test?

1. It should clearly explain what behaviour they're testing.
2. It should cover all use cases/edge cases for each public function.
3. It should test all public-facing functions and avoid testing private functions. (_<function_name> naming for private functions)
4. It should contain as little logic as possible.
5. It should not test code outside the scope of the test.

### 2. Integration testing

- It checks that the different pieces of code work together, maybe several classes, or a subsystem.

### 3. System (end-to-end) testing

- It checks all of the systems under test in an environment as close to the end-user environment as possible.

### 4. Functional testing

- It checks a single bit of functionality of a system.
- It should only break if we are intentionally changing the functionality of the system.

### 5. Subcutaneous testing

- It tests against an interface just below the surface.

---

## Naming conventions

- Test files should be named `test_<something>.py` or `<something>_test.py`.
• Test methods and functions should be named `test_<something>`.
• Test classes should be named `Test<Something>`.

---

## Output for the run

- `.` := passed test function or method
- `F`:= failures
- `E`:= errors
- `s`:= skips
- `x` := xfails
- `X`:= xpasses

## Testing parameters

`pip install pytest`

- It will look for tests in the current directory and subdirectories. It looks for files starting with `test_` or ending with `_test`. Also, you can specify the python test files or directories.

`pytest <test_name.py>`

`pytest -v <test_name.py>::<test_<function>>` # runs only one test

`pytest --collect-only` # like dryrun

`pytest -k "<key>"` # lets you use an expression to find what test functions to run

## It also can run a set of tests that have a common prefix or suffix in their names

`pytest -k "asdict or defaults" --collect-only` # , where asdict and defaults are the words in the function's name

`pytest -v -m "<mark1> or/and/and not <mark2>"` # `-m <mark>` marks a subset of your test functions so that they can be run together.

`pytest -l <test_name.py>` # If you use the -l/--showlocals option, local variables and their values are displayed
with tracebacks for failing tests.

`pytest -x` # exits when it encounters the first fail.

`pytest --maxfail=<number_of_fails>` # `--maxfail <number_of_fails>` stops after `<number_of_fails>`

`pytest --lf` # last failed

`pytest --ff` # first failed

`pytest -v` # verbose

`pytest -q` # quiet

`pytest -r <chars>` # show extra test summary info as specified by chars (f)ailed, (E)error, (s)skipped, (x)failed, (X)passed, (p)passed, (P)passed with output, (a)all except pP.

## assert

- `assert` to detect errors and debug easier.
  - If the condition is `True`, it continues to run.
  - Else, an `AssertionError` exception is raised with an optional error message.

- An assert is no mechanism for handling runtime errors.

- Asserts can be globally disabled with an interpreter setting.

- **Syntax**

`assert <expr1> ["," <expr2>]`, where `<expr1>` is the condition we test, and the optional `<expr2>` is an error message that's displayed if the assertion fails.

```python
""" assert_stmt ::= "assert" expression1 ["," expression2]`
"""

if not expression1:
  raise AssertionError(expression2)
```

1. **Do not use asserts for data validation:** Validate with regular if-statements and raise validation exceptions if necessary.

2. **Asserts that never fail:** `assert (counter == 10, 'It should have counted all the items')`

- Helper functions to make test assertions:
  - assertEqual
  - assertTrue
  - assertFalse, etc.

```python
def apply_discount( product, discount ):
  price = int(product['price'] * (1.0 - discount))
  assert 0 <= price <= product['price']
  return price

shoes = {'name': 'Fancy Shoes', 'price':14900}
apply_discount(product=shoes, discount=2.0)
```

### pytest

`assert something`
`assert a == b`
`assert a <= b`

### unittest

`assertTrue(something)`
`assertEqual(a, b)`
`assertLessEqual(a, b)`

## Built-in fixtures

### Using tmpdir and tmpdir_factory

- They create a temporary file system directory before your test runs and remove the directory when your test is finished.

#### 1. tmpdir

- If you’re testing something that reads, writes, or modifies files, you can use `tmpdir` to create files or directories used by a single test.
- It has a function scope.
- Any individual test that needs a temporary directory or file just for the single test can use `tmpdir`.

#### 2. tmpdir_factory

- You can use `tmpdir_factory` when you want to set up a directory for many tests.
- It has a session scope.
- For fixtures with a scope other than function (class, module, session).

## @pytest.fixture

- A test fixture is an environment used to consistently test a piece of software.
- It sets up a system for the software testing process by initializing it, thereby satisfying any preconditions the system may have.
- For each fixture used by a test function there is typically a parameter (named after the fixture) in the test function's definition.

### Parameters

- `Parameter`s are different from `function argument`s.
  - They can be passed as a list to the argument `params` of `@pytest.fixture()` decorator.
  - They must be iterables, such as generators, lists, tuples, sets, etc.
  - Pytest consumes such iterables and converts them into a list.
  - To use parameters, a fixture must consume a special fixture named `request`.
  - `request` contains `request.param` which contains one element from `params`.
  - The fixture is called as many times as the number of elements in the iterable of `params` argument, and the test function is called with values of fixtures the same number of times.

- `autouse` indicates that all tests in this file will use the fixture.
  - The code **before** `yield` runs before each test.
  - `yield` can return data to the test if desired.
  - The code **after** `yield` runs after each test.

- `tmpdir`

#### Setup

##### 1. In-line setup

- It leads to duplication when multiple tests require the same initial data.

##### 2. Delegate setup

- It places the test fixture in a separate standalone helper method that is accessed by multiple test methods.

##### 3. Implicit setup

- It places the test fixture in a setup method which is used to set up multiple test methods.
- Each test method has its setup procedures and links to an external test fixture.

## Marking test functions

- Marked tests from different files can all run together.
- A test can have more than one marker.
- A marker can be on multiple tests.

## Mocking

- As code grows eventually, you will need to start adding mocks to your test suite.

### `unittest.mock`

- It is Python's mock object library. (`pip install mock`)
- A _mock object_ (from the class `Mock`) substitutes and imitates a real object within a testing environment.
- `patch()` replaces the real objects in your code with `Mock` objects.
  - It can be used as either a context manager or a decorator.
- When you substitute an object in your code, the Mock must look like the real object it is replacing. Otherwise, your code will not be able to use the Mock in place of the original object.

```python
from unittest.mock import Mock

# If you are mocking the json library and your program
# calls dumps(), then your Python mock object must
# also contain dumps().
json = Mock() # patch the json library
json.dumps()

# do_something(mock) # pass mock as an argument to do_something()
```

## Parametrized testing

- A test function can turn into many test cases by running it multiple times with different test data.

## `pytest.ini`

- It is optional.
- It contains a project-wide pytest configuration.
- There should be at most only one in your project.
- It can contain directives that change the behaviour of pytest, such as setting up a list of options that will always be used.

## Running a subset of tests

- An expression can be used to match test names.

### A single directory

`pytest <dir> --tb=no`

### A single test file/module

`pytest <dir>/<test_file_name>.py`

### A single test function

`pytest <dir>/<test_file_name>.py::<function_name>`

### A single test class

- Test classes are a way to group tests that make sense to be grouped.

`pytest <dir>/<test_file_name>.py::<ClassName>`

### A single test method of a test class

- If you don't want to run all of a test class, just one method.

`pytest <dir>/<test_file_name>.py::<ClassName>::<function_name>`

### A set of tests based on the test name

- `k` parameter enables you to pass in an expression to run tests that have certain names specified by the expression as a substring of the test name.

`pytest -k <keyword>`
`pytest -k <keyword> and/or/and not/or not <keyword>`

## Skipping Tests

### Markers

- The `skip` and `skipif` markers enable you to skip tests that you don't want to run.

#### 1. `skip`

#### 2. `skipif`

#### 3. `xfail`
