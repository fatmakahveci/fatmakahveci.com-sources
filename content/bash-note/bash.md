---
title: Bash for beginners
description: Bash for beginners
summary: "Updated by Fatma, Mar 28, 2023."
date: 28-03-2023
categories:
  - "Coding"
tags:
  - "bash"
  - "coding"
  - "algorithms"
  - "data structures"
comments: true
---
## basename

- It strips paths from filenames:
  - `$ >> basename <dir>/<file_name.ext>`
        % <file_name.ext>
- It can also strip a suffix (e.g., extension):
  - `$ >> basename -s <.ext> <dir>/<filename.ext>`
        % <file_name>

## Command-Line Arguments

`$ >> nano args.sh`

```bash
#!/bin/bash
echo "script name: $0"
echo "first arg: $1"
```

`$ >> bash args.sh arg1`
% script name: args.sh
% first arg: arg1

- You can define the number of args using `$#`. It does not count the script name, `$0` as an argument.

`$ >> nano args.sh`

```bash
#!/bin/bash 

if [ "$#" -lt 3 ] # are there less than 3 arguments? 
then
    echo "error: too few arguments, you provided $#, 3 required"
    echo "usage: script.sh arg1 arg2 arg3"
    exit 1
fi
echo "script name: $0"
echo "first arg: $1"
echo "second arg: $2"
echo "third arg: $3" '
```

`$ >> bash args.sh arg1 arg2`

% error: too few arguments, you provided 2, 3 required
% usage: script.sh arg1 arg2 arg3

