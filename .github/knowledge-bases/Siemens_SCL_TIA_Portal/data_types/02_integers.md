# 02 Integers

# SINT (8-bit integers) (S7-1200, S7-1500, S7-1200 G2)

| SINT (8-bit integers) |
|---|
Description

An
operand of data type SINT (Short INT) has a length of 8 bits and
consists of two components: a sign and a numerical value in the two's
complement. The signal states of bits 0 to 6 represent the number value.
The signal state of bit 7 represents the sign. The sign may assume "0"
for the positive, or "1" for the negative signal state.

An operand of data type SINT occupies one BYTE in the memory.

The following table shows the properties of data type SINT:

| Length (bits) | Format | Value range | Examples of value input |
|---|---|---|---|
| 8 | Signed integers (decimal system) | -128 to +127 | +44 SINT#+44 SINT#10#+44 The value range extends to a maximum of SINT#255 when using the type SINT#. This value is interpreted as an integer with -1. |
| Binary numbers (only positive) | 2#0 to 2#0111_1111 | 2#0010_1100 SINT#2#0010_1100 SINT#2#10 | |
| Octal numbers (only positive) | 8#0 to 8#177 | 8#54 SINT#8#54 | |
| Hexadecimal numbers (only positive) | 16#0 to 16#7F | 16#2C SINT#16#2C The value range extends to a maximum of SINT#16#FF when using the type SINT#. This value is interpreted as an integer with -1. | |
Example

The following figure shows the integer +44 as a binary number:

See also

Overview of the valid data types Basics of constants Data type conversion for S7-1200 (S7-1200)


# USINT (8-bit integers) (S7-1200, S7-1500, S7-1200 G2)

| USINT (8-bit integers) |
|---|
Description

An operand of data type USINT (Unsigned Short INT) has a length of 8 bits and contains unsigned numerical values:

An operand of data type USINT occupies one BYTE in the memory.

The following table shows the properties of data type USINT:

| Length (bits) | Format | Value range | Examples of value input |
|---|---|---|---|
| 8 | Unsigned integers (decimal system) | 0 to 255 | 78 USINT#78 USINT#10#78 |
| Binary numbers | 2#0 to 2#1111_1111 | 2#0100_1110 USINT#2#0100_1110 USINT#2#10 | |
| Octal numbers | 8#0 to 8#377 | 8#116 USINT#8#116 | |
| Hexadecimal numbers | 16#0 to 16#FF | 16#4E USINT#16#4E | |
Example

The following figure shows the integer 78 as a binary number:

See also

Overview of the valid data types Basics of constants Data type conversion for S7-1200 (S7-1200)


# INT (16-bit integers)

| INT (16-bit integers) |
|---|
Description

An
operand of data type INT has a length of 16 bits and consists of two
components: a sign and a numerical value in the two's complement. The
signal states of bits 0 to 14 represent the number value. The signal
state of bit 15 represents the sign. The sign may assume "0" for the
positive, or "1" for the negative signal state.

An operand of data type INT occupies two BYTE in the memory.

The following table shows the properties of data type INT:

| Length (bits) | Format | Value range | Examples of value input |
|---|---|---|---|
| 16 | Signed integers (decimal system) | -32_768 to +32_767 | +3_785 INT#+3_785 INT#10#+3_785 |
| Binary numbers (only positive) | 2#0 to 2#0111_1111_1111_1111 | 2#0000_1110_1100_1001 INT#2#0000_1110_1100_1001 INT#2#10 | |
| Octal numbers (only positive) | 8#0 to 8#7_7777 | 8#7311 INT#8#7311 | |
| Hexadecimal numbers (only positive) | 16#0 to 16#7FFF | 16#0EC9 INT#16#0EC9 | |
Example

The following figure shows the integer +3785 as a binary number:

See also

Overview of the valid data types Basics of constants Data type conversion for S7-1200 (S7-1200)


