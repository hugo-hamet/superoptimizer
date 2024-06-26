# 🐢 AG2 lang documentation
**AG2** is an assembler-like language. It's designed to be lightweight, and also easily optimizable.

## Overview

Each program has a total of 8 registers, each containing an 8-bit integer (also called a `char`, for my fellow C programmers). All values are initialized at 0.\
A line can only contain one instruction. If you want to add more code, add more lines.

You can write in AG2 straight away using the `.at` file extension, and then compile your script with the `ag2` binary (learn how to build it in the [compiler section](#compiler)).

The purpose of an AG2 program is to execute each of its instructions, to then dump its memory in this format:
```v
[ reg0, reg1, reg2, reg3, reg4, reg5, reg6, reg7 ]
```

> *In the future...*
>   - Support for multiple instructions on a same line
>   - Add a header comment saved in the compiled binary
>   - Register overflow error handling
>   - Add more cheese
>   - Control flow instructions (screw the superoptimizer)
>   - Dynamic argument typings

## Instructions
* `val` - Numerical value. 5 means the number 5.
* `mem` - Index of one of the program's register. 5 means the 4th register (it starts at 0).
* `str` - String value, has to be constituted of printable characters only. If spaces are needed, add simple or double quotes at the start and end of the string.

| Hex value | Instruction usage | Description |
|---:|:---|:---|
| 0x00 | `NAME str` | Defines the name of the program: displayed at runtime. You are allowed one and only `NAME` instruction by program, and its value should not be over 128 characters long. |
| 0x01 | `LOAD val` | Loads the immediate value into the memory location 0. |
| 0x02 | `SWAP mem mem` | Swaps the values of the two memory locations. |
| 0x03 | `CMEM mem` | Counts the number of memory blocks that are empty, and stocks that value at the memory location. |
| 0x04 | `INC mem` | Increments the value at the memory location. |
| 0x05 | `XOR mem mem` | Performs a bitwise XOR operation on the memory blocks' values and stores the result in the first memory location. |

> [!NOTE]
> If you haven't guessed it yet, AG2 is a deterministic programming language. There is no chance or random involved: what you write is what's happening.

## Compiler <a name="compiler"></a>
Here is a step-by-step little guide on how to use the `ag2` compiler.

* After cloning the repository, go in the [`ag2-lang`](./../ag2-lang/) folder.
* Execute the `make` command.
* You now have the `ag2` binary! Try out the `--help` flag to learn more on its usage.

> *In the future...*
>   - Compilation warnings and suggestions
>   - More error handling

## Example

Source code:
```cpp
LOAD 2
XOR 0 3
XOR 0 4
INC 3
CMEM 6
XOR 6 3
```
Output:
```cpp
[ 2, 0, 0, 3, 2, 0, 5, 0 ]
```
