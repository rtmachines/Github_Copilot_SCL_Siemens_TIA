# 01 Binary Numbers

# BOOL (bit)

| BOOL (bit) |
|---|
Description

An operand of data type BOOL represents a bit value and contains one of the following values:

- TRUE

- FALSE

The following table shows the properties of data type BOOL:

| Length (bits) | Format | Value range | Examples of value input |
|---|---|---|---|
| 1 | Boolean | FALSE or TRUE BOOL#0 or BOOL#1 BOOL#FALSE or BOOL#TRUE | TRUE BOOL#1 BOOL#TRUE |
| Unsigned integers (decimal system) | 0 or 1 | 1 | |
| Binary numbers | 2#0 or 2#1 | 2#0 | |
| Octal numbers | 8#0 or 8#1 | 8#1 | |
| Hexadecimal numbers | 16#0 or 16#1 | 16#1 | |

| Note Applies to CPUs of the S7-1500 series For a block with the block property "Optimized block access", the bit has a length of 1 byte. |
|---|
See also

Overview of the valid data types Basics of constants Data type conversion for S7-1200 (S7-1200)


# Bit strings

BYTE
| BYTE |
|---|
Description

An operand of data type BYTE is a bit string of 8 bits.

The following table shows the properties of data type BYTE:

| Constants | Absolute and symbolic addresses |
|---|---|
| 8 | Integers1) (decimal system) |
| Binary numbers | 2#0 to 2#1111_1111 |
| Octal numbers | 8#0 to 8#377 |
| Hexadecimal numbers | 16#0 to 16#FF |
| 1) The value range depends on the relevant interpretation or conversion. | |

| Note The BYTE data type cannot be compared for more than or less than. It can only be supplied with the same decimal data that can be processed by the SINT and USINT data types. |
|---|
See also

Overview of the valid data types Basics of constants Data type conversion for S7-1200 (S7-1200)

WORD
| WORD |
|---|
Description

An operand of data type WORD is a bit string of 16 bits.

The following table shows the properties of data type WORD:

| Constants | Absolute and symbolic addresses |
|---|---|
| 16 | Integers (decimal system) |
| Binary numbers | 2#0 to 2#1111_1111_1111_1111 |
| Octal numbers | 8#0 to 8#177_777 |
| Hexadecimal numbers | 16#0 to 16#FFFF |
| BCD | C#0 to C#999 |
| Decimal sequence | B#(0, 0) to B#(255, 255) |

| Note The WORD data type cannot be compared for more than or less than. It can only be supplied with the same decimal data that can be processed by the INT and UINT data types. The "BCD" format is not possible in SCL. The "Decimal sequence" is not possible in SCL and GRAPH. |
|---|
See also

Overview of the valid data types Basics of constants Data type conversion for S7-1200 (S7-1200)

DWORD
| DWORD |
|---|
Description

An operand of data type DWORD is a bit string of 32 bits.

The following table shows the properties of data type DWORD:

| Constants | Absolute and symbolic addresses |
|---|---|
| 32 | Integers (decimal system) |
| Binary numbers | 2#0 to 2#1111_1111_1111_1111_1111_1111_1111_1111 |
| Octal numbers | 8#0 to 8#37_777_777_777 |
| Hexadecimal numbers | 16#0000_0000 to 16#FFFF_FFFF |
| Decimal sequence | B#(0, 0, 0, 0) to B#(255, 255, 255, 255) |

| Note The DWORD​ data type cannot be compared for more than or less than. It can only be supplied with the same decimal data that can be processed by the DINT and UDINT data types. The "Decimal sequence" is not possible in SCL and GRAPH. |
|---|
See also

Overview of the valid data types Basics of constants Data type conversion for S7-1200 (S7-1200)

LWORD (S7-1500, S7-1200 G2)
| LWORD |
|---|
Description

An operand of data type LWORD is a bit string of 64 bits.

The following table shows the properties of data type LWORD:

| Length (bits) | Format | Value range | Examples of value input |
|---|---|---|---|
| 64 | Integers (decimal system) | Signed integers: -9_223_372_036_854_775_808 to +9_223_372_036_854_775_807 Unsigned integers: 0 to 18_446_744_073_709_551_615 | +26_123_590_360_715 LWORD#+26_123_590_360_715 LWORD#10#+26_123_590_360_715 LW#+26_123_590_360_715 |
| Binary numbers | 2#0 to 2#1111_1111_1111_1111_1111_1111_1111_1111_1111_1111_1111_1111_1111_1111_1111_1111 | 2#0000_0000_0000_0000_0000_1011_1110_0001_0010_1111_0101_0010_1101_1110_1000_1011 LWORD#2#0000_0000_0000_0000_0000_1011_1110_0001_0010_1111_0101_0010_1101_1110_1000_1011 LW#2#0000_0000_0000_0000_0000_1011_1110_0001_0010_1111_0101_0010_1101_1110_1000_1011 | |
| Octal numbers | 8#0 to 8#1_777_777_777_777_777_777_777 | 8#13_724_557_213 LWORD#8#13_724_557_213 LW#8#13_724_557_213 | |
| Hexadecimal numbers | 16#0000_0000 to 16#FFFF_FFFF_FFFF_FFFF | 16#0000_0000_5F52_DE8B LWORD#16#0000_0000_5F52_DE8B LW#16#0000_0000_5F52_DE8B | |
| Decimal sequence | B#(0, 0, 0, 0, 0, 0, 0, 0) to B#(255, 255, 255, 255, 255, 255, 255, 255) | B#(127, 200, 127, 200, 127, 200, 127, 200) | |

| Note The LWORD data type cannot be compared for more than or less than. It can only be supplied with the same decimal data that can be processed by the LINT and ULINT data types. The "Decimal sequence" is not possible in SCL and GRAPH. |
|---|
See also

Overview of the valid data types Overview of data type conversion (S7-1500, S7-1200 G2) Basics of constants Implicit conversions (S7-1500, S7-1200 G2) Explicit conversions (S7-1500, S7-1200 G2) Data type conversion for S7-1200 (S7-1200)

Integers
