# 12 Conversions

# Overview of data type conversion (S7-1500, S7-1200 G2)

| Overview of data type conversion |
|---|
Introduction

If
you combine several operands in an instruction, you must make sure that
the data types are compatible. This also applies when you assign or
supply block parameters. If the operands are not of the same data type, a
conversion has to be carried out.

There are two options for conversion:

- Implicit conversion

Implicit
conversion is supported by the programming languages LAD, FBD, SCL and
GRAPH. Implicit conversion is not possible in the STL programming
language.

- Explicit conversion

You use an explicit conversion instruction before the actual instruction is executed.

| Note Converting bit strings to SCL All bit strings (BYTE, WORD, DWORD and LWORD) are handled like the corresponding unsigned integers (USINT, UINT, UDINT and ULINT) in expressions. Therefore, implicit conversion from DWORD to REAL is carried out like a conversion from UDINT to REAL, for example. |
|---|

| Note Converting REF() A data type conversion of REF() is not possible. The transferred tag must correspond exactly to the target data type. |
|---|
Implicit conversion

Implicit
conversion is executed automatically if the data types of the operands
are compatible. This compatibility test can be carried out according to
strict or less strict criteria:

- With IEC check (default setting)

If IEC check is set, the following rules are applied:

- Implicit conversion of BOOL into other data types is not possible.

- Only
the data types REAL, BYTE, WORD, DWORD, DINT, INT, SINT, UDINT, UINT,
USINT, TIME, LDT, DTL, DT, TOD, WCHAR and CHAR can be converted
implicitly.

- The
bit length of the source data type may not exceed the bit length of the
target data type. A WORD data type operand, for example, cannot be
specified at a parameter at which the BYTE data type is expected.

- Without IEC check

If IEC check is not set, the following rules are applied:

- Implicit conversion of BOOL into other data types is not possible.

- Only
the data types REAL, LREAL, BYTE, WORD, DWORD, LWORD, SINT, INT, DINT,
LINT, USINT, UINT, UDINT, ULINT, TIME, LTIME, S5TIME, LDT, DTL, TOD,
LTOD, DATE, STRING, WSTRING, WCHAR and CHAR can be converted implicitly.

- The
bit length of the source data type may not exceed the bit length of the
target data type. A DWORD data type operand, for example, cannot be
specified at a parameter at which the WORD data type is expected.

- The
bit length of an operand entered at in-out parameters (InOut) must be
the same as the programmed bit length for the parameter in question.

| Note Implicit conversion without IEC check The programming editor uses a gray rectangle to mark operands that are implicitly converted. The dark gray rectangle signals that an implicit conversion is possible without any accuracy loss, for example, if you convert the data type INT to DINT. A light gray rectangle signals that implicit conversion is possible, but errors could occur during runtime. If, for example, you are converting the data type LINT to DINT and an overflow occurs, the enable output ENO is set to "0". |
|---|

For more information about the setting of the IEC check and the implicit conversion, refer to "See also".

Explicit conversion

If
the operands are not compatible and implicit conversion is therefore
not possible, you can perform an explicit conversion. You can do this by
using the conversion instructions in the "Instructions" Task Card or
you can insert the conversion into the program manually. You can find
the format for explicit conversion functions under "See also".

Any
overflow will be displayed on the ENO enable output. An overflow
occurs, for example, if the value of the source data type is greater
than the value of the target data type.

| Note Shifting of bit patterns​ If the explicit conversion involves shifting a bit pattern, the enable output ENO is not set. |
|---|
You can find additional information on explicit conversion under "See also".

The following figure shows an example in which explicit data type conversion must be carried out:

The
"Block" function block expects a tag of the INT data type at the
"IN_INT" input parameter. The value of the "IN_DINT" tag has therefore
to the converted first from DINT to INT. Conversion is performed if the
value of the "IN_DINT" tag is within the admissible value range for the
INT data type. Otherwise an overflow is reported. However, a conversion
takes place even in the event of an overflow, but the values are
truncated and the ENO enable output is set to "0".

See also

Implicit conversions (S7-1500, S7-1200 G2) Explicit conversions (S7-1500, S7-1200 G2)


# Implicit conversions (S7-1500, S7-1200 G2)

Activate or deactivate IEC check (S7-1500, S7-1200 G2)
| Activate or deactivate IEC check |
|---|
The
data types of the operands used are checked for compatibility. This
compatibility test can be carried out according to criteria that are
more or less strict. If "IEC check for code blocks" is activated,
stricter criteria are applied.

You can set the IEC check centrally for all new blocks of the project or for individual blocks.

Setting IEC check for new blocks

To set the IEC check for all new blocks in the project, proceed as follows:

- Select the "Settings" command in the "Options" menu.

The "Settings" window is displayed in the work area.

- Select the "PLC programming > General" group in the area navigation.

- Select or clear the "IEC check for code blocks" check box in the "Default settings for new blocks" group.

The IEC check is enabled or disabled for all new blocks in the program.

Setting IEC check for a block

To set the IEC check for a block, proceed as follows:

- Open the block.

- Open the "Properties" tab in the inspector window.

- Select the "Attributes" group in the area navigation.

- Select or clear the "IEC check" check box.

The IEC check is enabled or disabled for this block. The setting is stored together with the project.

Binary numbers (S7-1500, S7-1200 G2) Implicit conversion of BOOL (S7-1500, S7-1200 G2)
| Implicit conversion of BOOL |
|---|
Implicit conversion options

The BOOL data type cannot be implicitly converted.

See also

BOOL (bit) Overview of data type conversion (S7-1500, S7-1200 G2) Activate or deactivate IEC check (S7-1500, S7-1200 G2) Explicit conversion of BOOL (S7-1500, S7-1200 G2)

Bit strings (S7-1500, S7-1200 G2) Implicit conversion of BYTE (S7-1500, S7-1200 G2)
| Implicit conversion of BYTE |
|---|
Implicit conversion options

The following table shows the options for the implicit conversion of BYTE data type:

| Source | Destination | With IEC check | Without IEC check | Explanation |
|---|---|---|---|---|
| BYTE | BOOL | - | - | No implicit conversion |
| WORD | X | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| DWORD | X | X | | |
| LWORD | X | X | | |
| SINT | - | X | | |
| USINT | - | X | | |
| INT | - | X | | |
| UINT | - | X | | |
| DINT | - | X | | |
| UDINT | - | X | | |
| LINT | - | X | | |
| ULINT | - | X | | |
| REAL | - | - | No implicit conversion | |
| LREAL | - | - | | |
| TIME | - | - | | |
| LTIME | - | - | | |
| S5TIME | - | - | | |
| LDT | - | - | | |
| DTL | - | - | | |
| DT | - | - | | |
| DATE | - | - | | |
| TOD | - | - | | |
| LTOD | - | - | | |
| STRING | - | - | | |
| WSTRING | - | - | | |
| CHAR | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| WCHAR | - | X | | |
| x: Conversion possible -: Conversion not possible | | | | |
See also

BYTE Activate or deactivate IEC check (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) Explicit conversion of BYTE (S7-1500, S7-1200 G2)

Implicit conversion of WORD (S7-1500, S7-1200 G2)
| Implicit conversion of WORD |
|---|
Implicit conversion options

The following table shows the options for the implicit conversion of WORD data type:

| Source | Destination | With IEC check | Without IEC check | Explanation |
|---|---|---|---|---|
| WORD | BOOL | - | - | No implicit conversion |
| BYTE | - | X | The low byte is transferred to the destination data type; the high byte is ignored. | |
| DWORD | X | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| LWORD | X | X | | |
| SINT | - | X | The low byte is transferred to the destination data type; the high byte is ignored. | |
| USINT | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| INT | - | X | | |
| UINT | - | X | | |
| DINT | - | X | | |
| UDINT | - | X | | |
| LINT | - | X | | |
| ULINT | - | X | | |
| REAL | - | - | No implicit conversion | |
| LREAL | - | - | | |
| TIME | - | - | | |
| LTIME | - | - | | |
| S5TIME | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| WORD | LDT | - | - | No implicit conversion |
| DTL | - | - | | |
| DT | - | - | | |
| DATE | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| TOD | - | - | No implicit conversion | |
| LTOD | - | - | | |
| STRING | - | - | | |
| WSTRING | - | - | | |
| CHAR | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| WCHAR | - | X | | |
| x: Conversion possible -: Conversion not possible | | | | |
See also

WORD Activate or deactivate IEC check (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) Explicit conversion of WORD (S7-1500, S7-1200 G2)

Implicit conversion of DWORD (S7-1500, S7-1200 G2)
| Implicit conversion of DWORD |
|---|
Implicit conversion options

The following table shows the options for the implicit conversion of DWORD data type:

| Source | Destination | With IEC check | Without IEC check | Explanation |
|---|---|---|---|---|
| DWORD | BOOL | - | - | No implicit conversion |
| BYTE | - | X | The right byte is transferred to the destination data type; the left byte is ignored. | |
| WORD | - | X | | |
| LWORD | X | X | | |
| SINT | - | X | | |
| USINT | - | X | | |
| INT | - | X | | |
| UINT | - | X | | |
| DINT | - | X | The bit pattern of the source value is transferred unchanged to the destination data type. | |
| UDINT | - | X | | |
| LINT | - | X | | |
| ULINT | - | X | | |
| REAL | - | X | The value is converted to the destination data type format. (The value "-1", for example, is converted to the value "-1.0".) | |
| LREAL | - | - | No implicit conversion | |
| TIME | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| LTIME | - | - | No implicit conversion | |
| S5TIME | - | - | | |
| LDT | - | - | | |
| DWORD | DTL | - | - | No implicit conversion |
| DT | - | - | | |
| DATE | - | - | | |
| TOD | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| LTOD | - | - | No implicit conversion | |
| STRING | - | - | | |
| WSTRING | - | - | | |
| CHAR | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| WCHAR | - | X | | |
| x: Conversion possible -: Conversion not possible | | | | |
See also

DWORD Activate or deactivate IEC check (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) Explicit conversion of DWORD (S7-1500, S7-1200 G2)

Implicit conversion of LWORD (S7-1500, S7-1200 G2)
| Implicit conversion of LWORD |
|---|
Implicit conversion options

The following table shows the options for the implicit conversion of LWORD data type:

| Source | Destination | With IEC check | Without IEC check | Explanation |
|---|---|---|---|---|
| LWORD | BOOL | - | - | No implicit conversion |
| BYTE | - | X | The right byte is transferred to the destination data type; the left byte is ignored. | |
| WORD | - | X | | |
| DWORD | - | X | | |
| SINT | - | X | | |
| USINT | - | X | | |
| INT | - | X | | |
| UINT | - | X | | |
| DINT | - | X | | |
| UDINT | - | X | | |
| LINT | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| ULINT | - | X | | |
| REAL | - | - | No implicit conversion | |
| LREAL | - | X | The value is converted to the destination data type format. (The value "-1", for example, is converted to the value "-1.0".) | |
| TIME | - | - | No implicit conversion | |
| LTIME | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| S5TIME | - | - | No implicit conversion | |
| LDT | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| DTL | - | - | No implicit conversion | |
| DT | - | - | | |
| DATE | - | - | | |
| TOD | - | - | | |
| LTOD | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| STRING | - | - | No implicit conversion | |
| WSTRING | - | - | | |
| CHAR | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| WCHAR | - | X | | |
| x: Conversion possible -: Conversion not possible | | | | |
See also

Activate or deactivate IEC check (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) LWORD (S7-1500, S7-1200 G2) Explicit conversion of LWORD (S7-1500, S7-1200 G2)

Integers (S7-1500, S7-1200 G2) Implicit conversion of SINT (S7-1500, S7-1200 G2)
| Implicit conversion of SINT |
|---|
Implicit conversion options

The following table shows the options for the implicit conversion of SINT data type:

