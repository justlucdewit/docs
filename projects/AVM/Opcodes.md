Undearneath is a table containing all the opcodes available in the AVM Bytecode format. Each opcode in the bytecode could be followed by a fixed amout of 'argument bytes' which are used to describe one or more arguments to the opcode.

for example:, an opcode used like `MOV A 5`, takes a register argument (which is 1 byte in size) and a literal argument (which is 8 bytes in size). This means that the opcode for `MOV <REG> <LIT>` has 8 + 1 = 9 argument bytes.

The opcode id itself, is always one byte, where the first nibble describes its opcode group, and the upper nibble describes the specific opcode.

## Opcode groups

| Group nibble | Group name             | Description                                                                   |
|:------------ |:---------------------- |:----------------------------------------------------------------------------- |
| 0x0          | Register management    | Moving and changing data in registers                                         |
| 0x1          | Stack management       | Moving and changing data on the stack                                         |
| 0x2          | Heap management        | Moving and changing data on the heap                                          |
| 0x4          | Control flow           | Changes where in the program the vm is executing, possibly conditionally      |
| 0x5          | Mathematical operators | Applies some mathematical operation to the stack or some register             |
| 0xF          | Miscelaneous           | Other opcodes that dont fit in a specific group like native function and halt |

## Opcodes

| Opcode id | Group name          | Arg byte # | Argument signature          | description |
|:--------- |:------------------- |:---------- |:--------------------------- |:----------- |
| 0x00      | Register management | 9          | MOV &lt;REG&gt; &lt;LIT&gt; | Moves some literal value into a register            |
| 0x01      | Register management | 2          | MOV &lt;REG&gt; &lt;REG&gt; | Moves from value in a register to another register            |
| 0x10      | Stack management    | 8          | PUSH &lt;LIT&gt;            | Pushes some literal value to the stack            |
| 0x11      | Stack management    | 1          | PUSH &lt;REG&gt;            | Pushes value of some register to the stack            |
| 0x12      | Stack management    | 8          | PUSH &lt;PTR&gt;            | Pushes some value at some memory location to the stack            |
| 0x13      | Stack management    | 1          | POP &lt;REG&gt;             | Pops value on top of stack to some register            |
| 0x14      | Stack management    | 8          | POP &lt;PTR&gt;             | Pops value on top of stack to some memory location            |
| 0x15      | Stack management    | 0          | SWAP                        | Swaps top 2 values on the stack            |
| 0x16      | Stack management    | 8          | DIG &lt;LIT&gt;             | Brings the Nth value on the stack (counted from the top) to the top            |
| 0x17      | Stack management    | 0          | POP                         | Trashes the top value of the stack            |
| 0xF0      | HALT                | 0          | HALT                        | Halts the program with code *whatever is in the A register*            |
| 0xF1      | NATFUNC             | 0          | NATFUNC                     | Calls some native functionality (needed to communicate with OS) based on what index is in the A register,             |
