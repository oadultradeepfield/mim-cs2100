# Mim: MIPS Reference Data Improved (for CS2100 AY2024/25 S2)

I found the given reference sheet quite difficult to use. I made a list that allows faster format conversion and reduces human errors when converting between binary, hex, and decimal. You can also get the PDF version [here](/mim_print.pdf) (this was created using [LaTeX](/mim_print.tex)).

## Register

Aside from the constant zeroes, we have `t` for temporaries and `s` for saved temporaries.

| `$zero` | `$t0` | `$t1` | `$t2` | `$t3` | `$t4` | `$t5` | `$t6` | `$t7` |
| ------- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| 00000   | 01000 | 01001 | 01010 | 01011 | 01100 | 01101 | 01110 | 01111 |

| `$t8` | `$t9` | `$s0` | `$s1` | `$s2` | `$s3` | `$s4` | `$s5` | `$s6` | `$s7` |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| 11000 | 11001 | 10000 | 10001 | 10010 | 10011 | 10100 | 10101 | 10110 | 10111 |

## R-Format

The R-format always has an `opcode` of 0. The instruction can be determined using the `funct` field. The shift amount (`shamt`) is only applicable to shift left/right logical instructions.

| Mnemonic            | `opcode` (6) | `rs` (5) | `rt` (5) | `rd` (5) | `shamt` (5) | `funct` (6) |
| ------------------- | ------------ | -------- | -------- | -------- | ----------- | ----------- |
| `add rd, rs, rt`    | 000000       | `rs`     | `rt`     | `rd`     | 00000       | 100000      |
| `sub rd, rs, rt`    | 000000       | `rs`     | `rt`     | `rd`     | 00000       | 100010      |
| `sll rd, rt, shamt` | 000000       | 00000    | `rt`     | `rd`     | `shamt`     | 000000      |
| `srl rd, rt, shamt` | 000000       | 00000    | `rt`     | `rd`     | `shamt`     | 000010      |
| `and rd, rs, rt`    | 000000       | `rs`     | `rt`     | `rd`     | 00000       | 100100      |
| `or rd, rs, rt`     | 000000       | `rs`     | `rt`     | `rd`     | 00000       | 100101      |
| `xor rd, rs, rt`    | 000000       | `rs`     | `rt`     | `rd`     | 00000       | 100110      |
| `nor rd, rs, rt`    | 000000       | `rs`     | `rt`     | `rd`     | 00000       | 100111      |
| `slt rd, rs, rt`    | 000000       | `rs`     | `rt`     | `rd`     | 00000       | 101010      |

## I-Format

The immediate is always a 16-bit integer. You need to use load upper immediate (`lui`) to extend it to 32 bits.

| Mnemonic                       | `opcode` (6) | `rs` (5) | `rt` (5) | `immediate` (16)   |
| ------------------------------ | ------------ | -------- | -------- | ------------------ |
| `beq rs, rt, relative address` | 000100       | `rs`     | `rt`     | `relative address` |
| `bne rs, rt, relative address` | 000101       | `rs`     | `rt`     | `relative address` |
| `addi rt, rs, immediate`       | 001000       | `rs`     | `rt`     | `immediate`        |
| `andi rt, rs, immediate`       | 001100       | `rs`     | `rt`     | `immediate`        |
| `ori rt, rs, immediate`        | 001101       | `rs`     | `rt`     | `immediate`        |
| `xori rt, rs, immediate`       | 001110       | `rs`     | `rt`     | `immediate`        |
| `lui rt, immediate`            | 001111       | 00000    | `rt`     | `immediate`        |
| `lb rt, immediate(rs)`         | 100000       | `rs`     | `rt`     | `immediate`        |
| `lw rt, immediate(rs)`         | 100011       | `rs`     | `rt`     | `immediate`        |
| `sb rt, immediate(rs)`         | 101000       | `rs`     | `rt`     | `immediate`        |
| `sw rt, immediate(rs)`         | 101011       | `rs`     | `rt`     | `immediate`        |

## J-Format

The memory address is always 32 bits. However, since it must be well-aligned with offsets as multiples of 4, the last 2 bits can be ignored. The full address is constructed using the upper 4 bits from the current PC + 4.

| Mnemonic    | `opcode (6)` | `address (26)`                                      |
| ----------- | ------------ | --------------------------------------------------- |
| `j address` | 000010       | 26-bit target address (shifted left by 2 when used) |

## Extra: Binary and Hexadecimal Conversion Table

This table would be helpful when encoding/decoding instructions so we can group every four bits in the binary representation to a single hexadecimal digit.

| Binary | Hexadecimal | Binary | Hexadecimal |
| ------ | ----------- | ------ | ----------- |
| 0000   | 0           | 1000   | 8           |
| 0001   | 1           | 1001   | 9           |
| 0010   | 2           | 1010   | A           |
| 0011   | 3           | 1011   | B           |
| 0100   | 4           | 1100   | C           |
| 0101   | 5           | 1101   | D           |
| 0110   | 6           | 1110   | E           |
| 0111   | 7           | 1111   | F           |

## License

This project is licensed under the MIT License. See the [LICENSE](/LICENSE) file for details.