| Source | Destination | With IEC check | Without IEC check | Explanation |
|---|---|---|---|---|
| SINT | BOOL | - | - | No implicit conversion |
| BYTE | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. The remaining bits are filled with "0". | |
| WORD | - | X | | |
| DWORD | - | X | | |
| LWORD | - | X | | |
| USINT | - | X | The bit pattern of the source value is converted and transferred to the destination data type. (for example, value transfer from SINT #-1 -> INT #-1, not filled with "0".) | |
| INT | X | X | | |
| UINT | - | X | | |
| DINT | X | X | | |
| UDINT | - | X | | |
| LINT | X | X | | |
| ULINT | - | X | | |
| REAL | X | X | The value is converted to the destination data type format. (The value "-1", for example, is converted to the value "-1.0".) | |
| LREAL | X | X | | |
| TIME | - | - | No implicit conversion | |
| LTIME | - | - | | |
| S5TIME | - | - | | |
| LDT | - | - | | |
| DTL | - | - | | |
| DT | - | - | | |
| DATE | - | - | | |
| TOD | - | - | | |
| LTOD | - | - | | |
| STRING | - | - | | |
| WSTRING | - | - | | |
| CHAR | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| WCHAR | - | X | | |
| x: Conversion possible -: Conversion not possible | | | | |
See also

Activate or deactivate IEC check (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) SINT (8-bit integers) (S7-1200, S7-1500, S7-1200 G2) Explicit conversion of SINT (S7-1500, S7-1200 G2)

Implicit conversion of USINT (S7-1500, S7-1200 G2)
| Implicit conversion of USINT |
|---|
Implicit conversion options

The following table shows the options for the implicit conversion of USINT data type:

| Source | Destination | With IEC check | Without IEC check | Explanation |
|---|---|---|---|---|
| USINT | BOOL | - | - | No implicit conversion |
| BYTE | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. The remaining bits are filled with "0". | |
| WORD | - | X | | |
| DWORD | - | X | | |
| LWORD | - | X | | |
| SINT | - | X | The bit pattern of the source value is converted and transferred to the destination data type. (for example, value conversion from USINT #10 -> DINT #10 or USINT #128 -> SINT #-128) | |
| INT | X | X | | |
| UINT | X | X | | |
| DINT | X | X | | |
| UDINT | X | X | | |
| LINT | X | X | | |
| ULINT | X | X | | |
| REAL | X | X | The value is converted to the destination data type format. (The value "-1", for example, is converted to the value "-1.0".) | |
| LREAL | X | X | | |
| TIME | - | - | No implicit conversion | |
| LTIME | - | - | | |
| S5TIME | - | - | | |
| LDT | - | - | | |
| DTL | - | - | | |
| DT | - | - | | |
| DATE | - | - | | |
| TOD | - | - | | |
| LTOD | - | - | | |
| STRING | - | - | | |
| WSTRING | - | - | | |
| CHAR | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| WCHAR | - | X | | |
| x: Conversion possible -: Conversion not possible | | | | |
See also

Activate or deactivate IEC check (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) USINT (8-bit integers) (S7-1200, S7-1500, S7-1200 G2) Explicit conversion of USINT (S7-1500, S7-1200 G2)

Implicit conversion of INT (S7-1500, S7-1200 G2)
| Implicit conversion of INT |
|---|
Implicit conversion options

The following table shows the options for the implicit conversion of INT data type:

| Source | Destination | With IEC check | Without IEC check | Explanation |
|---|---|---|---|---|
| INT | BOOL | - | - | No implicit conversion |
| BYTE | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| WORD | - | X | | |
| DWORD | - | X | | |
| LWORD | - | X | | |
| SINT | - | X | The bit pattern of the source value is converted and transferred to the destination data type. (for example, value conversion from INT #-1 -> SINT #-1, or INT #-32 767 -> UINT #32 769) | |
| USINT | - | X | | |
| UINT | - | X | | |
| DINT | X | X | | |
| UDINT | - | X | | |
| LINT | X | X | | |
| ULINT | - | X | | |
| REAL | X | X | The value is converted to the destination data type format. (The value "-1", for example, is converted to the value "-1.0".) | |
| LREAL | X | X | | |
| TIME | - | - | No implicit conversion | |
| LTIME | - | - | | |
| S5TIME | - | - | | |
| LDT | - | - | | |
| DTL | - | - | | |
| DT | - | - | | |
| DATE | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| TOD | - | - | No implicit conversion | |
| LTOD | - | - | | |
| STRING | - | - | | |
| WSTRING | - | - | | |
| CHAR | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| WCHAR | - | X | | |
| x: Conversion possible -: Conversion not possible | | | | |
See also

Activate or deactivate IEC check (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) INT (16-bit integers) Explicit conversion of INT (S7-1500, S7-1200 G2)

Implicit conversion of UINT (S7-1500, S7-1200 G2)
| Implicit conversion of UINT |
|---|
Implicit conversion options

The following table shows the options for the implicit conversion of UINT data type:

| Source | Destination | With IEC check | Without IEC check | Explanation |
|---|---|---|---|---|
| UINT | BOOL | - | - | No implicit conversion |
| BYTE | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| WORD | - | X | | |
| DWORD | - | X | | |
| LWORD | - | X | | |
| SINT | - | X | The bit pattern of the source value is converted and transferred to the destination data type. (for example, value conversion from UINT #100 -> DINT #100 or UINT #60 000 -> INT #-5536) | |
| USINT | - | X | | |
| INT | - | X | | |
| DINT | X | X | | |
| UDINT | X | X | | |
| LINT | X | X | | |
| ULINT | X | X | | |
| REAL | X | X | The value is converted to the destination data type format. (The value "-1", for example, is converted to the value "-1.0".) | |
| LREAL | X | X | | |
| TIME | - | - | No implicit conversion | |
| LTIME | - | - | | |
| S5TIME | - | - | | |
| LDT | - | - | | |
| DTL | - | - | | |
| DT | - | - | | |
| DATE | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| TOD | - | - | No implicit conversion | |
| LTOD | - | - | | |
| STRING | - | - | | |
| WSTRING | - | - | | |
| CHAR | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| WCHAR | - | X | | |
| x: Conversion possible -: Conversion not possible | | | | |
See also

Activate or deactivate IEC check (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) UINT (16-bit integers) (S7-1200, S7-1500, S7-1200 G2) Explicit conversion of UINT (S7-1500, S7-1200 G2)

Implicit conversion of DINT (S7-1500, S7-1200 G2)
| Implicit conversion of DINT |
|---|
Implicit conversion options

The following table shows the options for the implicit conversion of DINT data type:

| Source | Destination | With IEC check | Without IEC check | Explanation |
|---|---|---|---|---|
| DINT | BOOL | - | - | No implicit conversion |
| BYTE | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| WORD | - | X | | |
| DWORD | - | X | | |
| LWORD | - | X | | |
| SINT | - | X | The bit pattern of the source value is converted and transferred to the destination data type. (for example, value conversion from DINT #-1 -> SINT #-1 or DINT #-1 -> USINT #255) | |
| USINT | - | X | | |
| INT | - | X | | |
| UINT | - | X | | |
| UDINT | - | X | | |
| LINT | X | X | | |
| ULINT | - | X | | |
| REAL | - | X | The bit pattern of the source value is converted and transferred to the destination data type. (for example, value conversion from DINT #-1 -> REAL #-1.0, but there is a loss in accuracy for numbers with an absolute value greater than 8 388 608) | |
| LREAL | X | X | The value is converted to the destination data type format. (The value "-1", for example, is converted to the value "-1.0".) | |
| TIME | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| DINT | LTIME | - | - | No implicit conversion |
| S5TIME | - | - | | |
| LDT | - | - | | |
| DTL | - | - | | |
| DT | - | - | | |
| DATE | - | - | | |
| TOD | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| LTOD | - | - | No implicit conversion | |
| STRING | - | - | | |
| WSTRING | - | - | | |
| CHAR | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| WCHAR | - | X | | |
| x: Conversion possible -: Conversion not possible | | | | |
See also

Activate or deactivate IEC check (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) DINT (32-bit integers) Explicit conversion of DINT (S7-1500, S7-1200 G2)

Implicit conversion of UDINT (S7-1500, S7-1200 G2)
| Implicit conversion of UDINT |
|---|
Implicit conversion options

The following table shows the options for the implicit conversion of UDINT data type:

| Source | Destination | With IEC check | Without IEC check | Explanation |
|---|---|---|---|---|
| UDINT | BOOL | - | - | No implicit conversion |
| BYTE | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| WORD | - | X | | |
| DWORD | - | X | | |
| LWORD | - | X | | |
| SINT | - | X | The bit pattern of the source value is converted and transferred to the destination data type. (for example, value conversion from DINT #-1 -> SINT #-1 or DINT #-1 -> USINT #255) | |
| USINT | - | X | | |
| INT | - | X | | |
| UINT | - | X | | |
| DINT | - | X | | |
| LINT | X | X | | |
| ULINT | X | X | | |
| REAL | - | X | The bit pattern of the source value is converted and transferred to the destination data type. (for example, value conversion from DINT #-1 -> REAL #-1.0, but there is a loss in accuracy for numbers with an absolute value greater than 8 388 608) | |
| LREAL | X | X | The value is converted to the destination data type format. (The value "-1", for example, is converted to the value "-1.0".) | |
| TIME | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| UDINT | LTIME | - | - | No implicit conversion |
| S5TIME | - | - | | |
| LDT | - | - | | |
| DTL | - | - | | |
| DT | - | - | | |
| DATE | - | - | | |
| TOD | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| LTOD | - | - | No implicit conversion | |
| STRING | - | - | | |
| WSTRING | - | - | | |
| CHAR | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| WCHAR | - | X | | |
| x: Conversion possible -: Conversion not possible | | | | |
See also

Activate or deactivate IEC check (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) UDINT (32-bit integers) (S7-1200, S7-1500, S7-1200 G2) Explicit conversion of UDINT (S7-1500, S7-1200 G2)

Implicit conversion of LINT (S7-1500, S7-1200 G2)
| Implicit conversion of LINT |
|---|
Implicit conversion options

The following table shows the options for the implicit conversion of LINT data type:

| Source | Destination | With IEC check | Without IEC check | Explanation |
|---|---|---|---|---|
| LINT | BOOL | - | - | No implicit conversion |
| BYTE | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| WORD | - | X | | |
| DWORD | - | X | | |
| LWORD | - | X | | |
| SINT | - | X | The bit pattern of the source value is converted and transferred to the destination data type. (for example, value conversion from LINT #-1 -> SINT #-1 or LINT #-1 -> USINT #255) | |
| USINT | - | X | | |
| INT | - | X | | |
| UINT | - | X | | |
| DINT | - | X | | |
| UDINT | - | X | | |
| ULINT | - | X | | |
| REAL | - | X | The bit pattern of the source value is converted and transferred to the destination data type. (for example, value conversion from LINT #-1 -> REAL #-1.0, but there is a loss in accuracy for numbers with an absolute value greater than 8 388 608) | |
| LREAL | - | X | The bit pattern of the source value is converted and transferred to the destination data type. (for example, value conversion from LINT #-1 -> REAL #-1.0, but there is a loss in accuracy for numbers with an absolute value greater than 9 007 199 254 740 992) | |
| LINT | TIME | - | - | No implicit conversion |
| LTIME | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. (duration in nanoseconds) | |
| S5TIME | - | - | No implicit conversion | |
| LDT | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. (nanoseconds since 1/1/1970) | |
| DTL | - | - | No implicit conversion | |
| DT | - | - | | |
| DATE | - | - | | |
| TOD | - | - | | |
| LTOD | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| STRING | - | - | No implicit conversion | |
| WSTRING | - | - | | |
| CHAR | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| WCHAR | - | X | | |
| x: Conversion possible -: Conversion not possible | | | | |
See also

Activate or deactivate IEC check (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) LINT (64-bit integers) (S7-1500, S7-1200 G2) Explicit conversion of LINT (S7-1500, S7-1200 G2)

Implicit conversion of ULINT (S7-1500, S7-1200 G2)
| Implicit conversion of ULINT |
|---|
Implicit conversion options

The following table shows the options for the implicit conversion of ULINT data type:

| Source | Destination | With IEC check | Without IEC check | Explanation |
|---|---|---|---|---|
| ULINT | BOOL | - | - | No implicit conversion |
| BYTE | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| WORD | - | X | | |
| DWORD | - | X | | |
| LWORD | - | X | | |
| SINT | - | X | The bit pattern of the source value is converted and transferred to the destination data type. (for example, value conversion from ULINT #-1 -> SINT #-1 or ULINT #-1 -> USINT #255) | |
| USINT | - | X | | |
| INT | - | X | | |
| UINT | - | X | | |
| DINT | - | X | | |
| UDINT | - | X | | |
| LINT | - | X | | |
| REAL | - | X | The bit pattern of the source value is converted and transferred to the destination data type. (for example, value conversion from LINT #-1 -> REAL #-1.0, but there is a loss in accuracy for numbers with an absolute value greater than 8 388 608) | |
| LREAL | - | X | The bit pattern of the source value is converted and transferred to the destination data type. (for example, value conversion from LINT #-1 -> REAL #-1.0, but there is a loss in accuracy for numbers with an absolute value greater than 9 007 199 254 740 992) | |
| ULINT | TIME | - | - | No implicit conversion |
| LTIME | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. (duration in nanoseconds) | |
| S5TIME | - | - | No implicit conversion | |
| LDT | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. (nanoseconds since 1/1/1970) | |
| DTL | - | - | No implicit conversion | |
| DT | - | - | | |
| DATE | - | - | | |
| TOD | - | - | | |
| LTOD | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| STRING | - | - | No implicit conversion | |
| WSTRING | - | - | | |
| CHAR | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | |
| WCHAR | - | X | | |
| x: Conversion possible -: Conversion not possible | | | | |
See also

Activate or deactivate IEC check (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) ULINT (64-bit integers) (S7-1500, S7-1200 G2) Explicit conversion of ULINT (S7-1500, S7-1200 G2)

Floating-point numbers (S7-1500, S7-1200 G2) Implicit conversion of REAL (S7-1500, S7-1200 G2)
| Implicit conversion of REAL |
|---|
Implicit conversion options

The following table shows the options for the implicit conversion of REAL data type:

| Source | Destination | With IEC check | Without IEC check | Explanation |
|---|---|---|---|---|
| REAL | BOOL | - | - | No implicit conversion |
| BYTE | - | - | | |
| WORD | - | - | | |
| DWORD | - | X | The bit pattern of the source value is transferred unchanged to the destination data type. | |
| LWORD | - | - | No implicit conversion | |
| SINT | - | X | The bit pattern of the source value is rounded off and converted and transferred to the destination data type. (For example, rounding off and value conversion of REAL #2.5 -> INT #2, or negative numbers REAL #-2.5 -> INT #-2 -> USINT #254. With an overflow, the remainder is determined REAL #305.5 -> INT #306 -> USINT #50) | |
| USINT | - | X | | |
| INT | - | X | | |
| UINT | - | X | | |
| DINT | - | X | | |
| UDINT | - | X | | |
| LINT | - | X | | |
| ULINT | - | X | | |
| LREAL | X | X | The value is transferred to the destination data type. | |
| TIME | - | - | No implicit conversion | |
| LTIME | - | - | | |
| S5TIME | - | - | | |
| LDT | - | - | | |
| REAL | DTL | - | - | No implicit conversion |
| DT | - | - | | |
| DATE | - | - | | |
| TOD | - | - | | |
| LTOD | - | - | | |
| STRING | - | - | | |
| WSTRING | - | - | | |
| CHAR | - | - | | |
| WCHAR | - | - | | |
| x: Conversion possible -: Conversion not possible | | | | |
See also

Activate or deactivate IEC check (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) REAL Explicit conversion of REAL (S7-1500, S7-1200 G2)

Implicit conversion of LREAL (S7-1500, S7-1200 G2)
| Implicit conversion of LREAL |
|---|
Implicit conversion options

The following table shows the options for the implicit conversion of LREAL data type:

| Source | Destination | With IEC check | Without IEC check | Explanation |
|---|---|---|---|---|
| LREAL | BOOL | - | - | No implicit conversion |
| BYTE | - | - | | |
| WORD | - | - | | |
| DWORD | - | - | | |
| LWORD | - | X | The bit pattern of the source value is transferred unchanged to the destination data type. | |
| SINT | - | X | The bit pattern of the source value is rounded off and converted and transferred to the destination data type. (For example, rounding off and value conversion of LREAL #2.5 -> INT #2, or negative numbers LREAL #-2.5 -> INT #-2 -> USINT #254. With an overflow, the remainder is determined LREAL #305.5 -> INT #306 -> USINT #50) | |
| USINT | - | X | | |
| INT | - | X | | |
| UINT | - | X | | |
| DINT | - | X | | |
| UDINT | - | X | | |
| LINT | - | X | | |
| ULINT | - | X | | |
| REAL | - | X | The value is transferred to the destination data type. | |
| TIME | - | - | No implicit conversion | |
| LTIME | - | - | | |
| S5TIME | - | - | | |
| LDT | - | - | | |
| LREAL | DTL | - | - | No implicit conversion |
| DT | - | - | | |
| DATE | - | - | | |
| TOD | - | - | | |
| LTOD | - | - | | |
| STRING | - | - | | |
| WSTRING | - | - | | |
| CHAR | - | - | | |
| WCHAR | - | - | | |
| x: Conversion possible -: Conversion not possible | | | | |
See also

Activate or deactivate IEC check (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) LREAL (S7-1200, S7-1500, S7-1200 G2) Explicit conversion of LREAL (S7-1500, S7-1200 G2)

Timers (S7-1500, S7-1200 G2) Implicit conversion of S5TIME (S7-1500, S7-1200 G2)
| Implicit conversion of S5TIME |
|---|
Implicit conversion options

The following table shows the options for the implicit conversion of data type S5TIME:

| Source | Destination | With IEC check | Without IEC check | Explanation |
|---|---|---|---|---|
| S5TIME | BOOL | - | - | No implicit conversion |
| BYTE | - | - | | |
| WORD | - | X | The bit pattern of the source value is transferred unchanged to the destination data type. The result of conversion shows the duration in milliseconds. | |
| DWORD | - | - | No implicit conversion | |
| LWORD | - | - | | |
| SINT | - | - | | |
| USINT | - | - | | |
| INT | - | - | | |
| UINT | - | - | | |
| DINT | - | - | | |
| UDINT | - | - | | |
| LINT | - | - | | |
| ULINT | - | - | | |
| REAL | - | - | | |
| LREAL | - | - | | |
| TIME | - | - | | |
| LTIME | - | - | | |
| LDT | - | - | | |
| S5TIME | DTL | - | - | No implicit conversion |
| DT | - | - | | |
| DATE | - | - | | |
| TOD | - | - | | |
| LTOD | - | - | | |
| STRING | - | - | | |
| WSTRING | - | - | | |
| CHAR | - | - | | |
| WCHAR | - | - | | |
| x: Conversion possible -: Conversion not possible | | | | |
See also

Activate or deactivate IEC check (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) S5TIME (duration) (S7-300, S7-400, S7-1500) Explicit conversion of S5TIME (S7-1500, S7-1200 G2)

Implicit conversion of TIME (S7-1500, S7-1200 G2)
| Implicit conversion of TIME |
|---|
Implicit conversion options

The following table shows the options for the implicit conversion of TIME data type:

| Source | Destination | With IEC check | Without IEC check | Explanation |
|---|---|---|---|---|
| TIME | BOOL | - | - | No implicit conversion |
| BYTE | - | - | | |
| WORD | - | - | | |
| DWORD | - | X | The bit pattern of the source value is transferred unchanged to the destination data type. The result of conversion shows the duration in milliseconds. | |
| LWORD | - | - | No implicit conversion | |
| SINT | - | - | | |
| USINT | - | - | | |
| INT | - | - | | |
| UINT | - | - | | |
| DINT | - | X | The bit pattern of the source value is transferred unchanged to the destination data type. The result of conversion shows the duration in milliseconds. | |
| UDINT | - | X | | |
| LINT | - | - | No implicit conversion | |
| ULINT | - | - | | |
| REAL | - | - | | |
| LREAL | - | - | | |
| S5TIME | - | - | | |
| LTIME | X | X | The bit pattern of the source value is transferred unchanged to the destination data type. The result of the conversion shows the duration in nanoseconds. (1 ms = 1 000 000 ns) | |
| LDT | - | - | No implicit conversion | |
| DTL | - | - | | |
| DT | - | - | | |
| DATE | - | - | | |
| TOD | - | X | If the source value is between 0 s and 84599.999 s, the bit pattern of the source value is transferred unchanged to the destination data type. (Display in nanoseconds) The target value remains unchanged otherwise. The result of the conversion shows the time that has passed since midnight. | |
| LTOD | - | - | No implicit conversion | |
| STRING | - | - | | |
| WSTRING | - | - | | |
| CHAR | - | - | | |
| WCHAR | - | - | | |
| x: Conversion possible -: Conversion not possible | | | | |
See also

Activate or deactivate IEC check (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) TIME (IEC time) Explicit conversion of TIME (S7-1500, S7-1200 G2)

Implicit conversion of LTIME (S7-1500, S7-1200 G2)
| Implicit conversion of LTIME |
|---|
Implicit conversion options

The following table shows the options for the implicit conversion of LTIME data type:

| Source | Destination | With IEC check | Without IEC check | Explanation |
|---|---|---|---|---|
| LTIME | BOOL | - | - | No implicit conversion |
| BYTE | - | - | | |
| WORD | - | - | | |
| DWORD | - | - | | |
| LWORD | - | X | The bit pattern of the source value is transferred unchanged to the destination data type. The result of the conversion shows the duration in nanoseconds. | |
| SINT | - | - | No implicit conversion | |
| USINT | - | - | | |
| INT | - | - | | |
| UINT | - | - | | |
| DINT | - | - | | |
| UDINT | - | - | | |
| LINT | - | X | The bit pattern of the source value is transferred unchanged to the destination data type. The result of the conversion shows the duration in nanoseconds. | |
| ULINT | - | X | | |
| REAL | - | - | No implicit conversion | |
| LREAL | - | - | | |
| S5TIME | - | - | | |
| TIME | - | X | If the source value is outside the value range of the destination data type, the target value remains unchanged. (0.123456789 s becomes 0.123 s) | |
| LDT | - | X | The bit pattern of the source value is transferred unchanged to the destination data type. The result of the conversion shows the duration in nanoseconds since 1/1/1970. | |
| DTL | - | - | No implicit conversion | |
| DT | - | - | | |
| DATE | - | - | | |
| TOD | - | - | | |
| LTOD | - | X | The bit pattern of the source value is transferred unchanged to the destination data type. The result of the conversion shows the duration in nanoseconds since 1/1/1970. | |
| STRING | - | - | No implicit conversion | |
| WSTRING | - | - | | |
| CHAR | - | - | | |
| WCHAR | - | - | | |
| x: Conversion possible -: Conversion not possible | | | | |
See also

Activate or deactivate IEC check (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) LTIME (IEC time) (S7-1500, S7-1200 G2) Explicit conversion of LTIME (S7-1500, S7-1200 G2)

Date and time-of-day (S7-1500, S7-1200 G2) Implicit conversion of DT (S7-1500, S7-1200 G2)
| Implicit conversion of DT |
|---|
Implicit conversion options

The following table shows the options for the implicit conversion of DT data type:

| Source | Destination | With IEC check | Without IEC check | Explanation |
|---|---|---|---|---|
| DT | BOOL | - | - | No implicit conversion |
| BYTE | - | - | | |
| WORD | - | - | | |
| DWORD | - | - | | |
| LWORD | - | - | | |
| SINT | - | - | | |
| USINT | - | - | | |
| INT | - | - | | |
| UINT | - | - | | |
| DINT | - | - | | |
| UDINT | - | - | | |
| LINT | - | - | | |
| ULINT | - | - | | |
| REAL | - | - | | |
| LREAL | - | - | | |
| TIME | - | - | | |
| LTIME | - | - | | |
| S5TIME | - | - | | |
| LDT | X | X | The source value is transferred unchanged with the same value to the destination data type. (12/24/2012 14:30 remains 12/24/2012 14:30) | |
| DTL | X | X | | |
| DATE | - | - | No implicit conversion | |
| TOD | - | - | | |
| LTOD | - | - | | |
| STRING | - | - | | |
| WSTRING | - | - | | |
| CHAR | - | - | | |
| WCHAR | - | - | | |
| x: Conversion possible -: Conversion not possible | | | | |
See also

Activate or deactivate IEC check (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) DATE_AND_TIME (date and time of day) (S7-1500) Explicit conversion of DT (S7-1500, S7-1200 G2)

Implicit conversion of LDT (S7-1500, S7-1200 G2)
| Implicit conversion of LDT |
|---|
Implicit conversion options

The following table shows the options for the implicit conversion of LDT data type:

| Source | Destination | With IEC check | Without IEC check | Explanation |
|---|---|---|---|---|
| LDT | BOOL | - | - | No implicit conversion |
| BYTE | - | - | | |
| WORD | - | - | | |
| DWORD | - | - | | |
| LWORD | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. (nanoseconds since 1/1/1970) | |
| SINT | - | - | No implicit conversion | |
| USINT | - | - | | |
| INT | - | - | | |
| UINT | - | - | | |
| DINT | - | - | | |
| UDINT | - | - | | |
| LINT | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. (nanoseconds since 1/1/1970) | |
| ULINT | - | X | | |
| REAL | - | - | No implicit conversion | |
| LREAL | - | - | | |
| TIME | - | - | | |
| LTIME | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. (nanoseconds since 1/1/1970) | |
| S5TIME | - | - | No implicit conversion | |
| DT | - | X | The bit pattern of the source value is converted with a loss in accuracy to the destination data type. (12/24/2012 12:34:56.123456789 becomes 12/24/2012 12:34:56.123) | |
| DTL | X | X | The source value is transferred unchanged with the same value to the destination data type. (12/24/2012 14:30 remains 12/24/2012 14:30) | |
| DATE | - | - | No implicit conversion | |
| TOD | - | - | | |
| LTOD | - | - | | |
| STRING | - | - | | |
| WSTRING | - | - | | |
| CHAR | - | - | | |
| WCHAR | - | - | | |
| x: Conversion possible -: Conversion not possible | | | | |
See also

Activate or deactivate IEC check (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) Explicit conversion of LDT (S7-1500, S7-1200 G2) LDT (DATE_AND_LTIME) (S7-1500, S7-1200 G2)

Implicit conversion of DTL (S7-1500, S7-1200 G2)
| Implicit conversion of DTL |
|---|
Implicit conversion options

The following table shows the options for the implicit conversion of DTL data type:

| Source | Destination | With IEC check | Without IEC check | Explanation |
|---|---|---|---|---|
| DTL | BOOL | - | - | No implicit conversion |
| BYTE | - | - | | |
| WORD | - | - | | |
| DWORD | - | - | | |
| LWORD | - | - | | |
| SINT | - | - | | |
| USINT | - | - | | |
| INT | - | - | | |
| UINT | - | - | | |
| DINT | - | - | | |
| UDINT | - | - | | |
| LINT | - | - | | |
| ULINT | - | - | | |
| REAL | - | - | | |
| LREAL | - | - | | |
| TIME | - | - | | |
| LTIME | - | - | | |
| S5TIME | - | - | | |
| LDT | X | X | The source value is transferred unchanged with the same value to the destination data type. (12/24/2012 14:30 remains 12/24/2012 14:30) | |
| DT | - | X | The bit pattern of the source value is converted with a loss in accuracy to the destination data type. (12/24/2012 12:34:56.123456789 becomes 12/24/2012 12:34:56.123) | |
| DATE | - | - | No implicit conversion | |
| TOD | - | - | | |
| LTOD | - | - | | |
| STRING | - | - | | |
| WSTRING | - | - | | |
| CHAR | - | - | | |
| WCHAR | - | - | | |
| x: Conversion possible -: Conversion not possible | | | | |
See also

Activate or deactivate IEC check (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) DTL (S7-1200, S7-1500, S7-1200 G2) Explicit conversion of DTL (S7-1500, S7-1200 G2)

Implicit conversion of DATE (S7-1500, S7-1200 G2)
| Implicit conversion of DATE |
|---|
Implicit conversion options

The following table shows the options for the implicit conversion of data type DATE:

| Source | Destination | With IEC check | Without IEC check | Explanation |
|---|---|---|---|---|
| DATE | BOOL | - | - | No implicit conversion |
| BYTE | - | - | | |
| WORD | - | X | The bit pattern of the source value is transferred unchanged to the destination data type. The result of conversion is equal to the number of days since 01/01/1990. | |
| DWORD | - | - | No implicit conversion | |
| LWORD | - | - | | |
| SINT | - | - | | |
| USINT | - | - | | |
| INT | - | X | The bit pattern of the source value is transferred unchanged to the destination data type. The result of conversion is equal to the number of days since 01/01/1990. | |
| UINT | - | X | | |
| DINT | - | - | No implicit conversion | |
| UDINT | - | - | | |
| LINT | - | - | | |
| ULINT | - | - | | |
| REAL | - | - | | |
| LREAL | - | - | | |
| TIME | - | - | | |
| LTIME | - | - | | |
| S5TIME | - | - | | |
| DATE | LDT | - | - | No implicit conversion |
| DT | - | - | | |
| DTL | - | - | | |
| TOD | - | - | | |
| LTOD | - | - | | |
| STRING | - | - | | |
| WSTRING | - | - | | |
| CHAR | - | - | | |
| WCHAR | - | - | | |
| x: Conversion possible -: Conversion not possible | | | | |
See also

Activate or deactivate IEC check (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) DATE Explicit conversion of DATE (S7-1500, S7-1200 G2)

Implicit conversion of TOD (S7-1500, S7-1200 G2)
| Implicit conversion of TOD |
|---|
Implicit conversion options

The following table shows the options for the implicit conversion of TOD data type:

| Source | Destination | With IEC check | Without IEC check | Explanation |
|---|---|---|---|---|
| TOD | BOOL | - | - | No implicit conversion |
| BYTE | - | - | | |
| WORD | - | - | | |
| DWORD | - | X | The bit pattern of the source value is transferred unchanged to the destination data type. The result of the conversion corresponds to the number of milliseconds since the start of day (0:00). | |
| LWORD | - | - | No implicit conversion | |
| SINT | - | - | | |
| USINT | - | - | | |
| INT | - | - | | |
| UINT | - | - | | |
| DINT | - | X | The bit pattern of the source value is transferred unchanged to the destination data type. The result of the conversion corresponds to the number of milliseconds since the start of day (0:00). | |
| UDINT | - | X | | |
| LINT | - | - | No implicit conversion | |
| ULINT | - | - | | |
| REAL | - | - | | |
| LREAL | - | - | | |
| TIME | - | X | The bit pattern of the source value is transferred unchanged to the destination data type. The result of the conversion corresponds to the number of milliseconds since the start of day (0:00). | |
| LTIME | - | - | No implicit conversion | |
| S5TIME | - | - | | |
| LDT | - | - | | |
| DT | - | - | | |
| DTL | - | - | | |
| DATE | - | - | | |
| LTOD | X | X | The source value is transferred unchanged with the same value to the destination data type. (12:34:56.123 becomes 12:34:56.123000000) | |
| STRING | - | - | No implicit conversion | |
| WSTRING | - | - | | |
| CHAR | - | - | | |
| WCHAR | - | - | | |
| x: Conversion possible -: Conversion not possible | | | | |
See also

Activate or deactivate IEC check (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) TIME_OF_DAY (TOD) Explicit conversion of TOD (S7-1500, S7-1200 G2)

Implicit conversion of LTOD (S7-1500, S7-1200 G2)
| Implicit conversion of LTOD |
|---|
Implicit conversion options

The following table shows the options for the implicit conversion of LTOD data type:

| Source | Destination | With IEC check | Without IEC check | Explanation |
|---|---|---|---|---|
| LTOD | BOOL | - | - | No implicit conversion |
| BYTE | - | - | | |
| WORD | - | - | | |
| DWORD | - | - | | |
| LWORD | - | X | The bit pattern of the source value is transferred unchanged to the destination data type. The result of the conversion corresponds to the number of nanoseconds since the start of day (0:00 hrs). | |
| SINT | - | - | No implicit conversion | |
| USINT | - | - | | |
| INT | - | - | | |
| UINT | - | - | | |
| DINT | - | - | | |
| UDINT | - | - | | |
| LINT | - | X | The bit pattern of the source value is transferred unchanged to the destination data type. The result of the conversion corresponds to the number of nanoseconds since the start of day (0:00 hrs). | |
| ULINT | - | X | | |
| REAL | - | - | No implicit conversion | |
| LREAL | - | - | | |
| TIME | - | - | | |
| LTOD | LTIME | - | X | The bit pattern of the source value is transferred unchanged to the destination data type. The result of the conversion corresponds to the number of nanoseconds since the start of day (0:00 hrs). |
| S5TIME | - | - | No implicit conversion | |
| LDT | - | - | | |
| DT | - | - | | |
| DTL | - | - | | |
| DATE | - | - | | |
| TOD | - | X | The source value is transferred unchanged with the same value rounded off to the destination data type. (12:34:56.123456789 becomes 12:34:56.123) | |
| STRING | - | - | No implicit conversion | |
| WSTRING | - | - | | |
| CHAR | - | - | | |
| WCHAR | - | - | | |
| x: Conversion possible -: Conversion not possible | | | | |
See also

Activate or deactivate IEC check (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) Explicit conversion of LTOD (S7-1500, S7-1200 G2) LTOD (LTIME_OF_DAY) (S7-1500, S7-1200 G2)

String (S7-1500, S7-1200 G2) Implicit conversion of CHAR (S7-1500, S7-1200 G2)
| Implicit conversion of CHAR |
|---|
Implicit conversion options

The following table shows the options for the implicit conversion of CHAR data type:

| Source | Destination | With IEC check | Without IEC check | Explanation |
|---|---|---|---|---|
| CHAR | BOOL | - | - | No implicit conversion |
| BYTE | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. The remaining bits are filled from the left with "0". | |
| WORD | - | X | | |
| DWORD | - | X | | |
| LWORD | - | X | | |
| SINT | - | X | | |
| USINT | - | X | | |
| INT | - | X | | |
| UINT | - | X | | |
| DINT | - | X | | |
| UDINT | - | X | | |
| LINT | - | X | | |
| ULINT | - | X | | |
| REAL | - | - | No implicit conversion | |
| LREAL | - | - | | |
| TIME | - | - | | |
| LTIME | - | - | | |
| S5TIME | - | - | | |
| LDT | - | - | | |
| DTL | - | - | | |
| DT | - | - | | |
| DATE | - | - | | |
| TOD | - | - | | |
| LTOD | - | - | | |
| WCHAR | - | - | | |
| STRING | X | X | The STRING is shortened to length 1 and includes the character. | |
| WSTRING | - | - | No implicit conversion | |
| x: Conversion possible -: Conversion not possible | | | | |
See also

Activate or deactivate IEC check (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) CHAR Explicit conversion of CHAR (S7-1500, S7-1200 G2)

Implicit conversion of WCHAR (S7-1500, S7-1200 G2)
| Implicit conversion of WCHAR |
|---|
Implicit conversion options

The following table shows the options for the implicit conversion of WCHAR data type:

| Source | Destination | With IEC check | Without IEC check | Explanation |
|---|---|---|---|---|
| WCHAR | BOOL | - | - | No implicit conversion |
| BYTE | - | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. The remaining bits are filled from the left with "0". | |
| WORD | - | X | | |
| DWORD | - | X | | |
| LWORD | - | X | | |
| SINT | - | X | | |
| USINT | - | X | | |
| INT | - | X | | |
| UINT | - | X | | |
| DINT | - | X | | |
| UDINT | - | X | | |
| LINT | - | X | | |
| ULINT | - | X | | |
| REAL | - | - | No implicit conversion | |
| LREAL | - | - | | |
| TIME | - | - | | |
| LTIME | - | - | | |
| S5TIME | - | - | | |
| LDT | - | - | | |
| DTL | - | - | | |
| DT | - | - | | |
| DATE | - | - | | |
| TOD | - | - | | |
| LTOD | - | - | | |
| CHAR | - | - | | |
| STRING | - | - | | |
| WSTRING | X | X | The WSTRING is shortened to length 1 and includes the character. | |
| x: Conversion possible -: Conversion not possible | | | | |
See also

Activate or deactivate IEC check (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) WCHAR (S7-1200, S7-1500, S7-1200 G2) Explicit conversion of WCHAR (S7-1500, S7-1200 G2)

Implicit conversion of STRING (S7-1500, S7-1200 G2)
| Implicit conversion of STRING |
|---|
Implicit conversion options

The following table shows the options for the implicit conversion of STRING data type:

| Source | Destination | With IEC check | Without IEC check | Explanation |
|---|---|---|---|---|
| STRING | BOOL | - | - | No implicit conversion |
| BYTE | - | - | | |
| WORD | - | - | | |
| DWORD | - | - | | |
| LWORD | - | - | | |
| SINT | - | - | | |
| USINT | - | - | | |
| INT | - | - | | |
| UINT | - | - | | |
| DINT | - | - | | |
| UDINT | - | - | | |
| LINT | - | - | | |
| ULINT | - | - | | |
| REAL | - | - | | |
| LREAL | - | - | | |
| TIME | - | - | | |
| LTIME | - | - | | |
| S5TIME | - | - | | |
| LDT | - | - | | |
| DTL | - | - | | |
| DT | - | - | | |
| DATE | - | - | | |
| TOD | - | - | | |
| LTOD | - | - | | |
| CHAR | - | X | The first character of the STRING is returned if the STRING includes one or more characters. Otherwise, the character is output with coding $00. | |
| WCHAR | - | - | No implicit conversion | |
| WSTRING | - | - | | |
| x: Conversion possible -: Conversion not possible | | | | |
See also

Activate or deactivate IEC check (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) STRING Explicit conversion of STRING (S7-1500, S7-1200 G2)

Implicit conversion of WSTRING (S7-1500, S7-1200 G2)
| Implicit conversion of WSTRING |
|---|
Implicit conversion options

The following table shows the options for the implicit conversion of WSTRING data type:

| Source | Destination | With IEC check | Without IEC check | Explanation |
|---|---|---|---|---|
| WSTRING | BOOL | - | - | No implicit conversion |
| BYTE | - | - | | |
| WORD | - | - | | |
| DWORD | - | - | | |
| LWORD | - | - | | |
| SINT | - | - | | |
| USINT | - | - | | |
| INT | - | - | | |
| UINT | - | - | | |
| DINT | - | - | | |
| UDINT | - | - | | |
| LINT | - | - | | |
| ULINT | - | - | | |
| REAL | - | - | | |
| LREAL | - | - | | |
| TIME | - | - | | |
| LTIME | - | - | | |
| S5TIME | - | - | | |
| LDT | - | - | | |
| DTL | - | - | | |
| DT | - | - | | |
| DATE | - | - | | |
| TOD | - | - | | |
| LTOD | - | - | | |
| CHAR | - | - | | |
| WCHAR | - | X | The first character of the WSTRING is returned if the WSTRING includes one or more characters. Otherwise, the character is output with coding $0000. | |
| STRING | - | - | No implicit conversion | |
| x: Conversion possible -: Conversion not possible | | | | |
See also

Activate or deactivate IEC check (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) WSTRING (S7-1200, S7-1500, S7-1200 G2) Explicit conversion of WSTRING (S7-1500, S7-1200 G2)


# Explicit conversions (S7-1500, S7-1200 G2)

Binary numbers (S7-1500, S7-1200 G2) Explicit conversion of BOOL (S7-1500, S7-1200 G2)
| Explicit conversion of BOOL |
|---|
Options for explicit conversion

The following table shows the options and instructions for the explicit conversion of the BOOL data type:

| Source | Destination | Conversion | Explanation | Mnemonics of the instruction |
|---|---|---|---|---|
| BOOL | BYTE | X | Only the LSB (Least Significant Bit) is set in the destination data type. The enable output ENO is always "1". | BOOL_TO_BYTE |
| WORD | X | BOOL_TO_WORD | | |
| DWORD | X | BOOL_TO_DWORD | | |
| LWORD | X | BOOL_TO_LWORD | | |
| SINT | X | BOOL_TO_SINT | | |
| USINT | X | BOOL_TO_USINT | | |
| INT | X | BOOL_TO_INT | | |
| UINT | X | BOOL_TO_UINT | | |
| DINT | X | BOOL_TO_DINT | | |
| UDINT | X | BOOL_TO_UDINT | | |
| LINT | X | BOOL_TO_LINT | | |
| ULINT | X | BOOL_TO_ULINT | | |
| REAL | - | No explicit conversion | - | |
| LREAL | - | - | | |
| TIME | - | - | | |
| LTIME | - | - | | |
| S5TIME | - | - | | |
| LDT | - | - | | |
| DT | - | - | | |
| DTL | - | - | | |
| BOOL | TOD | - | No explicit conversion | - |
| LTOD | - | - | | |
| DATE | - | - | | |
| STRING | - | - | | |
| WSTRING | - | - | | |
| CHAR | - | - | | |
| WCHAR | - | - | | |
| x: Conversion possible - : Conversion not possible | | | | |
See also

Overview of data type conversion (S7-1500, S7-1200 G2) Implicit conversion of BOOL (S7-1500, S7-1200 G2) BOOL (bit)

Bit strings (S7-1500, S7-1200 G2) Explicit conversion of BYTE (S7-1500, S7-1200 G2)
| Explicit conversion of BYTE |
|---|
Options for explicit conversion

The following table shows the options and instructions for the explicit conversion of the BYTE data type:

| Source | Destination | Conversion | Explanation | Mnemonics of the instruction |
|---|---|---|---|---|
| BYTE1) | BOOL | X | The following possibilities can occur: If the source is "0", the destination data type is also "0" and the enable output ENO "1". If only the LSB (Least Significant Bit) "1" is set in the source value, the destination data type is also "1" and the enable output ENO "1". If bits are not equal to LSB in the source value, the destination data type is set according to LSB and the enable output ENO is "0". | BYTE_TO_BOOL |
| WORD1) | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | BYTE_TO_WORD | |
| DWORD1) | X | BYTE_TO_DWORD | | |
| LWORD1) | X | BYTE_TO_LWORD | | |
| SINT | X | BYTE_TO_SINT | | |
| USINT | X | BYTE_TO_USINT | | |
| INT | X | BYTE_TO_INT | | |
| UINT | X | BYTE_TO_UINT | | |
| DINT | X | BYTE_TO_DINT | | |
| BYTE1) | UDINT | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | BYTE_TO_UDINT |
| LINT | X | BYTE_TO_LINT | | |
| ULINT | X | BYTE_TO_ULINT | | |
| REAL | - | No explicit conversion | - | |
| LREAL | - | - | | |
| TIME | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | BYTE_TO_TIME | |
| LTIME | X | BYTE_TO_LTIME | | |
| S5TIME | - | No explicit conversion | - | |
| LDT | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | BYTE_TO_LDT | |
| DT | - | No explicit conversion | - | |
| DTL | - | - | | |
| TOD | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | BYTE_TO_TOD | |
| LTOD | X | BYTE_TO_LTOD | | |
| DATE | X | BYTE_TO_DATE | | |
| STRING | - | No explicit conversion | - | |
| WSTRING | - | - | | |
| CHAR | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | BYTE_TO_CHAR | |
| WCHAR | X | BYTE_TO_WCHAR | | |
| x: Conversion possible - : Conversion not possible 1) Bit strings (BYTE, WORD, DWORD, LWORD) are interpreted as an unsigned integer with the same bit length. The data type BYTE is interpreted as USINT, WORD as UINT, DWORD as UDINT and LWORD as ULINT. | | | | |
See also

Overview of data type conversion (S7-1500, S7-1200 G2) Implicit conversion of BYTE (S7-1500, S7-1200 G2) BYTE

Explicit conversion of WORD (S7-1500, S7-1200 G2)
| Explicit conversion of WORD |
|---|
Options for explicit conversion

The following table shows the options and instructions for the explicit conversion of the WORD data type:

| Source | Destination | Conversion | Explanation | Mnemonics of the instruction |
|---|---|---|---|---|
| WORD1) | BOOL | X | The following possibilities can occur: If the source is "0", the destination data type is also "0" and the enable output ENO "1". If only the LSB (Least Significant Bit) "1" is set in the source value, the destination data type is also "1" and the enable output ENO "1". If bits are not equal to LSB in the source value, the destination data type is set according to LSB and the enable output ENO is "0". | WORD_TO_BOOL |
| BYTE1) | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | WORD_TO_BYTE | |
| DWORD1) | X | WORD_TO_DWORD | | |
| LWORD1) | X | WORD_TO_LWORD | | |
| SINT | X | ENO = TRUE #sint1 := WORD_TO_SINT(16#FFFF); // -1 to #sint1 := WORD_TO_SINT(16#FF80); // -128 #sint1 := WORD_TO_SINT(16#0); // 0 to #sint1 := WORD_TO_SINT(16#007F); // 127 ENO = FALSE #sint1 := WORD_TO_SINT(16#FF7F); // -129 to #sint1 := WORD_TO_SINT(16#8000); // -32768 #sint1 := WORD_TO_SINT(16#0080); // 128 to #sint1 := WORD_TO_SINT(16#7FFF); // 32767 | WORD_TO_SINT | |
| USINT | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | WORD_TO_USINT | |
| INT | X | WORD_TO_INT | | |
| UINT | X | WORD_TO_UINT | | |
| DINT | X | WORD_TO_DINT | | |
| UDINT | X | WORD_TO_UDINT | | |
| LINT | X | WORD_TO_LINT | | |
| ULINT | X | WORD_TO_ULINT | | |
| REAL | - | No explicit conversion | - | |
| LREAL | - | - | | |
| TIME | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | WORD_TO_TIME | |
| LTIME | X | WORD_TO_LTIME | | |
| S5TIME | X | WORD_TO_S5TIME | | |
| LDT | X | WORD_TO_LDT | | |
| DT | - | No explicit conversion | - | |
| DTL | - | - | | |
| TOD | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | WORD_TO_TOD | |
| LTOD | X | WORD_TO_LTOD | | |
| DATE | X | WORD_TO_DATE | | |
| STRING | - | No explicit conversion | - | |
| WSTRING | - | - | | |
| CHAR | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | WORD_TO_CHAR | |
| WCHAR | X | WORD_TO_WCHAR | | |
| WORD_BCD16 | INT | X | The value to be converted has data type WORD and is accepted as a BCD-coded value between -999 and +999. The result is available after conversion as an integer (in binary notation) of the type INT. A real conversion takes place. If the bit pattern includes an invalid tetrad, a synchronous error is not triggered but only the status bit OV is set instead. | WORD_BCD16_TO_INT |
| BCD16 | INT | X | BCD16_TO_INT | |
| x: Conversion possible - : Conversion not possible 1) Bit strings (BYTE, WORD, DWORD, LWORD) are interpreted as an unsigned integer with the same bit length. The data type BYTE is interpreted as USINT, WORD as UINT, DWORD as UDINT and LWORD as ULINT. | | | | |
See also

Implicit conversion of WORD (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) WORD

Explicit conversion of DWORD (S7-1500, S7-1200 G2)
| Explicit conversion of DWORD |
|---|
Options for explicit conversion

The following table shows the options and instructions for the explicit conversion of the DWORD data type:

| Source | Destination | Conversion | Explanation | Mnemonics of the instruction |
|---|---|---|---|---|
| DWORD1) | BOOL | X | The following possibilities can occur: If the source is "0", the destination data type is also "0" and the enable output ENO "1". If only the LSB (Least Significant Bit) "1" is set in the source value, the destination data type is also "1" and the enable output ENO "1". If bits are not equal to LSB in the source value, the destination data type is set according to LSB and the enable output ENO is "0". | DWORD_TO_BOOL |
| BYTE1) | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | DWORD_TO_BYTE | |
| WORD1) | X | DWORD_TO_WORD | | |
| LWORD1) | X | DWORD_TO_LWORD | | |
| SINT | X | ENO = TRUE #sint1 := DWORD_TO_SINT(16#FFFF_FFFF); // -1 to #sint1 := DWORD_TO_SINT(16#FFFF_FF80); // -128 #sint1 := DWORD_TO_SINT(16#0); // 0 to #sint1 := DWORD_TO_SINT(16#0000_007F); // 127 ENO = FALSE #sint1 := DWORD_TO_SINT(16#FFFF_FF7F); // -129 #sint1 := DWORD_TO_SINT(16#8000_0000); // -2147483648 #sint1 := DWORD_TO_SINT(16#0000_0080); // 128 to #sint1 := DWORD_TO_SINT(16#7FFF_FFFF); // 2147483647 | DWORD_TO_SINT | |
| USINT | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | DWORD_TO_USINT | |
| INT | X | ENO = TRUE #int1 := DWORD_TO_INT(16#FFFF_FFFF); // -1 to #int1 := DWORD_TO_INT(16#FFFF_8000); // -32768 #int1 := DWORD_TO_INT(16#0); // 0 to #int1 := DWORD_TO_INT(16#0000_7FFF); // 32767 ENO = FALSE #int1 := DWORD_TO_INT(16#FFFF_7FFF); // -32769 #int1 := DWORD_TO_INT(16#8000_0000); // -2147483648 #int1 := DWORD_TO_INT(16#8000); // 32768 to #int1 := DWORD_TO_INT(16#7FFF_FFFF); // 2147483647 | DWORD_TO_INT | |
| UINT | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. If no errors occur during the conversion, the signal state of ENO = 1; if an error occurs during processing, the signal state of ENO = 0. | DWORD_TO_UINT | |
| DINT | X | DWORD_TO_DINT | | |
| UDINT | X | DWORD_TO_UDINT | | |
| LINT | X | DWORD_TO_LINT | | |
| ULINT | X | DWORD_TO_ULINT | | |
| REAL | X | DWORD_TO_REAL | | |
| LREAL | - | No explicit conversion | - | |
| TIME | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | DWORD_TO_TIME | |
| LTIME | X | DWORD_TO_LTIME | | |
| S5TIME | - | No explicit conversion | - | |
| LDT | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | DWORD_TO_LDT | |
| DT | - | No explicit conversion | - | |
| DTL | - | - | | |
| TOD | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | DWORD_TO_TOD | |
| LTOD | X | DWORD_TO_LTOD | | |
| DATE | X | DWORD_TO_DATE | | |
| STRING | - | No explicit conversion | - | |
| WSTRING | - | - | | |
| CHAR | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | DWORD_TO_CHAR | |
| WCHAR | X | DWORD_TO_WCHAR | | |
| DWORD_BCD32 | DINT | X | The value to be converted has data type DWORD and is accepted as a BCD-coded value between -9999999 and +9999999. The result is available after conversion as an integer (in binary notation) of the type DINT. A real conversion takes place. If the bit pattern includes an invalid tetrad, a synchronous error is not triggered but only the status bit OV is set instead. | DWORD_BCD32_TO_DINT |
| BCD32 | DINT | X | BCD32_TO_DINT | |
| x: Conversion possible - : Conversion not possible 1) Bit strings (BYTE, WORD, DWORD, LWORD) are interpreted as an unsigned integer with the same bit length. The data type BYTE is interpreted as USINT, WORD as UINT, DWORD as UDINT and LWORD as ULINT. | | | | |
See also

