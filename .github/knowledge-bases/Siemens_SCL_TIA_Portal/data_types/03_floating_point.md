# 03 Floating Point

# REAL

| REAL |
|---|
Description

Operands
of the data type REAL have a length of 32 bits and are used to
represent floating-point numbers. An operand of the REAL data type
consists of the following three components:

- Sign: The sign is determined by the signal state of bit 31. The bit 31 assume the value "0" (positive) or "1" (negative).

- 8-bit exponents to basis 2: The exponent is increased by a constant (base, +127), so that it has a value range of 0 to 255.

- 23-
bit mantissa: Only the fraction part of the mantissa is shown. The
integer part of the mantissa is always 1 with normalized floating-point
numbers and is not stored.

The REAL data type is processed with a precision of 6 digits.

The following figure shows the structure of the REAL data type:

| Note With floating-point numbers, only the precision defined by the IEEE754 standard is stored. Additionally specified decimals are rounded off according to IEEE754. The number of decimal places may decrease for frequently nested arithmetic calculations. If more decimal places are specified than can be stored by the data type, the number is rounded to the value corresponding to the precision allowed by this value range. |
|---|
The following table shows the properties of data type REAL:

| Length (bits) | Format | Value range | Examples of value input |
|---|---|---|---|
| 32 | Floating-point numbers according to IEEE754 | -3.402823e+38 to -1.175495e-38 ±0.0 +1.175495e-38 to +3.402823e+38 | 1.0e-5; REAL#1.0e-5 |
| Floating-point numbers | 1.0; REAL#1.0 | | |
See also

Overview of the valid data types Basics of constants Data type conversion for S7-1200 (S7-1200) Calculating with floating-point numbers (REAL and LREAL) in SCL


# LREAL (S7-1200, S7-1500, S7-1200 G2)

| LREAL |
|---|
Description

Operands
of the data type LREAL have a length of 64 bits and are used to
represent floating-point numbers. An operand of the LREAL data type
consists of the following three components:

- Sign: The sign is determined by the signal state of bit 63. The bit 63 assumes the value "0" (positive) or "1" (negative).

- 11-bit exponents to base 2: The exponent is increased by a constant (base, +1023), so that it has a value range of 0 to 2047.

- 52-
bit mantissa: Only the fraction part of the mantissa is shown. The
integer part of the mantissa is always 1 with normalized floating-point
numbers and is not stored.

The LREAL data type is processed with a precision of 15 digits.

The following figure shows the structure of the LREAL data type:

The following table shows the properties of data type LREAL:

| Length (bits) | Format | Value range | Examples of value input |
|---|---|---|---|
| 64 | Floating-point numbers according to IEEE754 | -1.7976931348623157e+308 to -2.2250738585072014e-308 ±0.0 +2.2250738585072014e-308 to +1.7976931348623157e+308 | 1.0e-5; LREAL#1.0e-5 |
| Floating-point numbers | 1.0; LREAL#1.0 | | |

| Note With floating-point numbers, only the precision defined by the IEEE754 standard is stored. Additionally specified decimals are rounded off according to IEEE754. The number of decimal places may decrease for frequently nested arithmetic calculations. If more decimal places are specified than can be stored by the data type, the number is rounded to the corresponding value of the precision allowed by this value range . |
|---|
See also

Overview of the valid data types Basics of constants Data type conversion for S7-1200 (S7-1200) Calculating with floating-point numbers (REAL and LREAL) in SCL


# Invalid floating-point numbers

| Invalid floating-point numbers |
|---|
Description

We distinguish between four number ranges for data types REAL and LREAL:

- normalized numbers stored with full accuracy

- denormalized numbers not stored with full accuracy

- Infinite numbers: +Inf/-Inf (infinity)

- Invalid numbers: NaN (Not a Number)

| Note Floating- point numbers are stored as specified by the IEEE754 standard. Results of conversion or arithmetic functions with a denormalized, infinite or NaN (Not a Number) floating point depend on the CPU. |
|---|
If
you are not working with normalized floating-point numbers in
mathematical functions, the result will show significant differences
depending on the series of the CPU which you are using.

A
CPU cannot calculate with denormalized floating-point numbers, with the
exception of older CPU versions of the S7-300 and S7-400 series. The
bit pattern of a denormalized number is interpreted as a zero. If the
result of calculation falls into this range, it is continued with zero;
the status bits OV and OS are set (number range undershoot).

Even
though the values of invalid floating-point numbers can only be
displayed with limited accuracy for mathematical functions, numbers with
an exponent of -39 (e.g. 2.4408e-039) can be monitored in the TIA
Portal and therefore do not necessarily represent a faulty result. This
means that floating-point values may be located outside the range of
valid numerical values.

| Note The following applies to CPUs of the series S7-1200 V1, V2 and V3: The comparison operation "Equal" uses the bit pattern of the invalid floating-point number. If two "NaN numbers" with the same bit pattern are compared, the output of the "Equal" comparison operation returns the result TRUE. |
|---|

| Note The following applies to CPUs of the S7-1200 V4 and S7-1500 series: If two invalid numbers (NaN) are compared with each other, the result is always FALSE, regardless of the bit pattern of the invalid number or the relation (>, >, ...). |
|---|

| Note Comparison of denormalized floating-point numbers For the comparison operation "Equal" with two denormalized floating-point numbers, the output for CPUs of the S7-300/400 series is set to the signal state "0" and for CPUs of the S7-1200/1500 series to the signal state "1". |
|---|
If
the input variables of a mathematical function represent an invalid
floating-point number, an invalid floating-point number will also be
output as result.

You have the following options to evaluate possible errors caused by invalid floating-point numbers:

- In LAD/FBD and SCL, you can query the enable output ENO for FALSE

- In STL, you can evaluate the status bit OV

See also

Overview of the valid data types Basics of constants Data type conversion for S7-1200 (S7-1200) Calculating with floating-point numbers (REAL and LREAL) in SCL

Timers