[https://data-skills.github.io/unix-and-bash/03-bash-scripts/index.html](https://data-skills.github.io/unix-and-bash/03-bash-scripts/index.html)

## Conditionals

### if-else

```bash
#!/bin/bash
set -e
set -u
set -o pipefail

if [<command>] then
    [<if_statement>]
else
    [<else_statement>]
fi
```

### File and directory test expressions

| File/directory expression | Description        |
| ------------------------- | ------------------ |
| -d dir                    | dir is a directory |
| -f file                   | file is a file     |
| -e file                   | file exists        |
| -h link                   | link is a link     |
| -r file                   | file is readable   |
| -w file                   | file is writable   |
| -x file                   | file is executable |

```bash
#!/bin/bash
set -e
set -u
set -o pipefail

if [ -f <file_name> ]
then <if_statement>
fi

```

[https://data-skills.github.io/unix-and-bash/03-bash-scripts/index.html](https://data-skills.github.io/unix-and-bash/03-bash-scripts/index.html)

## Curly Braces in Bash

### Array Builder

- `{0..10}` := 0 1 2 3 4 5 6 7 8 9 10
- `{10..0}` := 10 9 8 7 6 5 4 3 2 1 0
- `{10..0..2}` := 10 8 6 4 2 0
- `{a..z}` := a b c d e f g h i j k l m n o p q r s t u v w x y z
- You can use these in your scripts:
  - i.e. `$ >> touch {1..3}.txt` creates _1.txt, 2.txt, 3.txt_ files.

[https://www.linux.com/topic/desktop/all-about-curly-braces-bash/](https://www.linux.com/topic/desktop/all-about-curly-braces-bash/)

## Exit Codes

- _0_ OK
- _1_ if minor problems (e.g., cannot access subdirectory)
- _2_ if serious trouble (e.g., cannot access command-line argument)

## File Descriptors

```text
| File            | C identifier | File descriptor | Defaults to           |
| --------------- | ------------ | --------------- | --------------------- |
| Standard input  | stdin        | 0               | data fed into program |
| Standard output | stdout       | 1               | terminal              |
| Standard error  | stderr       | 2               | terminal              |

stdin (0) -> program -> stdout (1)
                     -> stderr (2)
```

[https://medium.com/@codenameyau/step-by-step-breakdown-of-dev-null-a0f516f53158](https://medium.com/@codenameyau/step-by-step-breakdown-of-dev-null-a0f516f53158)

## Output

- `>/dev/null` redirects the command standard output to the null device that discards the information written to it.
- `2>&1` redirects the standard error stream (2) to the standard output stream (1). Note that this takes the standard error stream and points it to the same location as the standard output at that moment. This is the reason for the order >/some/where 2>&1 because one needs to first point stdout to somewhere and then point stderr to the same location if one wants to combine both streams in the end.
- To save errors to a file:
  - `$ >> <bash_command> 2> <error_file.txt>`
- To save output and error messages into the same file:
  - `$ >> <bash_command> > <output_file_name> 2>&1`

[https://askubuntu.com/questions/12098/what-does-outputting-to-dev-null-accomplish-in-bash-scripts](https://askubuntu.com/questions/12098/what-does-outputting-to-dev-null-accomplish-in-bash-scripts)

## A robust Bash header

```bash
#!/usr/bin/bash
    set -e # tells the script to terminate if any command exited with a nonzero exit status.
    set -u # tells the script not to run any command containing a reference to an unset variable name
    set -o pipefail # to cover one of the exceptions of `set -e`: if the last program terminates with a nonzero status, the pipe will not be terminated.
```

[https://data-skills.github.io/unix-and-bash/03-bash-scripts/index.html](https://data-skills.github.io/unix-and-bash/03-bash-scripts/index.html)

## shell

- UNIX provides different flavours of shells:
  - Bourne shell (sh)
  - C shell (csh)
  - TC shell (tcsh)
  - Korn shell (ksh)
  - Bourne Again shell (bash)
- `$ >> echo $SHELL` # prints the default shell.
- `$ >> echo $0` # prints the current shell.

## shuf

- `shuf --help` for detailed information.
- There are three ways to use the shuf command:

### 1. file shuf

- It generates random permutations from input lines to standard output.
- If given a file or series of files, it will shuffle the lines and write the result to standard output.
- `shuf <file_name>`
- Pick a random line(s) from a file `shuf -n <number_of_line(s)_to_be_selected> <file_name>`

### 2. list shuf

- `shuf -e <space_separated_list>`
- Pick a random element(s) from a list `shuf -n <number_of_element(s)_to_be_selected> -e <space_separated_list>`

### 3. range shuf

- `shuf -i <start_index>-<end_index>` # it shuffles the numbers between <start_index> <end_index>
- `shuf -i <start_index>-<end_index> -n <number_of_number(s)_to_be_selected>` # it picks <number_of_number(s)_to_be_selected> number(s) between <start_index> <end_index>

[https://shapeshed.com/unix-shuf/](https://shapeshed.com/unix-shuf/)

## Variables

- They don't have data types, but it is helpful to think as strings.

```bash
results_dir="<dir>"
echo ${results_dir}
```

[https://data-skills.github.io/unix-and-bash/03-bash-scripts/index.html](https://data-skills.github.io/unix-and-bash/03-bash-scripts/index.html)

## Writing Pipes

- A pipeline is a sequence of one or more commands separated by one of the control operators '|' or '|&'.
- If ‘|&’ is used, the command’s standard error, in addition to its standard output, is connected to the next command’s standard input through the pipe; it is shorthand for 2>&1 |.

[https://www.gnu.org/software/bash/manual/html_node/Pipelines.html](https://www.gnu.org/software/bash/manual/html_node/Pipelines.html)

## xargs

- It reads data from standard input (stdin) and __executes the command one or more times based on the input read.__
`$ >> xargs` # == `echo`.

### xargs with another command

- It is extremely useful when combined with other commands. e.g., _find_ and _grep_.
`$ >> xargs find . -name` # waits for the input until `Ctrl+D` tell xargs that we are done with the input.
- Any blanks and spaces in the input are treated as delimiters, while blank lines are ignored.

### Making xargs execute command multiple times

- `-L` parameter requires a number which it treats as the maximum line of non-blank lines that should be passed as input to the command at one time.
  - `$ >> xargs find . -name -L 1` # to give all inputs as a single line in a way that _find_ command accepts.
- `-n` parameter requires a number that would represent the number of arguments that you want xargs to pass per command line.

### Handling filenames with spaces

- `-d '<delimiter>'` changes the delimiter.

### Handling filenames with newline characters

- `$ >> find . -name "<wildcard>" -print0 | xargs -0 gedit`
- `print0` prints the full file name on the standard output. It allows file names that contain new lines.

### Finding files containing a specific text

- `$ >> find . -name "<wildcard>" | xargs grep "<searching_word>"`

### Accepting input from a file

- `-a` expects a file name.
- `$ >> xargs -a <input_file_name> ls -lart`

### Seeking user permission before executing a command

- `-p` asks for permission each time it runs the command.

[https://www.howtoforge.com/tutorial/linux-xargs-command/](https://www.howtoforge.com/tutorial/linux-xargs-command/)

## yarn

- MacOS installation: `brew install yarn`
- `yarn` is a more convenient, safer and faster package dependency manager that can be used instead of `npm` in `JS` projects.
- To use yarn in your current npm project, simply run yarn in your project directory.
- Switching to `yarn` by `npm` is easy because it works with the same `package.json` format.
- When you run the `yarn add <package name>` code to install packages in the project directory, it will create the `yarn.lock` file in the project directory.
- `yarn create <pkg_name> <dir_name_to_put_app_there>`