Implicit conversion of DWORD (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) DWORD

Explicit conversion of LWORD (S7-1500, S7-1200 G2)
| Explicit conversion of LWORD |
|---|
Options for explicit conversion

The following table shows the options and instructions for the explicit conversion of the LWORD data type:

| Source | Destination | Conversion | Explanation | Mnemonics of the instruction |
|---|---|---|---|---|
| LWORD1) | BOOL | X | The following possibilities can occur: If the source is "0", the destination data type is also "0" and the enable output ENO "1". If only the LSB (Least Significant Bit) "1" is set in the source value, the destination data type is also "1" and the enable output ENO "1". If bit is not equal to LSB in the source value, the destination data type is set according to LSB and the enable output ENO is "0". | LWORD_TO_BOOL |
| BYTE1) | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | LWORD_TO_BYTE | |
| WORD1) | X | LWORD_TO_WORD | | |
| DWORD1) | X | LWORD_TO_DWORD | | |
| SINT | X | ENO = TRUE #sint1 := LWORD_TO_SINT(16#FFFF_FFFF_FFFF_FFFF); // -1 to #sint1 := LWORD_TO_SINT(16#FFFF_FFFF_FFFF_FF80); // -128 #sint1 := LWORD_TO_SINT(16#0); // 0 to #sint1 := LWORD_TO_SINT(16#0000_0000_0000_007F); // 127 ENO = FALSE #sint1 := LWORD_TO_SINT(16#FFFF_FFFF_FFFF_FF7F); // -129 #sint1 := LWORD_TO_SINT(16#8000_0000_0000_0000); // -9223372036854775808 #sint1 := LWORD_TO_SINT(16#0000_0000_0000_0080); // 128 #sint1 := LWORD_TO_SINT(16#7FFF_FFFF_FFFF_FFFF); // 9223372036854775807 | LWORD_TO_SINT | |
| USINT | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | LWORD_TO_USINT | |
| INT | X | ENO = TRUE #int1 := LWORD_TO_INT(16#FFFF_FFFF_FFFF_FFFF); // -1 to #int1 := LWORD_TO_INT(16#FFFF_FFFF_FFFF_8000); // -32768 #int1 := LWORD_TO_INT(16#0); // 0 to #int1 := LWORD_TO_INT(16#0000_0000_0000_7FFF); // 32767 ENO = FALSE #int1 := LWORD_TO_INT(16#FFFF_FFFF_FFFF_7FFF); // -32769 #int1 := LWORD_TO_INT(16#8000_0000_0000_0000); // -2147483648 #int1 := LWORD_TO_INT(16#0000_0000_0000_8000); // 32768 to #int1 := LWORD_TO_INT(16#7FFF_FFFF_FFFF_FFFF); // 2147483647 | LWORD_TO_INT | |
| UINT | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | LWORD_TO_UINT | |
| DINT | X | ENO = TRUE #dint1 := LWORD_TO_DINT(16#FFFF_FFFF_FFFF_FFFF); // -1 to #dint1 := LWORD_TO_DINT(16#FFFF_FFFF_8000_0000); // -2147483648 #dint1 := LWORD_TO_DINT(16#0); // 0 to #dint1 := LWORD_TO_DINT(16#0000_0000_7FFF_FFFF); // 2147483647 ENO = FALSE #dint1 := LWORD_TO_DINT(16#FFFF_FFFF_7FFF_FFFF); // -2147483649 to #dint1 := LWORD_TO_DINT(16#8000_0000_0000_0000); // -9223372036854775808 #dint1 := LWORD_TO_DINT(16#0000_0000_8000_0000); // 2147483648 to #dint1 := LWORD_TO_DINT(16#7FFF_FFFF_FFFF_FFFF); // 9223372036854775807 | LWORD_TO_DINT | |
| UDINT | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | LWORD_TO_UDINT | |
| LINT | X | LWORD_TO_LINT | | |
| ULINT | X | LWORD_TO_ULINT | | |
| REAL | - | No explicit conversion | - | |
| LREAL | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. If no errors occur during the conversion, the signal state of ENO = 1; if an error occurs during processing, the signal state of ENO = 0. | LWORD_TO_LREAL | |
| TIME | X | LWORD_TO_TIME | | |
| LTIME | X | LWORD_TO_LTIME | | |
| S5TIME | - | No explicit conversion | - | |
| LDT | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | LWORD_TO_LDT | |
| DT | - | No explicit conversion | - | |
| DTL | - | - | | |
| TOD | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | LWORD_TO_TOD | |
| LTOD | X | LWORD_TO_LTOD | | |
| DATE | X | LWORD_TO_DATE | | |
| STRING | - | No explicit conversion | - | |
| WSTRING | - | - | | |
| CHAR | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | LWORD_TO_CHAR | |
| WCHAR | X | LWORD_TO_WCHAR | | |
| x: Conversion possible - : Conversion not possible 1) Bit strings (BYTE, WORD, DWORD, LWORD) are interpreted as an unsigned integer with the same bit length. The data type BYTE is interpreted as USINT, WORD as UINT, DWORD as UDINT and LWORD as ULINT. | | | | |
See also