# UINT (16-bit integers) (S7-1200, S7-1500, S7-1200 G2)

| UINT (16-bit integers) |
|---|
Description

An operand of data type UINT (Unsigned INT) has a length of 16 bits and contains unsigned numerical values.

An operand of data type UINT occupies two BYTE in the memory.

The following table shows the properties of data type UINT:

| Length (bits) | Format | Value range | Examples of value input |
|---|---|---|---|
| 16 | Unsigned integers (decimal system) | 0 to 65_535 | 65_295 UINT#65_295 UINT#10#65_295 |
| Binary numbers | 2#0 to 2#1111_1111_1111_1111 | 2#1111_1111_0000_1111 UINT#2#1111_1111_0000_1111 UINT#2#10 | |
| Octal numbers | 8#0 to 8#17_7777 | 8#17_7417 UINT#8#17_7417 | |
| Hexadecimal numbers | 16#0 to 16#FFFF | 16#FF0F UINT#16#FF0F | |
Example

The following figure shows the integer 65295 as a binary number:

See also

Overview of the valid data types Basics of constants Data type conversion for S7-1200 (S7-1200)


# DINT (32-bit integers)

| DINT (32-bit integers) |
|---|
Description

An
operand of data type DINT (Double INT) has a length of 32 bits and
consists of two components: a sign and a numerical value in the two's
complement. The signal states of bits 0 to 30 represent the number
value. The signal state of bit 31 represents the sign. The sign may
assume "0" for the positive, or "1" for the negative signal state.

An operand of data type DINT occupies four BYTE in the memory.

The following table shows the properties of data type DINT:

| Length (bits) | Format | Value range | Examples of value input |
|---|---|---|---|
| 32 | Signed integers (decimal system) | -2_147_483_648 to +2_147_483_647 | +125_790 DINT#+125_790 DINT#10#+125_790 L#275 |
| Binary numbers (only positive) | 2#0 to 2#0111_1111_1111_1111_1111_1111_1111_1111 | 2#0000_0000_0000_0001_1110_1011_0101_1110 DINT#2#0000_0000_0000_0001_1110_1011_0101_1110 DINT#2#10 | |
| Octal numbers (only positive) | 8#0 to 8#177_7777_7777 | 8#36_5536 DINT#8#36_5536 | |
| Hexadecimal numbers | 16#0 to 16#7FFF_FFFF | 16#0001_EB5E DINT#16#0001_EB5E | |
Example

The following figure shows the integer +125790 as a binary number:

See also

Overview of the valid data types Basics of constants Data type conversion for S7-1200 (S7-1200)


# UDINT (32-bit integers) (S7-1200, S7-1500, S7-1200 G2)

| UDINT (32-bit integers) |
|---|
Description

An operand of data type UDINT (Unsigned Double INT) has a length of 32 bits and contains unsigned numerical values.

An operand of data type UDINT occupies four BYTE in the memory.

The following table shows the properties of data type UDINT:

| Length (bits) | Format | Value range | Examples of value input |
|---|---|---|---|
| 32 | Unsigned integers (decimal system) | 0 to 4_294_967_295 | 4_042_322_160 UDINT#4_042_322_160 UDINT#10#4_042_322_160 |
| Binary numbers | 2#0 to 2#1111_1111_1111_1111_1111_1111_1111_1111 | 2#1111_0000_1111_0000_1111_0000_1111_0000 UDINT#2#1111_0000_1111_0000_1111_0000_1111_0000 UDINT#2#10 | |
| Octal numbers | 8#0 to 8#377_7777_7777 | 8#360_7417_0360 UDINT#8#360_7417_0360 | |
| Hexadecimal numbers | 16#0 to 16#FFFF_FFFF | 16#F0F0_F0F0 UDINT#16#F0F0_F0F0 | |
Example

The following figure shows the integer 4042322160 as a binary number:

See also

Overview of the valid data types Basics of constants Data type conversion for S7-1200 (S7-1200)


