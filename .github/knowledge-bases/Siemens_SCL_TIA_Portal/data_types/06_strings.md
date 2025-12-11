# 06 Strings

# Character

CHAR
| CHAR |
|---|
Description

A tag of the CHAR (Character) data type has a length of 8 bits and occupies one BYTE of memory.

The
CHAR data type stores a single character in ASCII coding. You can find
information on the encoding of special characters under "See also >
STRING".

The following table shows the value range of the CHAR data type:

| Length (bits) | Format | Value range | Example of value inputs |
|---|---|---|---|
| 8 | ASCII characters | ASCII character set | 'A', CHAR#'A' |
See also

Overview of the valid data types STRING

WCHAR (S7-1200, S7-1500, S7-1200 G2)
| WCHAR |
|---|
Description

A tag of the data type WCHAR (Wide Characters) has a length of 16 bits and occupies two BYTE of memory.

The
data type WCHAR saves a single character of an expanded character set
in UTF-16 coding. However, only a subset of the entire Unicode range is
covered. Characters that cannot be displayed are made displayable using
an escape character.

The following table shows the value range of the WCHAR data type:

| Length (bits) | Format | Value range | Example of value input |
|---|---|---|---|
| 16 | Unicode | $0000 - $D7FF | WCHAR#'a' |
See also

Overview of the valid data types


# Character strings

STRING
| STRING |
|---|
Description

An
operand of the STRING data type saves several characters in a character
string that can consist of up to 254 characters. In a character string,
all characters of the codepage created on the system are permitted. The
characters are specified in single quotation marks.

A
character string can also contain special characters. The escape
character $ is used to identify control characters, dollar signs and
single quotation marks.

| Note Different code pages Please note that the special characters are coded using the code page currently set in Windows. This means that a string that contains special characters can be displayed differently on a different operating system with a different code page. The dependency of the codepage on the created system makes an international use of the user program more difficult. Only the characters from the 7-bit ASCII coding are internationally valid. |
|---|
The following table shows the properties of a STRING tag:

| Length (bytes) | Format | Value range | Example of value input |
|---|---|---|---|
| n + 2 1) | ASCII character string incl. special characters | 0 to 254 characters | 'Name' STRING#'NAME' STRING#'Na... (The actual length of the string is longer than the space available on the screen.) STRING#'' (The string is empty.) |
| 1) An operand of the STRING data type occupies two bytes more than the specified maximum length in the memory. | | | |
The table below shows examples for the notation of special characters:

| Character | Hex | Meaning | Example |
|---|---|---|---|
| $L or $l | 0A | Line feed | '$LText', '$0AText' |
| $N | 0A and 0D | Line break The line break occupies 2 characters in the character string and is converted to $R$L in the display in the editor. | '$NText', '$0A$0DText' |
| $P or $p | 0C | Page feed | '$PText', '$0CText' |
| $R or $r | 0D | Carriage return (CR) | '$RText','$0DText' |
| $T or $t | 09 | Tab | '$TText', '$09Text' |
| $$ | 24 | Dollar sign | '100$$', '100$24' |
| $' | 27 | Single quotation mark | '$'Text$'','$27Text$27' |
If
the escape character $ is followed by a letter from the table, the
character indicated in the table is entered in the string. If the escape
character $ is followed by a letter that is not in the table, this
letter is entered in the string. If the escape character $ is followed
by two hexadecimal digits or only one digit, this code is entered in the
string.

Use in the watch table