Implicit conversion of LWORD (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) LWORD (S7-1500, S7-1200 G2)

Integers (S7-1500, S7-1200 G2) Explicit conversion of SINT (S7-1500, S7-1200 G2)
| Explicit conversion of SINT |
|---|
Options for explicit conversion

The following table shows the options and instructions for explicit conversion of the SINT data type:

| Source | Destination | Conversion | Explanation | Mnemonics of the instruction |
|---|---|---|---|---|
| SINT | BOOL | X | The following scenarios are possible: If the source is "0", the target data type is also "0" and enable output ENO is "1". If only the LSB (Least Significant Bit) "1" is set in the source value, the target data type is also "1" and enable output ENO is "1". If bit is not equal to LSB in the source value, the target data type is set according to LSB and enable output ENO is "0". | SINT_TO_BOOL |
| BYTE1) | X | The bit pattern of the source value is transferred unchanged, right-justified, to the target data type. If a negative value is converted to an unsigned target data type, the enable output ENO is set to "0". | SINT_TO_BYTE | |
| WORD1) | X | SINT_TO_WORD | | |
| DWORD1) | X | SINT_TO_DWORD | | |
| LWORD1) | X | SINT_TO_LWORD | | |
| USINT | X | The bit pattern of the source value is converted and transferred to the target data type. (The value "-1" (16#FF) becomes the value "-1" (16#FFFFFFFF). Enable output ENO is set to "0" if a negative value is converted to an unsigned target data type. | SINT_TO_USINT | |
| INT | X | SINT_TO_INT | | |
| UINT | X | SINT_TO_UINT | | |
| DINT | X | SINT_TO_DINT | | |
| UDINT | X | SINT_TO_UDINT | | |
| LINT | X | SINT_TO_LINT | | |
| ULINT | X | SINT_TO_ULINT | | |
| REAL | X | The value is converted to the destination data type format. (The value "-1" is changed to the value "-1.0", for example, with the instruction "Convert value" (CONVERT). | SINT_TO_REAL, NORM_X | |
| LREAL | X | SINT_TO_LREAL, NORM_X | | |
| TIME | X | The value is transferred to the target data type and interpreted as milliseconds. | SINT_TO_TIME | |
| LTIME | X | The value is transferred to the destination data type and interpreted as nanoseconds. | SINT_TO_LTIME | |
| S5TIME | - | No explicit conversion | - | |
| LDT | X | The result is returned in nanoseconds since 1970-1-1-0:0:0.0. | SINT_TO_LDT | |
| DT | - | No explicit conversion | - | |
| DTL | - | - | | |
| TOD | X | The bit pattern of the source value is converted and transferred to the target data type. (The value "-1" (16#FF) becomes the value "-1" (16#FFFFFFFF). Enable output ENO is set to "0" if a negative value is converted to an unsigned target data type. (interpretation in milliseconds since 0:0) | SINT_TO_TOD | |
| LTOD | X | The bit pattern of the source value is converted and transferred to the target data type. (The value "-1" (16#FF) becomes the value "-1" (16#FFFFFFFF). Enable output ENO is set to "0" if a negative value is converted to an unsigned target data type. (interpretation in nanoseconds since 0:0) | SINT_TO_LTOD | |
| DATE | X | The bit pattern of the source value is converted and transferred to the target data type. (The value "-1" (16#FF) becomes the value "-1" (16#FFFFFFFF). Enable output ENO is set to "0" if a negative value is converted to an unsigned target data type. (interpretation in days since 1990-1-1) | SINT_TO_DATE | |
| STRING | X | The value is converted into a character string. The first characters of the string are padded with spaces. The number of spaces depends on the length of the numerical value. Positive numeric values are output without a sign. If the permitted length of the character string is violated, the enable output ENO is set to "0". The following special features apply to SCL: No spaces are inserted. The character string is shown preceded by a sign. | SINT_TO_STRING, S_CONV, VAL_STRG | |
| WSTRING | X | SINT_TO_WSTRING | | |
| CHAR1) | X | The bit pattern of the source value is converted and transferred to the target data type. (The value "-1" (16#FF) becomes the value "-1" (16#FFFFFFFF). Enable output ENO is set to "0" if a negative value is converted to an unsigned target data type. | SINT_TO_CHAR | |
| WCHAR1) | X | SINT_TO_WCHAR | | |
| x: Conversion possible - : Conversion not possible 1) Bit strings (BYTE, WORD, DWORD, LWORD) and the data types CHAR and WCHAR are initially extended to the necessary width including sign, and then the bits are copied. The source type determines the interpretation. | | | | |
See also

Implicit conversion of SINT (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) SINT (8-bit integers) (S7-1200, S7-1500, S7-1200 G2)

Explicit conversion of USINT (S7-1500, S7-1200 G2)
| Explicit conversion of USINT |
|---|
Options for explicit conversion

The following table shows the options and instructions for the explicit conversion of the USINT data type:

| Source | Destination | Conversion | Explanation | Mnemonics of the instruction |
|---|---|---|---|---|
| USINT | BOOL | X | The following scenarios are possible: If the source is "0", the target data type is also "0" and enable output ENO is "1". If only the LSB (Least Significant Bit) "1" is set in the source value, the target data type is also "1" and enable output ENO is "1". If bit is not equal to LSB in the source value, the target data type is set according to LSB and enable output ENO is "0". | USINT_TO_BOOL |
| BYTE 1) | X | The bit pattern of the source value is transferred unchanged, right-justified, to the target data type. | USINT_TO_BYTE | |
| WORD1) | X | USINT_TO_WORD | | |
| DWORD 1) | X | USINT_TO_DWORD | | |
| LWORD 1) | X | USINT_TO_LWORD | | |
| SINT | X | The bit pattern of the source value is transferred unchanged, right-justified, to the target data type. If the sign is changed during the conversion, the enable output ENO is set to "0". | USINT_TO_SINT | |
| INT | X | The bit pattern of the source value is converted and transferred to the target data type. | USINT_TO_INT | |
| UINT | X | USINT_TO_UINT | | |
| DINT | X | USINT_TO_DINT | | |
| UDINT | X | USINT_TO_UDINT | | |
| LINT | X | USINT_TO_LINT | | |
| ULINT | X | USINT_TO_ULINT | | |
| REAL | X | The value is converted to the destination data type format. (The value "1" is changed to the value "1.0", for example, with the instruction "Convert value" (CONVERT). | USINT_TO_REAL, NORM_X | |
| LREAL | X | USINT_TO_LREAL, NORM_X | | |
| TIME | X | The value is transferred to the target data type and interpreted as milliseconds. | USINT_TO_TIME | |
| LTIME | X | The value is transferred to the destination data type and interpreted as nanoseconds. | USINT_TO_LTIME | |
| S5TIME | - | No explicit conversion | - | |
| LDT | X | The result is returned in nanoseconds since 1970-1-1-0:0:0.0. | USINT_TO_LDT | |
| DT | - | No explicit conversion | - | |
| DTL | - | - | | |
| TOD | X | The bit pattern of the source value is converted and transferred to the target data type. (interpretation in milliseconds since 0:0) | USINT_TO_TOD | |
| LTOD | X | The bit pattern of the source value is converted and transferred to the target data type. (interpretation in nanoseconds since 0:0) | USINT_TO_LTOD | |
| DATE | X | The bit pattern of the source value is converted and transferred to the target data type. (interpretation in days since 1990-1-1) | USINT_TO_DATE | |
| STRING | X | The value is converted into a character string. The first characters of the string are padded with spaces. The number of spaces depends on the length of the numerical value. Positive numeric values are output without a sign. If the permitted length of the character string is violated, the enable output ENO is set to "0". The following special features apply to SCL: No spaces are inserted. The character string is shown preceded by a sign. | USINT_TO_STRING, S_CONV, VAL_STRG | |
| WSTRING | X | USINT_TO_WSTRING | | |
| CHAR 1) | X | The bit pattern of the source value is converted and transferred to the target data type. | USINT_TO_CHAR | |
| WCHAR 1) | X | USINT_TO_WCHAR | | |
| x: Conversion possible - : Conversion not possible 1) Bit strings (BYTE, WORD, DWORD, LWORD) and the data types CHAR and WCHAR are initially extended to the necessary width (the non-existing sign is replaced with zeros), and then the bits are copied. The source type determines the interpretation. | | | | |
See also

Implicit conversion of USINT (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) USINT (8-bit integers) (S7-1200, S7-1500, S7-1200 G2)

Explicit conversion of INT (S7-1500, S7-1200 G2)
| Explicit conversion of INT |
|---|
Options for explicit conversion

The following table shows the options and instructions for the explicit conversion of the INT data type:

| Source | Destination | Conversion | Explanation | Mnemonics of the instruction |
|---|---|---|---|---|
| INT | BOOL | X | The following scenarios are possible: If the source is "0", the target data type is also "0" and enable output ENO is "1". If only the LSB (Least Significant Bit) "1" is set in the source value, the target data type is also "1" and enable output ENO is "1". If bit is not equal to LSB in the source value, the target data type is set according to LSB and enable output ENO is "0". | INT_TO_BOOL |
| BYTE1) | X | The bit pattern of the source value is transferred unchanged, right-justified, to the target data type. If a negative value is converted to an unsigned target data type, the enable output ENO is set to "0". | INT_TO_BYTE | |
| WORD1) | X | INT_TO_WORD | | |
| DWORD1) | X | INT_TO_DWORD | | |
| LWORD1) | X | INT_TO_LWORD | | |
| SINT | X | The bit pattern of the source value is converted and transferred to the target data type. (The value "-1" (16#FF) becomes the value "-1" (16#FFFFFFFF)). If a negative value is converted to an unsigned target data type, the enable output ENO is set to "0". | INT_TO_SINT | |
| USINT | X | INT_TO_USINT | | |
| UINT | X | INT_TO_UINT | | |
| DINT | X | INT_TO_DINT | | |
| UDINT | X | INT_TO_UDINT | | |
| LINT | X | INT_TO_LINT | | |
| ULINT | X | INT_TO_ULINT | | |
| REAL | X | The value is converted to the destination data type format. (The value "-1" is changed to the value "-1.0", for example, with the instruction "Convert value" (CONVERT). | INT_TO_REAL, NORM_X | |
| LREAL | X | INT_TO_LREAL, NORM_X | | |
| TIME | X | The value is transferred to the target data type and interpreted as milliseconds. | INT_TO_TIME | |
| LTIME | X | The value is transferred to the destination data type and interpreted as nanoseconds. | INT_TO_LTIME | |
| S5TIME | - | No explicit conversion | - | |
| LDT | X | The result is returned in nanoseconds since 1970-1-1-0:0:0.0. | INT_TO_LDT | |
| DT | - | No explicit conversion | - | |
| DTL | - | - | | |
| TOD | X | The bit pattern of the source value is converted and transferred to the target data type. (The value "-1" (16#FF) becomes the value "-1" (16#FFFFFFFF)). If a negative value is converted to an unsigned target data type, the enable output ENO is set to "0". (interpretation in milliseconds since 0:0; check for 24h limit) | INT_TO_TOD | |
| LTOD | X | The bit pattern of the source value is converted and transferred to the target data type. (The value "-1" (16#FF) becomes the value "-1" (16#FFFFFFFF)). If a negative value is converted to an unsigned target data type, the enable output ENO is set to "0". (interpretation in nanoseconds since 0:0; check for 24h limit) | INT_TO_LTOD | |
| DATE | X | The bit pattern of the source value is converted and transferred to the target data type. (The value "-1" (16#FF) becomes the value "-1" (16#FFFFFFFF)). If a negative value is converted to an unsigned target data type, the enable output ENO is set to "0". (interpretation in days since 1990-1-1; check for negative value) | INT_TO_DATE | |
| STRING | X | The value is converted into a character string. The first characters of the string are padded with spaces. The number of spaces depends on the length of the numerical value. Positive numeric values are output without a sign. If the permitted length of the character string is violated, the enable output ENO is set to "0". The following special features apply to SCL: No spaces are inserted. The character string is shown preceded by a sign. | INT_TO_STRING, S_CONV, VAL_STRG | |
| WSTRING | X | INT_TO_WSTRING | | |
| CHAR1) | X | The bit pattern of the source value is converted and transferred to the target data type. (The value "-1" (16#FF) becomes the value "-1" (16#FFFFFFFF)). If a negative value is converted to an unsigned target data type, the enable output ENO is set to "0". | INT_TO_CHAR | |
| WCHAR1) | X | INT_TO_WCHAR | | |
| BCD16 | X | The value to be converted has type INT and is accepted as an integer with a value between -999 and +999. The result is available after conversion as a BCD-coded number of the type WORD. A real conversion takes place. If the value is outside the target area, a synchronous error is not triggered, but rather only the status bit OV is set. | INT_TO_BCD16 | |
| BCD16_WORD | X | INT_TO_BCD16_WORD | | |
| x: Conversion possible - : Conversion not possible 1) Bit strings (BYTE, WORD, DWORD, LWORD) and the data types CHAR and WCHAR are initially extended to the necessary width including sign, and then the bits are copied. The source type determines the interpretation. | | | | |
See also

Implicit conversion of INT (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) INT (16-bit integers)

Explicit conversion of UINT (S7-1500, S7-1200 G2)
| Explicit conversion of UINT |
|---|
Options for explicit conversion

The following table shows the options and instructions for the explicit conversion of the UINT data type:

| Source | Destination | Conversion | Explanation | Mnemonics of the instruction |
|---|---|---|---|---|
| UINT | BOOL | X | The following scenarios are possible: If the source is "0", the target data type is also "0" and enable output ENO is "1". If only the LSB (Least Significant Bit) "1" is set in the source value, the target data type is also "1" and enable output ENO is "1". If bits are not equal to LSB in the source value, the destination data type is set according to LSB and the enable output ENO is "0". | UINT_TO_BOOL |
| BYTE 1) | X | The bit pattern of the source value is transferred unchanged, right-justified, to the target data type. If bits are lost in the process, the enable output ENO is set to "0". | UINT_TO_BYTE | |
| WORD1) | X | UINT_TO_WORD | | |
| DWORD 1) | X | UINT_TO_DWORD | | |
| LWORD 1) | X | UINT_TO_LWORD | | |
| SINT | X | UINT_TO_SINT | | |
| USINT | X | UINT_TO_USINT | | |
| INT | X | The bit pattern of the source value is transferred unchanged, right-justified, to the target data type. If the sign bit is changed during the conversion, the enable output ENO is set to "0". | UINT_TO_INT | |
| DINT | X | The bit pattern of the source value is transferred unchanged, right-justified, to the target data type. | UINT_TO_DINT | |
| UDINT | X | UINT_TO_UDINT | | |
| LINT | X | UINT_TO_LINT | | |
| ULINT | X | UINT_TO_ULINT | | |
| REAL | X | The value is converted to the destination data type format. (The value "1" is changed to the value "1.0", for example, with the instruction "Convert value" (CONVERT). | UINT_TO_REAL, NORM_X | |
| LREAL | X | UINT_TO_LREAL, NORM_X | | |
| TIME | X | The value is transferred to the target data type and interpreted as milliseconds. | UINT_TO_TIME | |
| LTIME | X | The value is transferred to the destination data type and interpreted as nanoseconds. | UINT_TO_LTIME | |
| S5TIME | - | No explicit conversion | - | |
| LDT | X | The result is returned in nanoseconds since 1970-1-1-0:0:0.0. | UINT_TO_LDT | |
| DT | - | No explicit conversion | - | |
| DTL | - | - | | |
| TOD | X | The bit pattern of the source value is converted and transferred to the target data type. (interpretation in milliseconds since 0:0; check for 24h limit) | UINT_TO_TOD | |
| LTOD | X | The bit pattern of the source value is converted and transferred to the target data type. (interpretation in nanoseconds since 0:0; check for 24h limit) | UINT_TO_LTOD | |
| DATE | X | The bit pattern of the source value is converted and transferred to the target data type. (interpretation in days since 1990-1-1; check for negative value) | UINT_TO_DATE, T_CONV | |
| STRING | X | The value is converted into a character string. The first characters of the string are padded with spaces. The number of spaces depends on the length of the numerical value. Positive numeric values are output without a sign. If the permitted length of the character string is violated, the enable output ENO is set to "0". The following special features apply to SCL: No spaces are inserted. The character string is shown preceded by a sign. | UINT_TO_STRING, S_CONV, VAL_STRG | |
| WSTRING | X | UINT_TO_WSTRING | | |
| CHAR 1) | X | The bit pattern of the source value is transferred unchanged to the target data type. The enable output ENO is set to "0" in the event of overflow. | UINT_TO_CHAR | |
| WCHAR 1) | X | UINT_TO_WCHAR | | |
| x: Conversion possible - : Conversion not possible 1) Bit strings (BYTE, WORD, DWORD, LWORD) and the data types CHAR and WCHAR are initially extended to the necessary width (the non-existing sign is replaced with zeros), and then the bits are copied. The source type determines the interpretation. | | | | |
See also

Implicit conversion of UINT (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) UINT (16-bit integers) (S7-1200, S7-1500, S7-1200 G2)

Explicit conversion of DINT (S7-1500, S7-1200 G2)
| Explicit conversion of DINT |
|---|
Options for explicit conversion

The following table shows the options and instructions for the explicit conversion of the DINT data type:

| Source | Destination | Conversion | Explanation | Mnemonics of the instruction |
|---|---|---|---|---|
| DINT | BOOL | X | The following scenarios are possible: If the source is "0", the target data type is also "0" and enable output ENO is "1". If only the LSB (Least Significant Bit) "1" is set in the source value, the target data type is also "1" and enable output ENO is "1". If bits are not equal to LSB in the source value, the destination data type is set according to LSB and the enable output ENO is "0". | DINT_TO_BOOL |
| BYTE1) | X | The bit pattern of the source value is transferred unchanged, right-justified, to the target data type. If a negative value is converted to an unsigned target data type, the enable output ENO is set to "0". | DINT_TO_BYTE | |
| WORD1) | X | DINT_TO_WORD | | |
| DWORD1) | X | DINT_TO_DWORD | | |
| LWORD1) | X | DINT_TO_LWORD | | |
| SINT | X | The bit pattern of the source value is converted and transferred to the target data type. (The value "-1" (16#FF) becomes the value "-1" (16#FFFFFFFF)). If a negative value is converted to an unsigned target data type, the enable output ENO is set to "0". | DINT_TO_SINT | |
| USINT | X | DINT_TO_USINT | | |
| INT | X | DINT_TO_INT | | |
| UINT | X | DINT_TO_UINT | | |
| UDINT | X | DINT_TO_UDINT | | |
| LINT | X | DINT_TO_LINT | | |
| ULINT | X | DINT_TO_ULINT | | |
| REAL | X | The value is converted to the destination data type format. (The value "-1" is changed to the value "-1.0", for example, with the instruction "Convert value" (CONVERT). | DINT_TO_REAL, NORM_X | |
| LREAL | X | DINT_TO_LREAL, NORM_X | | |
| TIME | X | The value is transferred to the target data type and interpreted as milliseconds. | DINT_TO_TIME, T_CONV | |
| LTIME | X | The value is transferred to the destination data type and interpreted as nanoseconds. | DINT_TO_LTIME, T_CONV | |
| S5TIME | - | No explicit conversion | - | |
| LDT | X | The result is returned in nanoseconds since 1970-1-1-0:0:0.0. | DINT_TO_LDT | |
| DT | - | No explicit conversion | - | |
| DTL | - | - | | |
| TOD | X | The bit pattern of the source value is converted and transferred to the target data type. (The value "-1" (16#FF) becomes the value "-1" (16#FFFFFFFF)). If a negative value is converted to an unsigned target data type, the enable output ENO is set to "0". (interpretation in milliseconds since 0:0) | DINT_TO_TOD | |
| LTOD | X | The bit pattern of the source value is converted and transferred to the target data type. (The value "-1" (16#FF) becomes the value "-1" (16#FFFFFFFF)). If a negative value is converted to an unsigned target data type, the enable output ENO is set to "0". (interpretation in nanoseconds since 0:0) | DINT_TO_LTOD | |
| DATE | X | The bit pattern of the source value is converted and transferred to the target data type. (The value "-1" (16#FF) becomes the value "-1" (16#FFFFFFFF)). If a negative value is converted to an unsigned target data type, the enable output ENO is set to "0". (interpretation in days since 1990-1-1) | DINT_TO_DATE | |
| STRING | X | The value is converted into a character string. The first characters of the string are padded with spaces. The number of spaces depends on the length of the numerical value. Positive numeric values are output without a sign. If the permitted length of the character string is violated, the enable output ENO is set to "0". The following special features apply to SCL: No spaces are inserted. The character string is shown preceded by a sign. | DINT_TO_STRING, S_CONV, VAL_STRG | |
| WSTRING | X | DINT_TO_WSTRING | | |
| CHAR1) | X | The bit pattern of the source value is converted and transferred to the target data type. (The value "-1" (16#FF) becomes the value "-1" (16#FFFFFFFF)). If a negative value is converted to an unsigned target data type, the enable output ENO is set to "0". | DINT_TO_CHAR | |
| WCHAR1) | X | DINT_TO_WCHAR | | |
| BCD32 | X | The value to be converted has type DINT and is accepted as an integer with a value between –999999 and +9999999. The result is available after conversion as a BCD-coded number of the type DWORD. The enable output is set to "0" in the event of overflow. A real conversion takes place. If the value is outside the target area, a synchronous error is not triggered, but rather only the status bit OV is set. | DINT_TO_BCD32 | |
| BCD32_DWORD | X | DINT_TO_BCD32_DWORD | | |
| x: Conversion possible - : Conversion not possible 1) Bit strings (BYTE, WORD, DWORD, LWORD) and the data types CHAR and WCHAR are initially extended to the necessary width including sign, and then the bits are copied. The source type determines the interpretation. | | | | |
See also

Implicit conversion of DINT (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) DINT (32-bit integers)

Explicit conversion of UDINT (S7-1500, S7-1200 G2)
| Explicit conversion of UDINT |
|---|
Options for explicit conversion

The following table shows the options and instructions for the explicit conversion of the UDINT data type:

| Source | Destination | Conversion | Explanation | Mnemonics of the instruction |
|---|---|---|---|---|
| UDINT | BOOL | X | The following scenarios are possible: If the source is "0", the target data type is also "0" and enable output ENO is "1". If only the LSB (Least Significant Bit) "1" is set in the source value, the target data type is also "1" and enable output ENO is "1". If bits are not equal to LSB in the source value, the destination data type is set according to LSB and the enable output ENO is "0". | UDINT_TO_BOOL |
| BYTE 1) | X | The bit pattern of the source value is transferred unchanged, right-justified, to the target data type. If bits are lost in the process, the enable output ENO is set to "0". | UDINT_TO_BYTE | |
| WORD1) | X | UDINT_TO_WORD | | |
| DWORD 1) | X | UDINT_TO_DWORD | | |
| LWORD 1) | X | UDINT_TO_LWORD | | |
| SINT | X | UDINT_TO_SINT | | |
| USINT | X | UDINT_TO_USINT | | |
| INT | X | UDINT_TO_INT | | |
| UINT | X | UDINT_TO_UINT | | |
| DINT | X | The bit pattern of the source value is transferred unchanged, right-justified, to the target data type. If the sign bit is changed during the conversion, the enable output ENO is set to "0". | UDINT_TO_DINT | |
| LINT | X | The bit pattern of the source value is transferred unchanged, right-justified, to the target data type. | UDINT_TO_LINT | |
| ULINT | X | UDINT_TO_ULINT | | |
| REAL | X | The value is converted to the destination data type format. (The value "1" is changed to the value "1.0", for example, with the instruction "Convert value" (CONVERT). | UDINT_TO_REAL, NORM_X | |
| LREAL | X | UDINT_TO_LREAL, NORM_X | | |
| TIME | X | The value is transferred to the target data type and interpreted as milliseconds. | UDINT_TO_TIME | |
| LTIME | X | The value is transferred to the destination data type and interpreted as nanoseconds. | UDINT_TO_LTIME | |
| S5TIME | - | No explicit conversion | - | |
| LDT | X | The result is returned in nanoseconds since 1970-1-1-0:0:0.0. | UDINT_TO_LDT | |
| DT | - | No explicit conversion | - | |
| DTL | - | - | | |
| TOD | X | The bit pattern of the source value is converted and transferred to the target data type. (The value "-1" (16#FF) becomes the value "-1" (16#FFFFFFFF)). If a negative value is converted to an unsigned target data type, the enable output ENO is set to "0". (interpretation in milliseconds since 0:0; check for 24h limit) | UDINT_TO_TOD, T_CONV | |
| LTOD | X | The bit pattern of the source value is converted and transferred to the target data type. (The value "-1" (16#FF) becomes the value "-1" (16#FFFFFFFF)). If a negative value is converted to an unsigned target data type, the enable output ENO is set to "0". (interpretation in nanoseconds since 0:0; check for 24h limit) | UDNT_TO_LTOD, T_CONV | |
| DATE | X | The bit pattern of the source value is converted and transferred to the target data type. (The value "-1" (16#FF) becomes the value "-1" (16#FFFFFFFF)). If a negative value is converted to an unsigned target data type, the enable output ENO is set to "0". (interpretation in days since 1990-1-1; check for negative value) | UDINT_TO_DATE | |
| STRING | X | The value is converted into a character string. The first characters of the string are padded with spaces. The number of spaces depends on the length of the numerical value. Positive numeric values are output without a sign. If the permitted length of the character string is violated, the enable output ENO is set to "0". The following special features apply to SCL: No spaces are inserted. The character string is shown preceded by a sign. | UDINT_TO_STRING, S_CONV, VAL_STRG | |
| WSTRING | X | UDINT_TO_WSTRING | | |
| CHAR 1) | X | The bit pattern of the source value is transferred unchanged to the target data type. The enable output ENO is set to "0" in the event of overflow. | UDINT_TO_CHAR | |
| WCHAR 1) | X | UDINT_TO_WCHAR | | |
| x: Conversion possible - : Conversion not possible 1) Bit strings (BYTE, WORD, DWORD, LWORD) and the data types CHAR and WCHAR are initially extended to the necessary width (the non-existing sign is replaced with zeros), and then the bits are copied. The source type determines the interpretation. | | | | |
See also

Implicit conversion of UDINT (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) UDINT (32-bit integers) (S7-1200, S7-1500, S7-1200 G2)

Explicit conversion of LINT (S7-1500, S7-1200 G2)
| Explicit conversion of LINT |
|---|
Options for explicit conversion

The following table shows the options and instructions for the explicit conversion of the LINT data type:

| Source | Destination | Conversion | Explanation | Mnemonics of the instruction |
|---|---|---|---|---|
| LINT | BOOL | X | The following scenarios are possible: If the source is "0", the target data type is also "0" and enable output ENO is "1". If only the LSB (Least Significant Bit) "1" is set in the source value, the target data type is also "1" and enable output ENO is "1". If bits are not equal to LSB in the source value, the destination data type is set according to LSB and the enable output ENO is "0". | LINT_TO_BOOL |
| BYTE1) | X | The bit pattern of the source value is transferred unchanged, right-justified, to the target data type. If a negative value is converted to an unsigned target data type, the enable output ENO is set to "0". | LINT_TO_BYTE | |
| WORD1) | X | LINT_TO_WORD | | |
| DWORD1) | X | LINT_TO_DWORD | | |
| LWORD1) | X | LINT_TO_LWORD | | |
| SINT | X | LINT_TO_SINT | | |
| USINT | X | LINT_TO_USINT | | |
| INT | X | LINT_TO_INT | | |
| UINT | X | LINT_TO_UINT | | |
| DINT | X | LINT_TO_DINT | | |
| UDINT | X | LINT_TO_UDINT | | |
| ULINT | X | LINT_TO_ULINT | | |
| REAL | X | The value is converted to the destination data type format. (The value "-1" is changed to the value "-1.0", for example, with the instruction "Convert value" (CONVERT). | LINT_TO_REAL, NORM_X | |
| LREAL | X | LINT_TO_LREAL, NORM_X | | |
| TIME | X | The value is transferred to the target data type and interpreted as milliseconds. | LINT_TO_TIME, T_CONV | |
| LTIME | X | The value is transferred to the destination data type and interpreted as nanoseconds. | LINT_TO_LTIME, T_CONV | |
| S5TIME | - | No explicit conversion | - | |
| LDT | X | The result is returned in nanoseconds since 1970-1-1-0:0:0.0. | LINT_TO_LDT | |
| DT | - | No explicit conversion | - | |
| DTL | - | - | | |
| TOD | X | The bit pattern of the source value is converted and transferred to the target data type. (The value "-1" (16#FF) becomes the value "-1" (16#FFFFFFFF)). If a negative value is converted to an unsigned target data type, the enable output ENO is set to "0". (interpretation in milliseconds since 0:0) | LINT_TO_TOD | |
| LTOD | X | The bit pattern of the source value is converted and transferred to the target data type. (The value "-1" (16#FF) becomes the value "-1" (16#FFFFFFFF)). If a negative value is converted to an unsigned target data type, the enable output ENO is set to "0". (interpretation in nanoseconds since 0:0) | LINT_TO_LTOD | |
| DATE | X | The bit pattern of the source value is converted and transferred to the target data type. (The value "-1" (16#FF) becomes the value "-1" (16#FFFFFFFF)). If a negative value is converted to an unsigned target data type, the enable output ENO is set to "0". (interpretation in days since 1990-1-1) | LINT_TO_DATE | |
| STRING | X | The value is converted into a character string. The first characters of the string are padded with spaces. The number of spaces depends on the length of the numerical value. Positive numeric values are output without a sign. If the permitted length of the character string is violated, the enable output ENO is set to "0". The following special features apply to SCL: No spaces are inserted. The character string is shown preceded by a sign. | LINT_TO_STRING, S_CONV, VAL_STRG | |
| WSTRING | X | LINT_TO_WSTRING | | |
| CHAR1) | X | The bit pattern of the source value is converted and transferred to the target data type. (The value "-1" (16#FF) becomes the value "-1" (16#FFFFFFFF)). If a negative value is converted to an unsigned target data type, the enable output ENO is set to "0". | LINT_TO_CHAR | |
| WCHAR1) | X | LINT_TO_WCHAR | | |
| x: Conversion possible - : Conversion not possible 1) Bit strings (BYTE, WORD, DWORD, LWORD) and the data types CHAR and WCHAR are initially extended to the necessary width including sign, and then the bits are copied. The source type determines the interpretation. | | | | |
See also

Implicit conversion of LINT (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) LINT (64-bit integers) (S7-1500, S7-1200 G2)

Explicit conversion of ULINT (S7-1500, S7-1200 G2)
| Explicit conversion of ULINT |
|---|
Options for explicit conversion

The following table shows the options and instructions for the explicit conversion of the ULINT data type:

| Source | Destination | Conversion | Explanation | Mnemonics of the instruction |
|---|---|---|---|---|
| ULINT | BOOL | X | The following scenarios are possible: If the source is "0", the target data type is also "0" and enable output ENO is "1". If only the LSB (Least Significant Bit) "1" is set in the source value, the target data type is also "1" and enable output ENO is "1". If bits are not equal to LSB in the source value, the destination data type is set according to LSB and the enable output ENO is "0". | ULINT_TO_BOOL |
| BYTE 1) | X | The bit pattern of the source value is transferred unchanged, right-justified, to the target data type. | ULINT_TO_BYTE | |
| WORD1) | X | ULINT_TO_WORD | | |
| DWORD 1) | X | ULINT_TO_DWORD | | |
| LWORD 1) | X | ULINT_TO_LWORD | | |
| SINT | X | ULINT_TO_SINT | | |
| USINT | X | ULINT_TO_USINT | | |
| INT | X | ULINT_TO_INT | | |
| UINT | X | ULINT_TO_UINT | | |
| DINT | X | The bit pattern of the source value is transferred unchanged, right-justified, to the target data type. If the sign bit is overwritten during the conversion, the enable output ENO is set to "0". | ULINT_TO_DINT | |
| UDINT | X | The bit pattern of the source value is transferred unchanged, right-justified, to the target data type. | ULINT_TO_UDINT | |
| LINT | X | ULINT_TO_LINT | | |
| REAL | X | The value is converted to the destination data type format. (The value "1" is changed to the value "1.0", for example, with the instruction "Convert value" (CONVERT). | ULINT_TO_REAL, NORM_X | |
| LREAL | X | ULINT_TO_LREAL, NORM_X | | |
| TIME | X | The value is transferred to the target data type and interpreted as milliseconds. | ULINT_TO_TIME | |
| LTIME | X | The value is transferred to the destination data type and interpreted as nanoseconds. | ULINT_TO_LTIME | |
| S5TIME | - | No explicit conversion | - | |
| LDT | X | The result is returned in nanoseconds since 1970-1-1-0:0:0.0. | ULINT_TO_LDT | |
| DT | - | No explicit conversion | - | |
| DTL | - | - | | |
| TOD | X | The bit pattern of the source value is converted and transferred to the target data type. (interpretation in milliseconds since 0:0) | ULINT_TO_TOD, T_CONV | |
| LTOD | X | The bit pattern of the source value is converted and transferred to the target data type. (interpretation in nanoseconds since 0:0) | ULINT_TO_LTOD, T_CONV | |
| DATE | X | The bit pattern of the source value is converted and transferred to the target data type. (interpretation in days since 1990-1-1) | ULINT_TO_DATE | |
| STRING | X | The value is converted into a character string. The first characters of the string are padded with spaces. The number of spaces depends on the length of the numerical value. Positive numeric values are output without a sign. If the permitted length of the character string is violated, the enable output ENO is set to "0". The following special features apply to SCL: No spaces are inserted. The character string is shown preceded by a sign. | ULINT_TO_STRING, S_CONV, VAL_STRG | |
| WSTRING | X | ULINT_TO_WSTRING | | |
| CHAR 1) | X | The bit pattern of the source value is converted and transferred to the target data type. | ULINT_TO_CHAR | |
| WCHAR 1) | X | ULINT_TO_WCHAR | | |
| x: Conversion possible - : Conversion not possible 1) Bit strings (BYTE, WORD, DWORD, LWORD) and the data types CHAR and WCHAR are initially extended to the necessary width (the non-existing sign is replaced with zeros), and then the bits are copied. The source type determines the interpretation. | | | | |
See also

Implicit conversion of ULINT (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) ULINT (64-bit integers) (S7-1500, S7-1200 G2)

Floating-point numbers (S7-1500, S7-1200 G2) Explicit conversion of REAL (S7-1500, S7-1200 G2)
| Explicit conversion of REAL |
|---|
Options for explicit conversion

The following table shows the options and instructions for the explicit conversion of the REAL data type:

| Source | Destination | Conversion | Explanation | Mnemonics of the instruction |
|---|---|---|---|---|
| REAL | BOOL | - | No explicit conversion | - |
| BYTE | - | - | | |
| WORD | - | - | | |
| DWORD | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | REAL_TO_DWORD | |
| LWORD | - | No explicit conversion | - | |
| SINT | X | The value is converted into the destination data type. The result of conversion depends on the instruction employed. The enable output ENO is set to "0" if the admissible range of values of the destination data type is exceeded during conversion or the value to be converted has an invalid floating-point number. | REAL_TO_SINT, ROUND, CEIL, FLOOR, TRUNC, NORM_X, SCALE_X | |
| USINT | X | REAL_TO_USINT, ROUND, CEIL, FLOOR, TRUNC, NORM_X, SCALE_X | | |
| INT | X | REAL_TO_INT, ROUND, CEIL, FLOOR, TRUNC, NORM_X, SCALE_X | | |
| UINT | X | REAL_TO_UINT, ROUND, CEIL, FLOOR, TRUNC, NORM_X, SCALE_X | | |
| DINT | X | REAL_TO_DINT, ROUND, CEIL, FLOOR, TRUNC, NORM_X, SCALE_X | | |
| UDINT | X | REAL_TO_UDINT, ROUND, CEIL, FLOOR, TRUNC, NORM_X, SCALE_X | | |
| LINT | X | REAL_TO_LINT, ROUND, CEIL, FLOOR, TRUNC, NORM_X, SCALE_X | | |
| ULINT | X | REAL_TO_ULINT, ROUND, CEIL, FLOOR, TRUNC, NORM_X, SCALE_X | | |
| LREAL | X | The value is converted into the destination data type. The result of the conversion depends on the instruction used, e.g. TRUNC(2.5) = 2.0; CEIL(2.5) = 3.0 | REAL_TO_LREAL, ROUND, CEIL, FLOOR, TRUNC, NORM_X, SCALE_X | |
| TIME | - | No explicit conversion | - | |
| LTIME | - | - | | |
| S5TIME | - | - | | |
| LDT | - | - | | |
| DT | - | - | | |
| DTL | - | - | | |
| TOD | - | - | | |
| LTOD | - | - | | |
| DATE | - | - | | |
| STRING | X | The value is converted into a character string. The enable output ENO is set to "0" if the character string length is exceeded or the value to be converted has an invalid floating-point number. The min. length of the character string is 14 characters. | REAL_TO_STRING, S_CONV, VAL_STRG | |
| WSTRING | X | REAL_TO_WSTRING | | |
| CHAR | - | No explicit conversion | - | |
| WCHAR | - | - | | |
| x: Conversion possible - : Conversion not possible | | | | |
See also

Implicit conversion of REAL (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) REAL

Explicit conversion of LREAL (S7-1500, S7-1200 G2)
| Explicit conversion of LREAL |
|---|
Options for explicit conversion

The following table shows the options and instructions for the explicit conversion of the LREAL data type:

| Source | Destination | Conversion | Explanation | Mnemonics of the instruction |
|---|---|---|---|---|
| LREAL | BOOL | - | No explicit conversion | - |
| BYTE | - | - | | |
| WORD | - | - | | |
| DWORD | - | - | | |
| LWORD | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | LREAL_TO_LWORD | |
| SINT | X | The value is converted into the destination data type. The result of conversion depends on the instruction employed. The enable output ENO is set to "0" if the admissible range of values of the destination data type is exceeded during conversion or the value to be converted has an invalid floating-point number. | LREAL_TO_SINT, ROUND, CEIL, FLOOR, TRUNC, NORM_X, SCALE_X | |
| USINT | X | LREAL_TO_USINT, ROUND, CEIL, FLOOR, TRUNC, NORM_X, SCALE_X | | |
| INT | X | LREAL_TO_INT, ROUND, CEIL, FLOOR, TRUNC, NORM_X, SCALE_X | | |
| UINT | X | LREAL_TO_UINT, ROUND, CEIL, FLOOR, TRUNC, NORM_X, SCALE_X | | |
| DINT | X | LREAL_TO_DINT, ROUND, CEIL, FLOOR, TRUNC, NORM_X, SCALE_X | | |
| UDINT | X | LREAL_TO_UDINT, ROUND, CEIL, FLOOR, TRUNC, NORM_X, SCALE_X | | |
| LINT | X | LREAL_TO_LINT, ROUND, CEIL, FLOOR, TRUNC, NORM_X, SCALE_X | | |
| ULINT | X | LREAL_TO_ULINT, ROUND, CEIL, FLOOR, TRUNC, NORM_X, SCALE_X | | |
| REAL | X | The value is converted into the destination data type. If the permitted value range of the destination data type is violated during the conversion or if the value to be converted is an invalid floating-point number, the enable output ENO is set to "0". A loss in accuracy is tolerated. | LREAL_TO_LREAL, ROUND, CEIL, FLOOR, TRUNC, NORM_X, SCALE_X | |
| TIME | - | No explicit conversion | - | |
| LTIME | - | - | | |
| S5TIME | - | - | | |
| LDT | - | - | | |
| DT | - | - | | |
| DTL | - | - | | |
| TOD | - | - | | |
| LTOD | - | - | | |
| DATE | - | - | | |
| STRING | X | The value is converted into a character string. The enable output ENO is set to "0" if the character string length is exceeded or the value to be converted has an invalid floating-point number. The min. length of the character string is 21 characters. | LREAL_TO_STRING, S_CONV, VAL_STRG | |
| WSTRING | X | LREAL_TO_WSTRING | | |
| CHAR | - | No explicit conversion | - | |
| WCHAR | - | - | | |
| x: Conversion possible - : Conversion not possible | | | | |
See also

Implicit conversion of LREAL (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) LREAL (S7-1200, S7-1500, S7-1200 G2)

Timers (S7-1500, S7-1200 G2) Explicit conversion of S5TIME (S7-1500, S7-1200 G2)
| Explicit conversion of S5TIME |
|---|
Options for explicit conversion

The following table shows the options and instructions for the explicit conversion of the S5TIME data type:

| Source | Destination | Conversion | Explanation | Mnemonics of the instruction |
|---|---|---|---|---|
| S5TIME | BOOL | - | No explicit conversion | - |
| BYTE | - | - | | |
| WORD1) | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | S5TIME_TO_WORD | |
| DWORD | - | No explicit conversion | - | |
| LWORD | - | - | | |
| SINT | - | - | | |
| USINT | - | - | | |
| INT | - | - | | |
| UINT | - | - | | |
| DINT | - | - | | |
| UDINT | - | - | | |
| LINT | - | - | | |
| ULINT | - | - | | |
| REAL | - | - | | |
| LREAL | - | - | | |
| TIME | X | A conversion of the source value into the destination data type takes place here (for example, s5t#10ms becomes T#10ms) | S5TIME_TO_TIME | |
| LTIME | X | A conversion of the source value into the destination data type takes place here (for example, s5t#10ms becomes LTIME#10ms) | S5TIME_TO_LTIME | |
| LDT | - | No explicit conversion | - | |
| DT | - | - | | |
| DTL | - | - | | |
| TOD | - | - | | |
| LTOD | - | - | | |
| DATE | - | - | | |
| STRING | - | - | | |
| WSTRING | - | - | | |
| CHAR | - | - | | |
| WCHAR | - | - | | |
| x: Conversion possible - : Conversion not possible 1) Bit strings (BYTE, WORD, DWORD, LWORD) and the data types CHAR and WCHAR are initially extended to the necessary width, and then the bits are copied. The source type determines the interpretation. | | | | |
See also

Implicit conversion of S5TIME (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) S5TIME (duration) (S7-300, S7-400, S7-1500)

Explicit conversion of TIME (S7-1500, S7-1200 G2)
| Explicit conversion of TIME |
|---|
Options for explicit conversion

The following table shows the options and instructions for the explicit conversion of the TIME data type:

| Source | Destination | Conversion | Explanation | Mnemonics of the instruction |
|---|---|---|---|---|
| TIME | BOOL | - | No explicit conversion | - |
| BYTE1) | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | TIME_TO_BYTE | |
| WORD1) | X | TIME_TO_WORD | | |
| DWORD1) | X | TIME_TO_DWORD | | |
| LWORD1) | X | TIME_TO_LWORD | | |
| SINT | X | The bit pattern of the source value is transferred unchanged right-justified and interpreted as milliseconds to the destination data type. | TIME_TO_SINT | |
| USINT | X | TIME_TO_USINT | | |
| INT | X | TIME_TO_INT | | |
| UINT | X | TIME_TO_UINT | | |
| DINT | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. The result of conversion shows the duration in milliseconds. | TIME_TO_DINT, T_CONV | |
| UDINT | X | The bit pattern of the source value is transferred unchanged right-justified and interpreted as milliseconds to the destination data type. A change in sign has the result that the enable output ENO is set to "0". | TIME_TO_UDINT | |
| LINT | X | TIME_TO_LINT | | |
| ULINT | X | TIME_TO_ULINT | | |
| REAL | - | No explicit conversion | - | |
| LREAL | - | - | | |
| S5TIME | X | A conversion of the source value into the destination data type takes place here (for example, T#10ms becomes s5t#10ms) | TIME_TO_TIME | |
| LTIME | X | A conversion of the source value into the destination data type takes place here (for example, T#10ms becomes LTIME#10ms) | TIME_TO_LTIME | |
| LDT | - | No explicit conversion | - | |
| DT | - | - | | |
| DTL | - | - | | |
| TOD | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. If the source value is outside the value range of TOD, the destination data type remains unchanged. | TIME_TO_TOD | |
| LTOD | - | No explicit conversion | - | |
| DATE | - | - | | |
| STRING | - | - | | |
| WSTRING | - | - | | |
| CHAR | - | - | | |
| WCHAR | - | - | | |
| x: Conversion possible - : Conversion not possible 1) Bit strings (BYTE, WORD, DWORD, LWORD) and the data types CHAR and WCHAR are initially extended to the necessary width, and then the bits are copied. The source type determines the interpretation. | | | | |
See also

Implicit conversion of TIME (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) TIME (IEC time)

Explicit conversion of LTIME (S7-1500, S7-1200 G2)
| Explicit conversion of LTIME |
|---|
Options for explicit conversion

The following table shows the options and instructions for the explicit conversion of the LTIME data type:

| Source | Destination | Conversion | Explanation | Mnemonics of the instruction |
|---|---|---|---|---|
| LTIME | BOOL | - | No explicit conversion | - |
| BYTE1) | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | LTIME_TO_BYTE | |
| WORD1) | X | LTIME_TO_WORD | | |
| DWORD1) | X | LTIME_TO_DWORD | | |
| LWORD1) | X | LTIME_TO_LWORD | | |
| SINT | X | The bit pattern of the source value is transferred unchanged right-justified and interpreted as nanoseconds to the destination data type. A change in sign has the result that the enable output ENO is set to "0". | LTIME_TO_SINT | |
| USINT | X | LTIME_TO_USINT | | |
| INT | X | LTIME_TO_INT | | |
| UINT | X | LTIME_TO_UINT | | |
| DINT | X | LTIME_TO_DINT | | |
| UDINT | X | LTIME_TO_UDINT | | |
| LINT | X | LTIME_TO_LINT, T_CONV | | |
| ULINT | X | LTIME_TO_ULINT | | |
| REAL | - | No explicit conversion | - | |
| LREAL | - | - | | |
| S5TIME | X | A conversion of the source value into the destination data type takes place here (for example, LTIME#10ms becomes s5t#10ms) | LTIME_TO_S5TIME | |
| TIME | X | A conversion of the source value into the destination data type takes place here (for example, LTIMET#10ms becomes T#10ms) | LTIME_TO_TIME | |
| LDT | X | A conversion of the source value into the destination data type takes place here (for example, LTIMET#10ms becomes LDT#1970-1-1-0:0:0.010000000) | LTIME_TO_LDT | |
| DT | - | No explicit conversion | - | |
| DTL | - | - | | |
| TOD | - | - | | |
| LTOD | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. If the source value is outside the value range of LTOD, the destination data type remains unchanged. | LTIME_TO_LTOD | |
| DATE | - | No explicit conversion | - | |
| STRING | - | - | | |
| WSTRING | - | - | | |
| CHAR | - | - | | |
| WCHAR | - | - | | |
| x: Conversion possible - : Conversion not possible 1) Bit strings (BYTE, WORD, DWORD, LWORD) and the data types CHAR and WCHAR are initially extended to the necessary width, and then the bits are copied. The source type determines the interpretation. | | | | |
See also

Implicit conversion of LTIME (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) LTIME (IEC time) (S7-1500, S7-1200 G2)

Date and time-of-day (S7-1500, S7-1200 G2) Explicit conversion of DT (S7-1500, S7-1200 G2)
| Explicit conversion of DT |
|---|
Options for explicit conversion

The following table shows the options and instructions for the explicit conversion of the DT data type:

| Source | Destination | Conversion | Explanation | Mnemonics of the instruction |
|---|---|---|---|---|
| DT | BOOL | - | No explicit conversion | - |
| BYTE | - | - | | |
| WORD | - | - | | |
| DWORD | - | - | | |
| LWORD | - | - | | |
| SINT | - | - | | |
| USINT | - | - | | |
| INT | - | - | | |
| UINT | - | - | | |
| DINT | - | - | | |
| UDINT | - | - | | |
| LINT | - | - | | |
| ULINT | - | - | | |
| REAL | - | - | | |
| LREAL | - | - | | |
| S5TIME | - | - | | |
| TIME | - | - | | |
| LTIME | - | - | | |
| LDT | X | A conversion of the source value into the destination data type takes place here (for example, DT#1990-1-2-0:0:1.0 becomes LDT#1990-1-2-0:0:1.0) | DT_TO_LDT | |
| DTL | X | A conversion of the source value into the destination data type takes place here (for example, DT#1990-1-2-0:0:1.0 becomes DTL#1990-1-2-0:0:1.0) | DT_TO_DTL | |
| TOD | X | A conversion of the source value into the destination data type takes place here (for example, DT#1990-1-2-0:0:1.0 becomes TOD#1990-1-2-0:0:1.0) | DT_TO_TOD | |
| LTOD | X | A conversion of the source value into the destination data type takes place here (for example, DT#1990-1-2-0:0:1.0 becomes LTOD#1990-1-2-0:0:1.0) | DT_TO_LTOD | |
| DATE | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | DT_TO_DATE | |
| STRING | - | No explicit conversion | - | |
| WSTRING | - | - | | |
| CHAR | - | - | | |
| WCHAR | - | - | | |
| x: Conversion possible - : Conversion not possible | | | | |
See also

Implicit conversion of DT (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) DATE_AND_TIME (date and time of day) (S7-1500)

Explicit conversion of LDT (S7-1500, S7-1200 G2)
| Explicit conversion of LDT |
|---|
Options for explicit conversion

The following table shows the options and instructions for the explicit conversion of the LDT data type:

| Source | Destination | Conversion | Explanation | Mnemonics of the instruction |
|---|---|---|---|---|
| LDT | BOOL | - | No explicit conversion | - |
| BYTE1) | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | LDT_TO_BYTE | |
| WORD1) | X | LDT_TO_WORD | | |
| DWORD1) | X | LDT_TO_DWORD | | |
| LWORD1) | X | LDT_TO_LWORD | | |
| SINT | X | LDT_TO_SINT | | |
| USINT | X | LDT_TO_USINT | | |
| INT | X | LDT_TO_INT | | |
| UINT | X | LDT_TO_UINT | | |
| DINT | X | LDT_TO_DINT | | |
| UDINT | X | LDT_TO_UDINT | | |
| LINT | X | LDT_TO_LINT | | |
| ULINT | X | LDT_TO_ULINT | | |
| REAL | - | No explicit conversion | - | |
| LREAL | - | - | | |
| S5TIME | - | - | | |
| TIME | - | - | | |
| LTIME | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | LDT_TO_LTIME | |
| DT | X | A conversion of the source value into the destination data type takes place here (for example, LDT#1990-1-2-0:0:1.0 becomes DT#1990-1-2-0:0:1.0) | LDT_TO_DT | |
| DTL | X | A conversion of the source value into the destination data type takes place here (for example, LDT#1990-1-2-0:0:1.0 becomes DTL#1990-1-2-0:0:1.0) | LDT_TO_DTL | |
| TOD | X | A conversion of the source value into the destination data type takes place here (for example, LDT#1990-1-2-0:0:1.0 becomes TOD#1990-1-2-0:0:1.0) | LDT_TO_TOD | |
| LTOD | X | A conversion of the source value into the destination data type takes place here (for example, LDT#1990-1-2-0:0:1.0 becomes LTOD#1990-1-2-0:0:1.0) | LDT_TO_LTOD | |
| DATE | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | LDT_TO_DATE | |
| STRING | - | No explicit conversion | - | |
| WSTRING | - | - | | |
| CHAR | - | - | | |
| WCHAR | - | - | | |
| x: Conversion possible - : Conversion not possible 1) Bit strings (BYTE, WORD, DWORD, LWORD) and the data types CHAR and WCHAR are initially extended to the necessary width, and then the bits are copied. The source type determines the interpretation. | | | | |
See also

Implicit conversion of LDT (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) LDT (DATE_AND_LTIME) (S7-1500, S7-1200 G2)

Explicit conversion of DTL (S7-1500, S7-1200 G2)
| Explicit conversion of DTL |
|---|
Options for explicit conversion

The following table shows the options and instructions for the explicit conversion of the DTL data type:

| Source | Destination | Conversion | Explanation | Mnemonics of the instruction |
|---|---|---|---|---|
| DTL | BOOL | - | No explicit conversion | - |
| BYTE | - | - | | |
| WORD | - | - | | |
| DWORD | - | - | | |
| LWORD | - | - | | |
| SINT | - | - | | |
| USINT | - | - | | |
| INT | - | - | | |
| UINT | - | - | | |
| DINT | - | - | | |
| UDINT | - | - | | |
| LINT | - | - | | |
| ULINT | - | - | | |
| REAL | - | - | | |
| LREAL | - | - | | |
| S5TIME | - | - | | |
| TIME | - | - | | |
| LTIME | - | - | | |
| LDT | X | A conversion of the source value into the destination data type takes place here (for example, DTL#1990-1-2-0:0:1.0 becomes LDT#1990-1-2-0:0:1.0) | DTL_TO_LDT | |
| DT | X | A conversion of the source value into the destination data type takes place here (for example, DTL#1990-1-2-0:0:1.0 becomes DT#1990-1-2-0:0:1.0) | DTL_TO_DT | |
| TOD | X | During the conversion, the time of day is extracted from the DTL format and written to the destination data type. | DTL_TO_TOD, T_CONV | |
| LTOD | X | DTL_TO_LTOD | | |
| DATE | X | During the conversion, the date is extracted from the DTL format and written to the destination data type. The enable output ENO is set to "0" in the event of overflow. | DTL_TO_DATE, T_CONV | |
| STRING | - | No explicit conversion | - | |
| WSTRING | - | - | | |
| CHAR | - | - | | |
| WCHAR | - | - | | |
| x: Conversion possible - : Conversion not possible | | | | |
See also

Implicit conversion of DTL (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) DTL (S7-1200, S7-1500, S7-1200 G2)

Explicit conversion of DATE (S7-1500, S7-1200 G2)
| Explicit conversion of DATE |
|---|
Options for explicit conversion

The following table shows the options and instructions for the explicit conversion of the DATE data type:

| Source | Target | Conversion | Explanation | Mnemonics of the instruction |
|---|---|---|---|---|
| DATE | BOOL | - | No explicit conversion | - |
| BYTE1) | X | The bit pattern of the source value is transferred unchanged, right-justified, to the target data type. | DATE_TO_BYTE | |
| WORD1) | X | DATE_TO_WORD | | |
| DWORD1) | X | DATE_TO_DWORD | | |
| LWORD1) | X | DATE_TO_LWORD | | |
| SINT | X | The number of days since 1/1/1990 is returned as result. | DATE_TO_SINT | |
| USINT | X | DATE_TO_USINT | | |
| INT | X | DATE_TO_INT | | |
| UINT | X | DATE_TO_UINT | | |
| DINT | X | DATE_TO_DINT | | |
| UDINT | X | DATE_TO_UDINT | | |
| LINT | X | DATE_TO_LINT | | |
| ULINT | X | DATE_TO_ULINT | | |
| REAL | - | No explicit conversion | - | |
| LREAL | - | - | | |
| S5TIME | - | - | | |
| TIME | - | - | | |
| LTIME | - | - | | |
| DT | X | The conversion sets the date in the destination type. | DATE_TO_DT | |
| LDT | X | DATE_TO_LDT | | |
| DTL 2) | X | DATE_TO_DTL | | |
| TOD | - | No explicit conversion | - | |
| LTOD | - | - | | |
| STRING | - | - | | |
| WSTRING | - | - | | |
| CHAR | - | - | | |
| WCHAR | - | - | | |
| x: Conversion possible - : Conversion not possible 1) Bit strings (BYTE, WORD, DWORD, LWORD) and the data types CHAR and WCHAR are initially extended to the necessary width, and then the bits are copied. The source type determines the interpretation. 2) The data type DTL is initialized as follows: 1970-1-1-0:0:0. Conversion from DATE_TO_DTL only sets the corresponding part of the DTL. The rest of the DTL remains as it was initialized. This results in the following differences for the instructions "T_COMBINE" and "T_CONV": T_COMBINE(D#2015-24-12, LTOD#12:13:14) returns DTL#2015-24-12-12:13:14 myDTL := T_CONV(D#2015-24-12); myDTL := T_CONV(LTOD#12:13:14) results in myDTL = DTL#1970-1-1-12:13:14 | | | | |
See also

Implicit conversion of DATE (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) DATE

Explicit conversion of TOD (S7-1500, S7-1200 G2)
| Explicit conversion of TOD |
|---|
Options for explicit conversion

The following table shows the options and instructions for the explicit conversion of the TOD data type:

| Source | Destination | Conversion | Explanation | Mnemonics of the instruction |
|---|---|---|---|---|
| TOD | BOOL | - | No explicit conversion | - |
| BYTE1) | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | TOD_TO_BYTE | |
| WORD1) | X | TOD_TO_WORD | | |
| DWORD1) | X | TOD_TO_DWORD | | |
| LWORD1) | X | TOD_TO_LWORD | | |
| SINT | X | The number of milliseconds since midnight is returned as result. | TOD_TO_SINT | |
| USINT | X | TOD_TO_USINT | | |
| INT | X | TOD_TO_INT | | |
| UINT | X | TOD_TO_UINT | | |
| DINT | X | TOD_TO_DINT | | |
| UDINT | X | The result of the conversion corresponds to the number of milliseconds since the start of day (0:00). | TOD_TO_UDINT, T_CONV | |
| LINT | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | TOD_TO_LINT | |
| ULINT | X | TOD_TO_ULINT | | |
| REAL | - | No explicit conversion | - | |
| LREAL | - | - | | |
| S5TIME | - | - | | |
| TIME | X | The duration since midnight is returned as result. | TOD_TO_TIME | |
| LTIME | - | No explicit conversion | - | |
| DT | X | The conversion sets the time in the destination data type. | TOD_TO_DT | |
| LDT | X | TOD_TO_LDT | | |
| DTL | X | TOD_TO_DTL | | |
| DATE | - | No explicit conversion | - | |
| LTOD | X | A conversion of the source value into the destination data type takes place here (for example, TOD#1:0:0.0 becomes LTOD#1:0:0.0) | TOD_TO_LTOD | |
| STRING | - | No explicit conversion | - | |
| WSTRING | - | - | | |
| CHAR | - | - | | |
| WCHAR | - | - | | |
| x: Conversion possible - : Conversion not possible 1) Bit strings (BYTE, WORD, DWORD, LWORD) and the data types CHAR and WCHAR are initially extended to the necessary width, and then the bits are copied. The source type determines the interpretation. | | | | |
See also

