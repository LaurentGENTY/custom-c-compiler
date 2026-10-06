# myC compiler

A compiler for **myC**, a small C-like language, that outputs **three-address C code**. Built with **flex** (lexer) and **bison** (parser) in C.

> School project, ENSEIRB-MATMECA (2nd year, Computer Science), by Laurent Genty and Johan Chataigner.

## What it does

The compiler performs the three classic front-end passes:

- **Name analysis**: every variable and function used must be declared.
- **Type analysis**: operations must be well typed (`int`, `float`, pointers).
- **Code generation**: the program is lowered to C in three-address form (one operation per instruction, explicit temporaries).

## Supported features

| Feature | Status |
| --- | --- |
| Explicit variable declarations | ✅ |
| Arbitrary arithmetic expressions | ✅ |
| Assignments to user variables | ✅ |
| `int` / `float` typing | ✅ |
| Memory reads/writes through pointers | ✅ |
| `if` / `if … else` | ✅ (block-local variables not handled) |
| Recursive functions, `struct` | ❌ not implemented |

## Example

Input (`test/test.myc`):

```c
int a, b;
a = 1;
b = 2;
if (a != b) { a = b + 1; } else { b = a + 1; }
```

The compiler produces a `.c` / `.h` pair in three-address form, which is then compiled with `gcc` to check it is valid C.

## Getting started

Requirements: `make`, `gcc`, `flex`, `bison`.

```bash
./compil test/test.myc   # builds myc, compiles the .myc file, then checks the output with gcc
```

Or step by step:

```bash
make          # build the myc compiler
make test     # compile test/test.myc
make clean
```

## Project structure

```
src/
  lang.l                      # lexer (flex)
  lang.y                      # grammar + semantic actions (bison)
  Attribute.{c,h}             # attributes carried during type/name analysis
  Table_des_symboles.{c,h}    # symbol table (linked list: name, type, value)
  Table_des_chaines.{c,h}     # string table for identifiers
test/test.myc                 # sample program
compil                        # build-and-check script
```