The
following applies to a CPU of the S7-300/400 series: If a tag of the
STRING data type is being monitored, only the first 30 characters will
be displayed. If the actual length is greater than 30 characters, an
ellipsis (…) is displayed instead of the final apostrophe ('). STRING
values with more than 30 characters cannot be used for modifying.

Maximum length of a character string

The
maximum length of the character string can be specified during the
declaration of an operand using square brackets after the keyword STRING
(for example, STRING[4]). You can also use local or global constants to
declare the maximum length (for example, STRING[#loc_const] or
STRING["glob_const"]). If the specification of the maximum length is
omitted, the standard length of 254 characters is set for the respective
operand.

You can find additional information about using local or global constants to declare the maximum length here:

- Declaring the block interface: Declare variables of the STRING and WSTRING data types

- Programming data blocks: Declaring tags of the STRING data type

- Examples of using constants

If
the actual length of a specified character string is shorter than the
declared maximum length, the characters are written to the character
string left-justified and the remaining character spaces remain
undefined. Only occupied character spaces that define the actual length
of the string are considered for the value processing and all displays.

| Note For S7-300/400 CPUs, please note: If a temporary tag of the STRING data type was defined, you must describe the BYTE "Max. length of string" with the defined length before you use the tags in the user program. |
|---|
Transferring a STRING for parameter supply

You can transfer the STRING data type as a parameter. You can find additional information on parameter supply with STRING here:

- Transferring a tag of the STRING or WSTRING data type

- For S7-1200/1500: Valid data types in the block interface

- For S7-300/400: Valid data types in the block interface

Example

The example below shows the byte sequence if the STRING[4] data type is specified with output value 'QB':

See also

Overview of the valid data types Basics of constants Data type conversion for S7-1200 (S7-1200)

Structure of a STRING tag
| Structure of a STRING tag |
|---|
Introduction

A
tag with STRING data type (character string) is maximum 256 characters
long with 254 bytes user data. It starts in a non-optimized block at a
word limit (at a byte with even address). In an optimized block it can
start at any byte limit.

When
tags are created their maximum length is specified. In the case of the
preassignment or editing of the character string, the current length
(the actually used length of the character string = number of valid
characters) is entered. The maximum length is located in the first byte
of the character string. The current length is in the second byte. This
is followed by the characters, coded according to the codepage set in
Windows.

Structure of a STRING tag

WSTRING (S7-1200, S7-1500, S7-1200 G2)
| WSTRING |
|---|
Description

An
operand of data type WSTRING (Wide Character String) stores several
Unicode characters of data type WCHAR in one character string. If you do
not specify a length, the character string has a preset length of 254
characters. In a character string, all characters that are supported by
the operating system are permitted. This means you can also use Chinese
characters in a character string. Windows supports only some (but
sufficient number) of the characters defined in Unicode.

| Note Coding STEP 7 prohibits all coding of $D000 to $FFFF. |
|---|
When
declaring an operand of data type WSTRING you can define its length
using square brackets (for example WSTRING[10]). If you do not specify a
length, the length of the WSTRING is set to 254 characters by default.
You can declare a length of up to 16382 characters (WSTRING[16382]).

The specification of the characters occurs in single quotes and always with the qualifier WSTRING#.

The following table shows the properties of a WSTRING tag:

| Length (WORD) | Format | Value range | Example of value input |
|---|---|---|---|
| n + 2 1) | Unicode character string; n specifies the length of the character string. | Preset value: 0 to 254 characters Max. possible value: 0 to 16382 | WSTRING#'Hello World' WSTRING#'Hello Wo... (The actual length of the string is longer than the space available on the screen.) WSTRING#'' (The string is empty.) |
| 1) An operand of the WSTRING data type occupies two WORDs more in the memory than the specified maximum length. | | | |
A
character string can also contain special characters. The escape
character $ is used to identify control characters, dollar signs and
single quotation marks.

The table below shows examples for the notation of special characters:

| Character | Hex | Meaning | Example |
|---|---|---|---|
| $L or $l | 000A | Line feed | '$LText', '$000AText' |
| $N | 000A and 000D | Line break The line break occupies 2 characters in the character string and is converted to $R$L in the display in the editor. | '$NText', '$000A$000DText' |
| $P or $p | 000C | Page feed | '$PText', '$000CText' |
| $R or $r | 000D | Carriage return (CR) | '$RText','$000DText' |
| $T or $t | 0009 | Tab | '$TText', '$0009Text' |
| $$ | 0024 | Dollar sign | '100$$', '100$0024' |
| $' | 0027 | Single quotation mark | '$'Text$'','$0027Text$0027' |
If
the escape character $ is followed by a letter from the table, the
character indicated in the table is entered in the string. If the escape
character $ is followed by a letter that is not in the table, this
letter is entered in the string. If the escape character $ is followed
by four hexadecimal digits, this code is entered in the string.

| Note Conversion of WSTRING tags Implicit conversion of the WSTRING data type is not possible. Explicit conversion of the WSTRING data type to STRING is generally possible. However, as standard, it is only possible to convert characters in the code range from 0 - 127 in all Windows code pages. For all characters outside this range, the code page character and the lower byte of the Unicode character must be in exactly the same position for the conversion to work without errors. |
|---|
Use in the watch table