Implicit conversion of TOD (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) TIME_OF_DAY (TOD)

Explicit conversion of LTOD (S7-1500, S7-1200 G2)
| Explicit conversion of LTOD |
|---|
Options for explicit conversion

The following table shows the options and instructions for the explicit conversion of the LTOD data type:

| Source | Destination | Conversion | Explanation | Mnemonics of the instruction |
|---|---|---|---|---|
| LTOD | BOOL | - | No explicit conversion | - |
| BYTE1) | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | LTOD_TO_BYTE | |
| WORD1) | X | LTOD_TO_WORD | | |
| DWORD1) | X | LTOD_TO_DWORD | | |
| LWORD1) | X | LTOD_TO_LWORD | | |
| SINT | X | The number of nanoseconds since midnight is returned as result. | LTOD_TO_SINT | |
| USINT | X | LTOD_TO_USINT | | |
| INT | X | LTOD_TO_INT | | |
| UINT | X | LTOD_TO_UINT | | |
| DINT | X | LTOD_TO_DINT | | |
| UDINT | X | LTOD_TO_UDINT | | |
| LINT | X | LTOD_TO_LINT | | |
| ULINT | X | LTOD_TO_ULINT, T_CONV | | |
| REAL | - | No explicit conversion | - | |
| LREAL | - | - | | |
| S5TIME | - | - | | |
| TIME | - | - | | |
| LTIME | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | LTOD_TO_LTIME | |
| DT | X | A conversion of the source value into the destination data type takes place here (for example, LTOD#1:0:0.0 becomes DT#1:0:0.0) | LTOD_TO_DT | |
| LDT | X | A conversion of the source value into the destination data type takes place here (for example, LTOD#1:0:0.0 becomes LDT#1:0:0.0) | LTOD_TO_LDT | |
| DTL | X | A conversion of the source value into the destination data type takes place here (for example, LTOD#1:0:0.0 becomes DTL#1:0:0.0) | LTOD_TO_DTL | |
| DATE | - | No explicit conversion | - | |
| TOD | X | A conversion of the source value into the destination data type takes place here (for example, LTOD#1:0:0.0 becomes TOD#1:0:0.0) | LTOD_TO_TOD | |
| STRING | - | No explicit conversion | - | |
| WSTRING | - | - | | |
| CHAR | - | - | | |
| WCHAR | - | - | | |
| x: Conversion possible - : Conversion not possible 1) Bit strings (BYTE, WORD, DWORD, LWORD) and the data types CHAR and WCHAR are initially extended to the necessary width, and then the bits are copied. The source type determines the interpretation. | | | | |
See also

Implicit conversion of LTOD (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) LTOD (LTIME_OF_DAY) (S7-1500, S7-1200 G2)

String (S7-1500, S7-1200 G2) Explicit conversion of CHAR (S7-1500, S7-1200 G2)
| Explicit conversion of CHAR |
|---|
Options for explicit conversion

The following table shows the options and instructions for the explicit conversion of the CHAR data type:

| Source | Destination | Conversion | Explanation | Mnemonics of the instruction |
|---|---|---|---|---|
| CHAR | BOOL | - | No explicit conversion | - |
| BYTE1) | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | CHAR_TO_BYTE | |
| WORD1) | X | CHAR_TO_WORD | | |
| DWORD1) | X | CHAR_TO_DWORD | | |
| LWORD1) | X | CHAR_TO_LWORD | | |
| SINT | X | CHAR_TO_SINT | | |
| USINT | X | CHAR_TO_USINT | | |
| INT | X | CHAR_TO_INT | | |
| UINT | X | CHAR_TO_UINT | | |
| DINT | X | CHAR_TO_DINT | | |
| UDINT | X | CHAR_TO_UDINT | | |
| LINT | X | CHAR_TO_LINT | | |
| ULINT | X | CHAR_TO_ULINT | | |
| REAL | - | No explicit conversion | - | |
| LREAL | - | - | | |
| S5TIME | - | - | | |
| TIME | - | - | | |
| LTIME | - | - | | |
| DT | - | - | | |
| LDT | - | - | | |
| DTL | - | - | | |
| TOD | - | - | | |
| LTOD | - | - | | |
| DATE | - | - | | |
| STRING | X | The value is converted into the first character in the character string (STRING). The length "1" is set after conversion if the character string length is not defined. If the character string length is defined, it remains unchanged following conversion. | CHAR_TO_STRING, S_CONV | |
| WSTRING | - | No explicit conversion | - | |
| WCHAR | X | | CHAR_TO_WCHAR | |
| x: Conversion possible - : Conversion not possible 1) Bit strings (BYTE, WORD, DWORD, LWORD) and the data type WCHAR are initially extended to the necessary width, and then the bits are copied. The source type determines the interpretation. | | | | |
See also

