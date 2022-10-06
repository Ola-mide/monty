# Stacks, Queues - LIFO, FIFO

# Requirements
## General

<li> Allowed editors: vi, vim, emacs
<li> All your files will be compiled on Ubuntu 20.04 LTS using gcc, using the options -Wall -Werror -Wextra -pedantic -std=c89
<li> All your files should end with a new line
<li> A README.md file, at the root of the folder of the project is mandatory
<li> Your code should use the Betty style. It will be checked using betty-style.pl and betty-doc.pl
<li> You allowed to use a maximum of one global variable
<li> No more than 5 functions per file
<li> You are allowed to use the C standard library
<li> The prototypes of all your functions should be included in your header file called monty.h
<li> Don’t forget to push your header file
<li> All your header files should be include guarded
<li> You are expected to do the tasks in the order shown in the project

## Compilation & Output

<li> Your code will be compiled this way:

```
$ gcc -Wall -Werror -Wextra -pedantic -std=c89 *.c -o monty
```

<li> Any output must be printed on stdout
<li> Any error message must be printed on stderr

## The Monty Language

Monty 0.98 is a scripting language that is first compiled into Monty byte codes (Just like Python). It relies on a unique stack, with specific instructions to manipulate it. The goal of this project is to create an interpreter for Monty ByteCodes files.

### Monty byte code files

Files containing Monty byte codes usually have the .m extension. Most of the industry uses this standard but it is not required by the specification of the language. There is not more than one instruction per line. There can be any number of spaces before or after the opcode and its argument:

```
julien@ubuntu:~/monty$ cat -e bytecodes/000.m
push 0$
push 1$
push 2$
  push 3$
                   pall    $
push 4$
    push 5    $
      push    6        $
pall$
julien@ubuntu:~/monty$
```

Monty byte code files can contain blank lines (empty or made of spaces only, and any additional text after the opcode or its required argument is not taken into account:

```
julien@ubuntu:~/monty$ cat -e bytecodes/001.m
push 0 Push 0 onto the stack$
push 1 Push 1 onto the stack$
$
push 2$
  push 3$
                   pall    $
$
$
                           $
push 4$
$
    push 5    $
      push    6        $
$
pall This is the end of our program. Monty is awesome!$
julien@ubuntu:~/monty$
```

### The monty program

<li> Usage: <b>monty file</b>

where <b>file</b>  is the path to the file containing Monty byte code
<li> If the user does not give any file or more than one argument to your program, print the error message <b>USAGE: monty file</b>, followed by a new line, and exit with the status <b>EXIT_FAILURE</b>
<li> If, for any reason, it’s not possible to open the file, print the error message <b>Error: Can't open file <file></b>, followed by a new line, and exit with the status <b>EXIT_FAILURE</b>

where <b>file</b> is the name of the file
<li> If the file contains an invalid instruction, print the error message <b>L<line_number>: unknown instruction <opcode></b>, followed by a new line, and exit with the status <b>EXIT_FAILURE</b>

where is the line number where the instruction appears.

Line numbers always start at 1
<li> The monty program runs the bytecodes line by line and stop if either:

it executed properly every line of the file

it finds an error in the file

an error occured
<li> If you can’t malloc anymore, print the error message <b>Error: malloc failed</b>, followed by a new line, and exit with status <b>EXIT_FAILURE</b>.
<li> You have to use <b>malloc</b> and <b>free</b> and are not allowed to use any other function from <b>man malloc</b> (realloc, calloc, …)