# LINT (64-bit integers) (S7-1500, S7-1200 G2)

| LINT (64-bit integers) |
|---|
Description

An
operand of data type LINT (Long INT) has a length of 64 bits and
consists of two components: a sign and a numerical value in the two's
complement. The signal states of bits 0 to 62 represent the number
value. The signal state of bit 63 represents the sign. The sign may
assume "0" for the positive, or "1" for the negative signal state.

An operand of data type LINT occupies eight BYTE in the memory.

The following table shows the properties of data type LINT:

| Length (bits) | Format | Value range | Examples of value input |
|---|---|---|---|
| 64 | Signed integers (decimal system) | -9_223_372_036_854_775_808 to +9_223_372_036_854_775_807 | +154_325_790_816_159 LINT#+154_325_790_816_159 LINT#10#+154_325_790_816_159 |
| Binary numbers (only positive) | 2#0 to 2#0111_1111_1111_1111_1111_1111_1111_1111_1111_1111_1111_1111_1111_1111_1111_1111 | 2#0000_0000_0000_0000_1000_1100_0101_1011_1100_0101_1111_0000_1111_0111_1001_1111 LINT#2#0000_0000_0000_0000_1000_1100_0101_1011_1100_0101_1111_0000_1111_0111_1001_1111 LINT#2#10 | |
| Octal numbers (only positive) | 8#0 to 8#7_7777_7777_7777_7777_7777 | 8#4305_5705_7417_3637 LINT#8#4305_5705_7417_3637 | |
| Hexadecimal numbers (only positive) | 16#0 to 16#7FFF_FFFF_FFFF_FFFF | 16#0000_8C5B_C5F0_F79F LINT#16#0000_8C5B_C5F0_F79F | |
Example

The following figure shows the integer +154325790816159 as a binary number:

See also

Overview of the valid data types Overview of data type conversion (S7-1500, S7-1200 G2) Basics of constants Implicit conversions (S7-1500, S7-1200 G2) Explicit conversions (S7-1500, S7-1200 G2) Data type conversion for S7-1200 (S7-1200)


# ULINT (64-bit integers) (S7-1500, S7-1200 G2)

| ULINT (64-bit integers) |
|---|
Description

An operand of data type ULINT (Unsigned Long INT) has a length of 64 bits and contains unsigned numerical values.

An operand of data type ULINT occupies eight BYTE in the memory.

The following table shows the properties of data type ULINT:

| Length (bits) | Format | Value range | Examples of value input |
|---|---|---|---|
| 64 | Unsigned integers (decimal system) | 0 to 18_446_744_073_709_551_615 | 154_325_790_816_159 ULINT#154_325_790_816_159 ULINT#10#154_325_790_816_159 |
| Binary numbers | 2#0 to 2#1111_1111_1111_1111_1111_1111_1111_1111_1111_1111_1111_1111_1111_1111_1111_1111 | 2#0000_0000_0000_0000_1000_1100_0101_1011_1100_0101_1111_0000_1111_0111_1001_1111 ULINT#2#0000_0000_0000_0000_1000_1100_0101_1011_1100_0101_1111_0000_1111_0111_1001_1111 ULINT#2#10 | |
| Octal numbers | 8#0 to 8#17_7777_7777_7777_7777_7777 | 8#4305_5705_7417_3637 ULINT#8#4305_5705_7417_3637 | |
| Hexadecimal numbers | 16#0 to 16#FFFF_FFFF_FFFF_FFFF | 16#0000_8C5B_C5F0_F79F ULINT#16#0000_8C5B_C5F0_F79F | |
Example

The following figure shows the integer 154325790816159 as a binary number:

See also

Overview of the valid data types Overview of data type conversion (S7-1500, S7-1200 G2) Basics of constants Implicit conversions (S7-1500, S7-1200 G2) Explicit conversions (S7-1500, S7-1200 G2) Data type conversion for S7-1200 (S7-1200)

Floating-point numbers