Implicit conversion of CHAR (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) CHAR

Explicit conversion of WCHAR (S7-1500, S7-1200 G2)
| Explicit conversion of WCHAR |
|---|
Options for explicit conversion

The following table shows the options and instructions for the explicit conversion of the WCHAR data type:

| Source | Destination | Conversion | Explanation | Mnemonics of the instruction |
|---|---|---|---|---|
| WCHAR | BOOL | - | No explicit conversion | - |
| BYTE1) | X | The bit pattern of the source value is transferred unchanged right-justified to the destination data type. | WCHAR_TO_BYTE | |
| WORD1) | X | WCHAR_TO_WORD | | |
| DWORD1) | X | WCHAR_TO_DWORD | | |
| LWORD1) | X | WCHAR_TO_LWORD | | |
| SINT | X | WCHAR_TO_SINT | | |
| USINT | X | WCHAR_TO_USINT | | |
| INT | X | WCHAR_TO_INT | | |
| UINT | X | WCHAR_TO_UINT | | |
| DINT | X | WCHAR_TO_DINT | | |
| UDINT | X | WCHAR_TO_UDINT | | |
| LINT | X | WCHAR_TO_LINT | | |
| ULINT | X | WCHAR_TO_ULINT | | |
| REAL | - | No explicit conversion | - | |
| LREAL | - | - | | |
| S5TIME | - | - | | |
| TIME | - | - | | |
| LTIME | - | - | | |
| DT | - | - | | |
| LDT | - | - | | |
| DTL | - | - | | |
| TOD | - | - | | |
| LTOD | - | - | | |
| DATE | - | - | | |
| STRING | - | | - | |
| WSTRING | X | The value is converted into the first character in the character string (WSTRING). The length "1" is set after conversion if the character string length is not defined. If the character string length is defined, it remains unchanged following conversion. | WCHAR_TO_WSTRING | |
| CHAR | X | | WCHAR_TO_CHAR | |
| x: Conversion possible - : Conversion not possible 1) Bit strings (BYTE, WORD, DWORD, LWORD) and the data type CHAR are initially extended to the necessary width, and then the bits are copied. The source type determines the interpretation. | | | | |
See also