If
a tag of the WSTRING data type is being monitored, only the first 254
characters are displayed. If the actual length is greater than 254
characters, an ellipsis (…) is displayed instead of the closing
apostrophe ('). WSTRING values with more than 254 characters cannot be
used for modifying.

Use in SCL

In
rare cases, the WSTRING results are truncated when you create very
large WSTRINGs using WSTRING-generating functions (e.g. CONCAT, INSERT,
JOIN, SPLIT, LEFT, MID, RIGHT) in SCL.

Therefore, check the ENO of these functions for FALSE to see if the WSTRING has been truncated.

Maximum length of a character string

The
maximum length of the character string can be specified during the
declaration of an operand using square brackets after the keyword
WSTRING (for example, WSTRING[4]). You can also use local or global
constants to declare the maximum length (for example,
WSTRING[#loc_const] or WSTRING["glob_const"]). If the specification of
the maximum length is omitted, the standard length of 254 characters is
set for the respective operand.

You can find additional information about using local or global constants to declare the maximum length here:

- Declaring the block interface: Declare variables of the STRING and WSTRING data types

- Programming data blocks: Declaring tags of the STRING data type

- Examples of using constants

If
the actual length of a specified character string is shorter than the
declared maximum length, the characters are written to the character
string left-justified and the remaining character spaces remain
undefined. Only occupied character spaces are considered in the value
processing.

Transferring a WSTRING for parameter supply

Operands of the data type WSTRING can be transferred as parameters up to the maximum length for blocks with "optimized" access.

For
function blocks (FB) with "standard" access, operands of the data type
WSTRING can be declared as parameters in all sections of the block
interface except in the section "InOut". For a function (FC) with
"standard" access, only operands of the WSTRING data type can be
transferred as parameters.

The
function value of an FC in the "Return" section and expressions in the
SCL programming language are another exception to this rule. In these
cases, the WSTRING tag must not be longer than 1022 characters.

The
declared lengths of formal and actual parameters may be different. You
can find additional information on parameter supply with WSTRING here:

- Transferring a tag of the STRING or WSTRING data type

- Valid data types in the block interface

Example

The example below shows the byte sequence if the WSTRING[4] data type is specified with output value 'QB':

See also

Overview of the valid data types Constants

Addressing individual characters of a STRING or WSTRING
| Addressing individual characters of a STRING or WSTRING |
|---|
Addressing individual characters of a STRING or WSTRING

Use the syntax StringName[i] to
access an individual character of a STRING or WSTRING tag. The counting
index "i" begins with "1". Thus, you access the first character of the
string with StringName[1].

You cannot access individual characters of a STRING or WSTRING constant.

Examples

The following examples show the addressing of (W)STRINGs:

| Addressing | Explanation |
|---|---|
| #myWSTRING[3] | Addresses the third character of the WSTRING. |
| "myDB".mySTRING[3] | Addresses the third character of the STRING in the data block. |
| myNamespace.myDB.mySTRING[3] | Addresses the third character of the STRING in the data block in the "myNamespace" namespace. |

| Note Calling and addressing blocks in namespaces Blocks located in namespaces are represented in the program code in IEC-compliant notation: The block name is not in quotation marks. The namespace precedes the block name, separated by a dot. You can find detailed information on the notation of namespaces under: Introduction to namespaces |
|---|
Troubleshooting W(STRING) access

Access
errors result during runtime when you access a character that is
located outside the STRING length. On read access to the character
string, you receive the character '$00' or '$0000'; write access to the
character string is not executed. If the instruction has the enable
output ENO, ENO is set to the signal state FALSE. The CPU does not
change to STOP.

The only exception is when the character is written directly after the actual length of the character string.

The
following example shows the string 'Hello' with the actual length of 5.
The 27th character of the STRING lies outside the actual length and
cannot therefore be written. The STRING remains unchanged; the result of
the assignment is 'hello'.

| SCL |
|---|
| MyDB.mystring := 'hello'; |
| MyDB.mystring[27] := CHAR_TO_BYTE('!'); |

The
following example shows the specified exception: The character is
written directly behind the STRING to the 6th character. The result of
the assignment is 'hello!'.

| SCL |
|---|
| MyDB.mystring := 'hello'; |
| MyDB.mystring[6] := CHAR_TO_BYTE('!'); |

Where possible, use instructions from the "Extended instructions > String + Char" pane to handle STRINGs.

| |
|---|
| CONCAT(IN1 := 'hello', IN2 := '!'); |
Transferring a tag of the STRING or WSTRING data type
| Transferring a tag of the STRING or WSTRING data type |
|---|
Description

You
can transfer tags of the STRING or WSTRING data type as parameters. The
following table shows the rules that apply to the (W)STRING transfer in
the various CPU families:

| CPU family | Data type | Rules for transfer at the block call |
|---|---|---|
| S7-300/400 | STRING | The declared lengths of formal and actual parameters must be identical. |
| S7-1200/1500 | STRING WSTRING | The declared lengths of formal and actual parameters may be different. If the declared length of the target parameter during runtime is insufficient to accept the (W)STRING, the (W)STRING is truncated and the enable output ENO is set to FALSE. In the programming editor, a gray rectangle at the parameter indicates that (W)STRING might be truncated during runtime. Exception: When calling STL blocks, the declared lengths of formal and actual parameters must always be identical. |
The
following figure shows a block call in which the lengths of the
declared formal and actual parameters differ. Due to the different
declared lengths, both "Input_String_20" and "Output_String_10" could be
truncated during runtime.

See also

Rules for supplying block parameters

PLC data types (UDT)