Overview of data type conversion (S7-1500, S7-1200 G2) WCHAR (S7-1200, S7-1500, S7-1200 G2) Implicit conversion of WCHAR (S7-1500, S7-1200 G2)

Explicit conversion of STRING (S7-1500, S7-1200 G2)
| Explicit conversion of STRING |
|---|
Options for explicit conversion

The following table shows the options and instructions for the explicit conversion of the STRING data type:

| Source | Destination | Conversion | Explanation | Mnemonics of the instruction |
|---|---|---|---|---|
| STRING | BOOL | - | No explicit conversion | - |
| BYTE | - | - | | |
| WORD | - | - | | |
| DWORD | - | - | | |
| LWORD | - | - | | |
| SINT | X | Conversion begins with the first character in the character string (STRING) and stops at the end of the string or at the first inadmissible character. The following characters are admissible for conversion: Digit Sign Dot The first character in the character string may be a sign (+, -) or a digit. Leading spaces are ignored. The dot is used as separation for the conversion of floating-point numbers. The exponential notation "e" or "E" is not permitted. The comma as thousand separator to the left of the decimal point is permitted but is ignored. If the layout of the character string is invalid for the conversion or an overflow occurs, then the enable output ENO will be set to "0". | STRING_TO_SINT, S_CONV, STRG_VAL | |
| USINT | X | STRING_TO_USINT, S_CONV, STRG_VAL | | |
| INT | X | STRING_TO_INT, S_CONV, STRG_VAL | | |
| UINT | X | STRING_TO_UINT, S_CONV, STRG_VAL | | |
| DINT | X | STRING_TO_DINT, S_CONV, STRG_VAL | | |
| UDINT | X | STRING_TO_UDINT, S_CONV, STRG_VAL | | |
| LINT | X | STRING_TO_LINT, S_CONV, STRG_VAL | | |
| ULINT | X | STRING_TO_ULINT, S_CONV, STRG_VAL | | |
| REAL | X | STRING_TO_REAL, S_CONV, STRG_VAL | | |
| LREAL | X | STRING_TO_LREAL, S_CONV, STRG_VAL | | |
| S5TIME | - | No explicit conversion | - | |
| TIME | - | - | | |
| LTIME | - | - | | |
| DT | - | - | | |
| LDT | - | - | | |
| DTL | - | - | | |
| TOD | - | - | | |
| LTOD | - | - | | |
| DATE | - | - | | |
| CHAR | X | The first character in the character string (STRING) is transferred to the destination data type. The value "0" is written to the destination data type if the character string is empty. | STRING_TO_CHAR, S_CONV | |
| WCHAR | - | No explicit conversion | - | |
| WSTRING | X | | STRING_TO_WSTRING | |
| x: Conversion possible - : Conversion not possible | | | | |
See also

Implicit conversion of STRING (S7-1500, S7-1200 G2) Overview of data type conversion (S7-1500, S7-1200 G2) STRING

Explicit conversion of WSTRING (S7-1500, S7-1200 G2)
| Explicit conversion of WSTRING |
|---|
Options for explicit conversion

The following table shows the options and instructions for the explicit conversion of the WSTRING data type:

| Source | Destination | Conversion | Explanation | Mnemonics of the instruction |
|---|---|---|---|---|
| WSTRING | BOOL | - | No explicit conversion | - |
| BYTE | - | - | | |
| WORD | - | - | | |
| DWORD | - | - | | |
| LWORD | - | - | | |
| SINT | X | Conversion begins with the first character in the character string (WSTRING) and stops at the end of the string or at the first inadmissible character. The following characters are admissible for conversion: Digit Sign Dot The first character in the character string may be a sign (+, -) or a digit. Leading spaces are ignored. The dot is used as separation for the conversion of floating-point numbers. The exponential notation "e" or "E" is not permitted. The comma as thousand separator to the left of the decimal point is permitted but is ignored. If the layout of the character string is invalid for the conversion or an overflow occurs, then the enable output ENO will be set to "0". | WSTRING_TO_SINT, S_CONV, STRG_VAL | |
| USINT | X | WSTRING_TO_USINT, S_CONV, STRG_VAL | | |
| INT | X | WSTRING_TO_INT, S_CONV, STRG_VAL | | |
| UINT | X | WSTRING_TO_UINT, S_CONV, STRG_VAL | | |
| DINT | X | WSTRING_TO_DINT, S_CONV, STRG_VAL | | |
| UDINT | X | WSTRING_TO_UDINT, S_CONV, STRG_VAL | | |
| LINT | X | WSTRING_TO_LINT, S_CONV, STRG_VAL | | |
| ULINT | X | WSTRING_TO_ULINT, S_CONV, STRG_VAL | | |
| REAL | X | WSTRING_TO_REAL, S_CONV, STRG_VAL | | |
| LREAL | X | WSTRING_TO_LREAL, S_CONV, STRG_VAL | | |
| S5TIME | - | No explicit conversion | - | |
| TIME | - | - | | |
| LTIME | - | - | | |
| DT | - | - | | |
| LDT | - | - | | |
| DTL | - | - | | |
| TOD | - | - | | |
| LTOD | - | - | | |
| DATE | - | - | | |
| CHAR | - | - | | |
| WCHAR | X | The first character in the character string (WSTRING) is transferred to the destination data type. The value "0" is written to the destination data type if the character string is empty. | WSTRING_TO_WCHAR | |
| STRING | X | | WSTRING_TO_STRING | |
| x: Conversion possible - : Conversion not possible | | | | |
See also

Overview of data type conversion (S7-1500, S7-1200 G2) WSTRING (S7-1200, S7-1500, S7-1200 G2) Implicit conversion of WSTRING (S7-1500, S7-1200 G2)

Data type conversion for S7-1200 (S7-1200)
