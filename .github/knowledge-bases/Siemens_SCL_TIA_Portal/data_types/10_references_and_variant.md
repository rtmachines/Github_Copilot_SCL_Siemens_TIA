# 10 References And Variant

# References (S7-1500, S7-1200 G2)

Basic information about references (S7-1500, S7-1200 G2)
| Basic information about references |
|---|
Description

A reference is a tag that itself contains no value but rather points to the memory location of another tag.

References
enable the forwarding of tags beyond block boundaries and thus the
direct manipulation of tag values without having to create a copy of the
tags.

When you
declare the reference you specify from which data type the referenced
tag must be. References are type-safe. This is a key aspect in
particular for control system on which runtime errors need to be
avoided. The restriction, made in IEC, that references must point to
temporary data elements further increases the reliability. In this way
runtime errors are avoidable.

It is ensured that references either refer to a valid memory space of the correct data type or are assigned the value NULL.

Using references in the program

Requirement for using references is a CPU of the S7-1500 series with the firmware version V2.5 or higher.

The following graphic provides an overview of options for using references.

Differences between references and VARIANT

A
tag of VARIANT data type is like a pointer that can point to other tags
of any data type. For this reason, the data type that the VARIANT tag
will point to does not have to be defined yet when the program is
created. The data type is not defined until runtime. A VARIANT tag can
even have different data types in different program cycles. The data
type VARIANT is suitable for creating generic programs and for indirect
addressing. If you want to further process a VARIANT tag in the program
code, however, you need to use special instructions to determine which
data type is currently present. You also cannot directly read and write
VARIANT tags. Rather, special instructions, e.g. VariantGet and
VariantPut must likewise be used for this.

If
you use references, you define the data type when creating the program.
Because the data type does not have to be determined at runtime, the
program will perform better and be more clearly structured. Through
dereferencing you can have direct write or read access to the referenced
tag without having to integrate additional instructions in your
program.

Unlike VARIANT, however, references may only point to data that are located in an optimized memory area.

Examples

The example below shows various possible applications for references.

The block interface contains the "myRefInt" tag that was declared as a reference:

The figure below shows how this tag is used in SCL:

Declaring references (S7-1500, S7-1200 G2)
| Declaring references |
|---|
Description

References
can be declared in the block interface of functions and function
blocks. The following declaration areas are permitted for this purpose:

- FC: Input, Output, Temp, Return

- FB: Temp

- OB: Temp

Reference declarations in structures are not possible.

To
declare references, use keyword "REF_TO" and specify the required data
type of the referenced tag. However, do not yet specify which specific
tag the reference points to:

References can point to the following elements:

| Referenced element | Comments |
|---|---|
| Bit strings | References to BYTE, WORD, DWORD and LWORD are possible. References to BOOL are not possible. |
| Integers | References to integers are possible. |
| Floating-point numbers | References to floating-point numbers are possible. |
| Character strings | References to character strings are possible. Length declarations for character strings are not possible. |
| IEC timers | References to IEC_TIMER and IEC_LTIMER are possible. References to derived data types, such as TON, are not possible. |
| IEC counters | References to IEC_COUNTER / IEC_UCOUNTER, IEC_SCOUNTER / IEC_USCOUNTER, IEC_DCOUNTER / IEC_UDCOUNTER are possible. References to derived data types, such as CTU, are not possible. |
| PLC data types (UDT) | References to PLC data types are possible. |
| System data types (SDT) | References to system data types are possible. |
| ARRAY | References to ARRAYs of the data types listed above are possible. References to ARRAY[*] are not possible. ARRAYs from references are not possible. The following declaration would therefore not be permitted: ARRAY of REF_TO |
| Technology objects | References to technology objects of the "Motion" and "SIMATIC Ident" categories are possible as of firmware V3.0. You can use up to ten references to technology objects in a block. References to ARRAYs of technology objects are not possible. The following declaration would therefore not be permitted: REF_TO ARRAY of |
| Data block | References to an entire data block are only possible if the data block was originally derived from a PLC data type (UDT) or system data type (SDT). |
Initialization

When
a reference tag is created, the system initializes it with the value
NULL. This means that although the reference itself exists, it still
does not refer to any valid memory. If a ZERO reference is accessed
during runtime, a programming error is output. You cannot yourself enter
an initialization in the block interface.

Use the instruction "REF ()" to initialize a reference.

See also: Referencing

Retentivity

References cannot be retentive. However, they can point to retentive data.

| Note Maximum number of reference parameters per block The permissible maximum amount of parameters of data type "REF_TO" in a block depends on various factors, such as the block type and the number of other declared parameters with structured data type (ARRAYs, PLC data types, etc.) as well as the number of declared instances. If the maximum number is exceeded, you receive a message during the compilation process. In this case, you can combine several parameters in a PLC data type (UDT) or in a global data block (DB) and transfer it as a block parameter. |
|---|
See also

Basic information about references (S7-1500, S7-1200 G2) Valid data types in the block interface (S7-1200, S7-1500)

Referencing (S7-1500, S7-1200 G2)
| Referencing |
|---|
Description

The
keyword "REF()" is used to specify the tag to which a previously
declared reference is to point. As parameter, specify the tag to be
referenced. The data type of the tag must correspond exactly to the data
type of the declared reference. This means that a reference with data
type "REF_TO Int" can only point to a tag of data type "Int". No data
type conversion is made.

| Note Transferring "REF()" as an actual parameter during the block call You can also transfer "REF()" as an actual parameter to a called block in whose interface references are declared. See also: Transferring references as block parameters |
|---|
Rules

The following rules apply to referencing:

- The data to which a reference points must be located in an optimized memory space.

- The reference must only point to data in a global DB or static tags.

- The reference must not refer to the following data:

- Temporary local data

- Global tags from the PLC tag table

- Block parameters

- Constants

- Write-protected tags

- The following applies to references to arrays:

- The array limits and dimensions of the reference and the referenced tag must be identical.

- References to arrays with dynamic limits (Array[*]) cannot be created.

- References to ARRAY DBs that are based on a PLC data type must be created as follows:

REF("my_ArrayDB_UDT"."THIS")

REF("my_ArrayDB_UDT"."THIS"[i])

- Technology objects cannot be referenced with REF().

Examples

The
example below shows the interface of a block: The interface contains
several parameters that were declared with data type "REF_TO". When
declaring the reference, you define only the data type of the referenced
tag. You do not yet specify the tag to which the reference points.

In the program code you specify to which specific tag the declared reference parameters should point.

Examples in SCL:

Examples in LAD:

Examples in STL:

See also

Basic information about references (S7-1500, S7-1200 G2) Declaring references (S7-1500, S7-1200 G2)

Dereferencing (S7-1500, S7-1200 G2)
| Dereferencing |
|---|
Description

To
have read or write access to the value of a referenced tag, you use the
caret character "^". This type of access is called "dereferencing".

Examples

The
example below shows the interface of a block: The interface contains
the "myRefInt" parameter that was declared as a reference and a few
static parameters that have already been initialized with a value:

The
figure below shows how the "REF()" instruction is used to specify that
"myRefInt" points to "#a" and how "#a" is used in calculations in SCL.

The
following example shows how to read or write the elements of a
referenced technology object using the caret character. The interface
contains the two reference declarations "myReferenceSpeedAxis" and
"myReferencePositioningAxis":

The following figure shows the write and read access:

See also

Basic information about references (S7-1500, S7-1200 G2)

Standard instructions with references (S7-1500, S7-1200 G2)
| Standard instructions with references |
|---|
You can use references as input or output parameters of assignments or comparison instructions.

You can use dereferenced values as parameters of any instruction, provided they have the correct data type.

Assignment

References
can be assigned to each other like any other tag. In this case, the
address of the reference, not its value, is assigned to the second
reference. References can only be assigned to each other if they refer
to the same data type. No implicit data type conversion is made.

References
to PLC data types, too, must be of the same data type. It is not enough
for both PLC data types to have the same structure.

You can also assign a reference to a VARIANT. In this case the VARIANT must be declared as temporary tag (Temp).

The following rules apply to references to technology objects:

- Two technology objects of the same type can be assigned to each other.

- A derived type can be assigned to its basic type.

- A basic type cannot be assigned to its derived type.

- Assignment to a pointer, e.g. a VARIANT, is not possible.

Comparison

References
can be used in compare instructions. You can use a comparison with NULL
to determine whether a tag has already been assigned to a reference.
This is always advisable when the program flow does not explicitly
ensure that a reference has been initialized.

Other comparisons are not possible.

Examples

The following example shows the use of references in assignments and comparison instructions in SCL:

The following example shows the use in LAD:

See also

Basic information about references (S7-1500, S7-1200 G2)

Assignment attempt to a reference (S7-1500, S7-1200 G2)
| Assignment attempt to a reference |
|---|
With the "?=" assignment attempt, you attempt to make an assignment to a reference tag.

The following assignment attempts are possible:

- Assignment attempt of a VARIANT to a reference

- Assignment attempt of a DB_ANY to the reference of a technology object

Assignment attempt of a VARIANT to a reference

The
data type of a reference tag is determined at the time of declaration.
However, the data type of a VARIANT tag is determined at runtime. An
implicit data type conversion is not permitted with reference tags.
Therefore, to assign the two data types to each other, use the
assignment attempt. With the assignment attempt, a check is made at
runtime to find out whether the assigned tag is of the correct data
type. If this is the case, the assignment is performed. If the
instruction is executed successfully, there is a valid reference in the
target tag, otherwise a NULL.

After
the assignment attempt, you can check if the attempt was successful
and, depending on the result, continue processing the program. In LAD
and FBD, you can use the enable output ENO for the check. ENO returns
the signal state "1" if the assignment attempt was successful. Only then
are the subsequent instructions executed in the network.

In
STL and SCL you can use the instructions "IS_NULL" or "NOT_NULL", for
example, to check the success of an assignment attempt. See the examples
below.

The
following rules apply to the assignment attempt of VARIANT. VARIANT tags
that do not match these rules return the value "NULL" at runtime.

- The VARIANT must point to an address in an optimized memory area.

- The VARIANT must not point to an address in a temporary memory area.

- If you want to assign a VARIANT to a reference to an ARRAY, the following rules apply:

- The
VARIANT tag must point to an ARRAY whose limits exactly match with
those of the declared reference. A VARIANT tag which points to an ARRAY
[0..9], does not match a tag REF_TO ARRAY[1..10].

- Moreover,
you should compile the blocks that form the value of the VARIANT tag
once in a CPU of the S7-1500 series, firmware version V2.5.

- The assignment attempt of a VARIANT to the reference of a technology object is not possible.

- In SCL, assignment attempts cannot be used in multiple assignments (a := b := c;).

Example

The
following example shows how you can use references to symbolically read
or write the value of a VARIANT tag directly. It is not necessary to
copy the value with the "VariantGet" and "VariantPut" instructions.

The VARIANT tag "variantTelegramData" can transfer data of type "Telegram1" and data of type "Telegram2".

An
assignment attempt is used to test whether the data is of the type
"Telegram1". If this is the case, the values "T" and "W" are assigned to
the parameters "Info1" and "Info2".

Example in SCL:

Example in LAD:

Assignment attempt of a DB_ANY to the reference of a technology object

A
reference to a technology object always points to a specific technology
object, e.g. REF_TO TO_SpeedAxis. If you want to assign a technology
object via a tag of the type DB_ANY during runtime, you need to check
whether the technology object matches the declared reference. To do
this, use the assignment attempt. With the assignment attempt, a check
is made during runtime to find out whether the technology object has the
declared type. If this is the case, the assignment is performed. If
this is executed successfully, there is a valid reference in the target
tag, otherwise a NULL.

The following rules apply to the assignment attempt of a DB_ANY to the reference of a technology object:

- The DB_ANY must point to a technology object in an optimized memory area.

- Two technology objects of the same type can be assigned to each other.

- A derived type can be assigned to its basic type.

- A basic type cannot be assigned to its derived type.

You can find an example of using the assignment attempt for a technology object here:

Example: Editing different axis types iteratively in a program loop

See also

Basic information about references (S7-1500, S7-1200 G2)

Transferring references as block parameters (S7-1500, S7-1200 G2)
| Transferring references as block parameters |
|---|
Description

References can also be transferred as block parameters when calling functions or function blocks.

When
you call a block in whose interface a reference is declared as a formal
parameter, you can transfer a reference in the form of "REF()" or
"#MyRef" as an actual parameter.

Rules

The following rules apply to the transfer of references as block parameters:

- "REF()" can only be transferred as an actual parameter for an input parameter (Input) of a function.

- "REF()" cannot be transferred as an actual parameter to a block parameter of data type "VARIANT".

- The
data type of the transferred tag must correspond exactly to the data
type of the declared reference. No data type conversion is made.

- A reference to a derived technology object can be passed to a reference of the basic type.

- A reference to the basic type cannot be passed to a reference to a derived technology object.

Example 1

The
example below shows the interface of the "Callee" function. The
interface contains several parameters that were declared as reference:

The following figure shows the call of this block in SCL and the parameter assignment for the declared references.

Example 2

The following example shows additional options for transferring references during a block call:

The example shows two possibilities for the transfer:

- Transfer from the FB to the called FC:

The input parameter "refStationData" is declared in the "FC StationData".

"FB LineData" transfers REF("ReceiveData1")
as an actual parameter (line 2 in the program code of the "FB
LineData") during the call. "ReceiveData1" is a data block that is based
on the PLC data type "typeStationData".

- Return from the FC to the calling FB:

References with the same data type are declared in the interface of both blocks (in the example: "refPoductionData").

During the block call, the two references are assigned to each other (line 3 in the program code of the "FB LineData").

The
reference is initialized in the called "FC StationData" (line 2) and is
written to the temporary data of the calling FB via the output
parameter.

The
example shows a section from the programming example "Return data to
the calling block via reference". You can find the detailed program code
under "See also".

See also

Basic information about references (S7-1500, S7-1200 G2) Dereferencing (S7-1500, S7-1200 G2) Example: Return data to the calling block via reference (S7-1500, S7-1200 G2)

Example: Transferring tags of different data types using references (S7-1500, S7-1200 G2)
| Example: Transferring tags of different data types using references |
|---|
Task

In
the following application example, a production plant requests data.
Different data is transferred to the plant depending on the type of data
structure requested.

The
data structures are mapped in two different PLC data types. The PLC
data type "typeTelegram1" contains general information of the data type
"CHAR", the PLC data type "typeTelegram2" contains the part ID of the
data type "STRING". A data block is generated from each of the two PLC
data types:

Example programs

The following figure shows the implementation of the task with and without the use of references in SCL:

Because
both blocks should be able to process different telegram formats, they
have an in-out parameter (InOut) of data type "VARIANT" at which the
telegrams are transferred as structured tags. Since the data type of a
VARIANT parameter is not yet known at the time the program is created,
it is not possible to directly access the parameter. Therefore, in both
examples, "TypeOf" is used to determine which data type is currently
available at the time of the call.

In
the left block, the tag pending during runtime is now copied into a
temporary tag of the corresponding data type using the "VariantGet"
instruction, where it is described with the appropriate values. Then the
structure is copied back to the "telegram" parameter using the
"VariantPut" instruction. Copying has a detrimental effect on the
program runtime and costs memory space.

In
the right block, references are used to solve the task: The interface
contains one reference parameter each for the two possible data
structures. Depending on the currently pending tag, the matching
reference is initialized using "AssignmentAttempt" and now points to the
memory location of the tag in the data block. The values are now
written directly to the data block.

The
program code is clearer and easier to maintain. Because the structured
tags do not have to be copied, the program runtime and memory
requirements are not affected.

Example: Return data to the calling block via reference (S7-1500, S7-1200 G2)
| Example: Return data to the calling block via reference |
|---|
Task

In
the following application example, we are configuring a production
plant that consists of multiple stations. The stations are controlled by
two CPUs which send data to a control CPU. This CPU must analyze for
which station new data exists and execute the higher-level control
tasks, for example, adding up the number of produced pieces.

The following figure shows the structure of the production plant:

Blocks in the example program

The program on the control CPU is structured as follows:

- PLC data type "typeStationData"

The
data of a station is mapped in the PLC data type "typeStationData". The
PLC data type contains two lower-level PLC data types:

- "typeGeneralInfo"

The data type contains the station number.

- "typeProductionData"

The data type contains the number of pieces of the station.

- DB "ReceiveData"

For
communication between the CPUs, a "ReceiveData" data block of the type
"typeStationData" is available for each CPU. The communication data is
written to this block.

- "FB LineData"

The
FB runs a complete analysis of the production line. This includes, for
example, adding up all unit counters of the individual stations. It also
calls the "FC StationData" which, among other things, copies the
received data from the "ReceiveData" DB to the global DB "Station".

- "FC StationData"

The
FC checks from which station new data was received and copies it to the
corresponding ARRAY element in the global DB "Station". The ARRAY
element is then returned as reference to the calling "FB LineData" for
further processing.

- Global DB "Station"

This
DB contains the station information of the five stations. It is stored
in an ARRAY of the type "typeStationData" from five components.

Example program

The following figure shows the implementation of the task in SCL:

The "FB LineData" calls the "FC StationData" and transfers the reference to the receive data block when being called by REF("ReceiveData").

By
dereferencing to the transferred receive data block, the FC reads out
the station number and writes it to the temporary tag "stationNo".

The production data from the receive data block is then copied to the corresponding ARRAY element in the global DB "Station".

This ARRAY element is returned as reference to the calling "FB LineData" via the "refProductionData" output.

It
can subsequently access the transferred ARRAY element directly by
dereferencing and thus update the unit counter for the entire production
line.

See also

Transferring references as block parameters (S7-1500, S7-1200 G2)

Example: Editing different axis types iteratively in a program loop (S7-1500, S7-1200 G2)
| Example: Editing different axis types iteratively in a program loop |
|---|
Example

The
following example shows how you can iteratively edit different axis
types in a FOR loop. In addition to the "SpeedAxis" type, derived axis
types can also be processed in the loop, e.g. the "PositioningAxis" or
"SynchronousAxis" axis types.

- Create
a global data block and declare an ARRAY of the "DB_ANY" data type. Any
technology object can be passed to a DB_ANY in runtime. You can, for
example, initialize the global data block in a startup OB by assigning
specific technology objects to the ARRAY elements.

- In
the SCL block, declare a reference of the "REF_TO TO_SpeedAxis" data
type. Axes of the "SpeedAxis" type as well as derived axes can be passed
to the reference in runtime.

- In
the FOR loop, first there is a check for each technology object from
the "DB_Axis" to determine whether it matches the declared reference. An
assignment attempt is used for this.

If the assignment attempt is successful, the axis parameters are read and written.

See also

Assignment attempt to a reference (S7-1500, S7-1200 G2)


# VARIANT (S7-1200, S7-1500, S7-1200 G2)

Basic information on VARIANT (S7-1200, S7-1500, S7-1200 G2)
| Basic information on VARIANT |
|---|
Description

A
parameter of VARIANT data type is a pointer or a reference It can point
to tags of various data types. The VARIANT pointer cannot point to an
instance and therefore cannot point to a multiple instance or ARRAY of
multiple instances. The VARIANT pointer can be an object of an
elementary data type, such as INT or REAL. It can also be a STRING, DTL,
ARRAY of STRUCT, UDT, or ARRAY of UDT. The VARIANT pointer can
recognize structures and point to individual structure components. An
operand of data type VARIANT occupies no space in the instance data
block or work memory. However, it will occupy memory space on the CPU.

A
tag of the VARIANT type is not an object but rather a reference to
another object. Individual elements of the VARIANT type can only be
declared on formal parameters within the block interface of a function
in the VAR_IN, VAR_IN_OUT and VAR_TEMP sections. For this reason, it
cannot be declared in a data block or in the static section of the block
interface of a function block, for example, because its size is
unknown. The size of the referenced objects can change.

Using
the VARIANT data type, you can in particular create generic,
standardized function blocks (FB) or functions (FC) for various data
types. Various instructions in all programming languages are available
to you for this purpose. During the creation of the program, you can
specify which data types the block should be able to process. The
VARIANT data type supports you here by allowing the interconnection of
any tags. You can then react accordingly to their data types in the
block. When a block is called, you can connect the parameters of the
block to tags of any data type. When a block is called, the type
information of the tag is transferred in addition to a pointer to the
tag. The code of the block can then be executed according to its type in
line with the tag transferred during runtime.

If,
for example, a block parameter of a function has the VARIANT data type,
then a tag of the integer data type can be transferred at one point in
the program, and a tag of the PLC data type can be transferred at
another point in the program. With the help of the VARIANT instructions,
the function is then in a position to react to the situation without
errors.

| Note You can only point to a complete data block if it was originally derived from a user-defined data type (UDT). |
|---|

| Note Address I/O Direct reading or writing of a signal from an I/O input or output is only possible on a CPU of an S7-1500 module. (: P) |
|---|
The following table shows the properties of the VARIANT pointer:

| Length (bytes) | Representation | Format | Example of value input |
|---|---|---|---|
| 0 | Symbolic | Operand | "TagResult" |
| NameDataBlock.NameOperand.Component | "Data_TIA_Portal".StructVariable.FirstComponent | | |
| Absolute | Operand | %MW10 | |
| DataBlockNumber.Operand Type Length | P#DB10.DBX10.0 INT 12 1) | | |
| NULL pointer | NULL | | |
| 1) If you use the prefix P#, you can only point to memory areas with "standard" access mode. | | | |
Coding of data types

If you use absolute addressing with P#, the following data types are permitted:

- BOOL

- BYTE

- CHAR

- WORD

- INT

- DWORD

- DINT

- REAL

- TIME

- S5TIME

- DATE

- TOD

- DT

Example

The following example shows how VARIANT works using the "MOVE: Move value" instruction of STL:

| STL | Explanation |
|---|---|
| CALL MOVE | // The instruction is called. |
| value_type := VARIANT | // Data type of the parameters IN and OUT |
| IN := "Data_TIA_Portal".StructVariable.FirstComponent | // The contents of the "FirstComponent" operand are moved from the "Data_TIA_Portal" DB. |
| OUT := "MotorDB".StructResult.TagResult | // And transferred to the "TagResult" operand from the "MotorDB" DB. |
See also

Basics of indirect addressing (S7-1200, S7-1500) Overview of the valid data types Basics of constants Basics of block access Principles of block calls VARIANT instructions (S7-1200, S7-1500, S7-1200 G2) Accessing I/O devices Data type conversion for S7-1200 (S7-1200)

Applications for pointers in the comparison (S7-1200, S7-1500, S7-1200 G2)
| Applications for pointers in the comparison |
|---|
Application cases for pointers with an S7-1200/1500 CPU as compared to S7-300/400

The
following table provides you with an overview of the various
applications for pointers on a CPU of the S7-300/400 series (ANY
pointer) and their solution with a CPU of the S7-1200/1500 series.

In
most applications, the use of a pointer is no longer required on a CPU
of the S7-1200/1500 series. Instead, much simpler language resources are
available.

It is
only advisable to use the VARIANT data type for indirect addressing,
when the data types are only determined during the program runtime.

| What is the purpose of the ANY pointer? | Recommendations in the TIA Portal (S7-1200/S7-1500) |
|---|---|
| Moving data of any source and destination data type in the program using the instruction "BLKMOV: Move block". | Definition of tags within a PLC data type. You can use the instructions "Serialize" and "Deserialize" to move the tags. |
| Initializing an ARRAY structure | Using the instruction "FILL_BLK: Fill block", you initialize or fill an ARRAY structure. |
| Moving ARRAY elements | Using the instruction "MOVE_BLK: Move block". you move the content of multiple elements of an ARRAY structure to another ARRAY structure. |
| Memory and performance optimization using structured data | Use the InOut section in the block interface to optimize memory and performance. You can find more information in the "Programming Guideline for S7-1200/1500" under the following link Programming Guideline for S7-1200/1500 |
| Access to individual bits/bytes of a WORD | Use the "slice access" You can find more information here: Example of a slice access |
| Determination of the length of structures or data blocks | Use an ARRAY and read its length using the instruction "CountOfElements: Get number of ARRAY elements". The instruction only works in conjunction with the VARIANT data type or the ResolvedSymbol system data type. |
| Indirect addressing | You can use the VARIANT pointer for the indirect addressing of data types that will only be known during runtime. You can use the data type DB_ANY for indirect access to a data block. |

VARIANT instructions (S7-1200, S7-1500, S7-1200 G2)
| VARIANT instructions |
|---|
VARIANT instructions

The following instructions for working with VARIANT are available to you in the TIA Portal:

| Category | Instruction | Description |
|---|---|---|
| Comparator operations | EQ_Type | Compare data type for EQUAL with the data type of a tag |
| NE_Type | Compare data type for UNEQUAL with the data type of a tag | |
| EQ_ElemType | Compare data type of an ARRAY element for EQUAL with the data type of a tag | |
| NE_ElemType | Compare data type of an ARRAY element for UNEQUAL with the data type of a tag | |
| IS_NULL | Query for EQUALS ZERO pointer | |
| NOT_NULL | Query for UNEQUALS ZERO pointer | |
| IS_ARRAY | Check for ARRAY | |
| TypeOf | Check data type of a VARIANT tag | |
| TypeOfElements | Check element data type of a VARIANT tag | |
| Move operations | MOVE_BLK_VARIANT | Move block |
| VariantGet | Read out VARIANT tag value | |
| VariantPut | Write VARIANT tag value | |
| CountOfElements | Get number of ARRAY elements | |
| Conversion operations | VARIANT_TO_DB_ANY | Convert VARIANT to DB_ANY |
| DB_ANY_TO_VARIANT | Convert DB_ANY to VARIANT | |

| Note Differences between MOVE, MOVE_BLK and MOVE_BLK_VARIANT You can use the "MOVE" instruction to copy complete structures. You can use the "MOVE_BLK" instruction to move parts of ARRAYs with known data type. The MOVE_BLK_VARIANT instruction is only required if you want to move parts of ARRAYs with a data type that is only known during program runtime. |
|---|
You
can find additional information on the individual instructions in the
information system under "Basic instructions > Respective programming
language".

You can also find additional instructions which also work with the VARIANT data type under the "Extended instructions".

See also

Basic information on VARIANT (S7-1200, S7-1500, S7-1200 G2) Indirect addressing with the VARIANT data type

Application options for VARIANT instructions (S7-1200, S7-1500, S7-1200 G2)
| Application options for VARIANT instructions |
|---|
Introduction

In the following chapter, you will learn which application options you have with VARIANT instructions.

Evaluating data types of tags to which a VARIANT points

In the table below, you see which instructions are available to you to evaluate data types of tags to which a VARIANT points:

| Function | Instruction | Description |
|---|---|---|
| To determine the data type | TypeOf(): Check data type of a VARIANT tag (This instruction is available only in SCL and only in conjunction with an IF or CASE instruction.) | You use this instruction to compare the data type to which a VARIANT tag points with the data type of any other tag. You can also make the comparison with a PLC data type. |
| TypeOfElements(): Scan data type of an ARRAY element of a VARIANT tag (This instruction is available only in SCL and only in conjunction with an IF or CASE instruction.) | You use this instruction to compare the data type to which a VARIANT tag points with the data type of any other tag. You can also make the comparison with a PLC data type. If the data type of the VARIANT tag is an ARRAY, the data type of the ARRAY elements is compared. | |
| EQ_Type: Compare data type for EQUAL with the data type of a tag NE_Type: Compare data type for UNEQUAL with the data type of a tag | You use this instruction to compare the data type to which a VARIANT tag points with the data type of any other tag. You can also make the comparison with a PLC data type. | |
| EQ_ElemType: Compare data type of an ARRAY element for EQUAL with the data type of a tag NE_ElemType: Compare data type of an ARRAY element for UNEQUAL with the data type of a tag | You use this instruction to compare the data type to which a VARIANT tag points with the data type of any other tag. You can also make the comparison with a PLC data type. If the data type of the VARIANT tag is an ARRAY, the data type of the ARRAY elements is compared. | |
| To evaluate ARRAY elements | IS_ARRAY: Check for ARRAY | You use this instruction to check whether the data type to which a VARIANT tag points is an ARRAY. |
| CountOfElements: Get number of ARRAY elements | You use this instruction to read out how many ARRAY elements the tag has to which the VARIANT tag points. | |
You
can find additional information on the individual instructions in the
information system under "Basic instructions > Respective programming
language".

Reading data to which a VARIANT points

To be able to use the data you must move this data to a tag as an intermediate step, as it cannot be processed directly.

| VARIANT points to | Destination data type |
|---|---|
| VariantGet: Read out VARIANT tag value | You use this instruction to move the value of a single tag to another tag. The data types of both tags must match. |
| REAL | REAL |
| DINT | DWORD |
Assigning data to a VARIANT tag

You
cannot use the instruction to initialize VARIANT tags. The VARIANT tags
must therefore already be initialized when the data is returned to the
tag. Do not use uninitialized temporary VARIANT tags.

| Source data type | VARIANT points to: |
|---|---|
| VariantPut: Write VARIANT tag value | You use this instruction to move the value of a single tag to another tag. The data types of both tags must match. |
| REAL | REAL |
| DINT | DWORD |
Processing dynamic ARRAY structures

| To evaluate ARRAY elements | TypeOfElements(): Scan data type of an ARRAY element of a VARIANT tag (This instruction is available only in SCL and only in conjunction with an IF or CASE instruction.) | You use this instruction to compare the data type to which a VARIANT tag points with the data type of any other tag. You can also make the comparison with a PLC data type. If the data type of the VARIANT tag is an ARRAY, the data type of the ARRAY elements is compared. |
|---|---|---|
| IS_ARRAY: Check for ARRAY | You use this instruction to check whether the data type to which a VARIANT tag points is an ARRAY. | |
| CountOfElements: Get number of ARRAY elements | You use this instruction to read out how many ARRAY elements the tag has to which the VARIANT tag points. | |
| MOVE_BLK_VARIANT: Move block | This instruction is used to move dynamic and type-safe (integrated type test) ARRAYs. You can freely select the limit values for the source and destination ARRAYs. The data types of ARRAY elements must match. | |

| Note Differences between MOVE, MOVE_BLK and MOVE_BLK_VARIANT You can use the "MOVE" instruction to copy complete structures. You can use the "MOVE_BLK" instruction to move parts of ARRAYs with known data type. The MOVE_BLK_VARIANT instruction is only required if you want to move parts of ARRAYs with a data type that is only known during program runtime. |
|---|
Additional information on the use of the MOVE_BLK_VARIANT instruction can be found in the "Moving data" programming example.

See also

Basic information on VARIANT (S7-1200, S7-1500, S7-1200 G2) Example of moving data (S7-1200, S7-1500, S7-1200 G2)

Initializing VARIANT (S7-1200, S7-1500, S7-1200 G2)
| Initializing VARIANT |
|---|
Description

Initialize
the VARIANT data type by assigning a specific tag to the VARIANT block
parameter at the block call. This forms a reference to the address of
the passed tag. To do this, create a block parameter of the VARIANT data
type in the block interface. In the following example, these are the
two block parameters SourceArray and DestinationArray in the section
InOut.

The
example shows a section from the programming example "Example of moving
data". You can find the detailed program code under "See also".

| Note Direct passing of a tag to a VARIANT tag is not possible, such as myVARIANT := #Variable |
|---|
See also

Example of moving data (S7-1200, S7-1500, S7-1200 G2)

Transferring and reading out various data types with VARIANT (S7-1200, S7-1500, S7-1200 G2)
| Transferring and reading out various data types with VARIANT |
|---|
The
example shows a section from the programming example "Example of moving
data". You can find the detailed program code under "See also".

| Note VARIANT as formal parameter If the VARIANT is declared as a formal parameter, no write-protected data may be transferred as actual parameters. |
|---|
Passing various data types

In
the following example, you see how the VARIANT block parameter can be
initialized with different tags when a generic, standardized function is
called multiple times:

The
"FC_PartialArrayCopy" function is called twice. The VARIANT parameter
SourceArray is interconnected with an ARRAY of "my_struct" with the left
call. The VARIANT parameter SourceArray is interconnected with an ARRAY
of REAL with the right call.

Reading out and checking data types

Various
comparison instructions are available to you to read out the data type
of a tag or an element and compare it with data types of other tags or
elements.

In the
figure below, you see the usage of multiple comparison instructions to
check whether the elements of the ARRAYs have the same data type:

The MOVE_BLK_VARIANT instruction is only executed if the data types of the ARRAY elements are the same.

See also

Example of moving data (S7-1200, S7-1500, S7-1200 G2)

Examples of using the VARIANT data type (S7-1200, S7-1500, S7-1200 G2) Example of moving data (S7-1200, S7-1500, S7-1200 G2)
| Example of moving data |
|---|
Programming example

In
this programming example, data values, which are collected for example
during a production shift, are moved for further processing. The data is
collected in an ARRAY. Using the "MOVE_BLK_VARIANT instruction: Move
block", you can move either the entire ARRAY or only individual ARRAY
elements dynamically and type-safe. You can freely select the ARRAY
limits for the respective source and destination ARRAYs and these do not
have to match. However, the data type of the data values that are to be
moved must match. This instruction is available in all programming
languages.

By
using the VARIANT data type, you can use the created program code to
move data for other production shifts as well, by specifying a different
source and destination area at the block call.​

Procedure

- Create a function using the SCL programming language and give it the name "FC_PartialArrayCopy".

- Declare the block interface as follows:

- Create the SCL program code as follows:

You can find the program code below as template.

- Create the PLC data type "UDT_MyStruct":

- Create the global data block "DB_WithArrays":

- Call
the "FC_PartialArrayCopy" function in an organization block, for
example OB1, and initialize the parameters with the DB_WithArrays data
block. Enter the named constants:

- Instead
of using the first two ARRAYs, which have the data type UDT_MyStruct,
you can also use the third and fourth ARRAY, which have the data type
REAL:

Result

As
soon as the "FC_PartialArrayCopy" block is called in the program cycle,
two data values, starting with the fourth element, are copied from the
first ARRAY of the "DB_WithArrays" global data block to the second ARRAY
of the data block. The copied data values are inserted in the second
ARRAY, starting from the fourth element.

SCL program code for copying:

| SCL |
|---|
| IF IS_ARRAY(#SourceArray) AND TypeOfElements(#SourceArray) = TypeOfElements(#DestinationArray) THEN |
| #Error := MOVE_BLK_VARIANT(COUNT := #Count, SRC := #SourceArray, SRC_INDEX := #SourceIndex, |
| DEST => #DestinationArray, DEST_INDEX := #DestinationIndex); |
| END_IF; |
| #FC_PartialArrayCopy := #Error; |
See also

Basic information on VARIANT (S7-1200, S7-1500, S7-1200 G2)

Example of programming a queue (FIFO) (S7-1200, S7-1500, S7-1200 G2)
| Example of programming a queue (FIFO) |
|---|
Programming example

In
the following example, you program a ring buffer which consists of an
ARRAY and is written and read according to the FIFO principle. The
program code has a read-VARIANT pointer and a write-VARIANT pointer.
Using the VARIANT instructions, you can program the program code
robustly and ensure reliable copying or deleting.

Using
the VARIANT data type, program sections can be influenced during
runtime. The VARIANT pointer is a type-safe pointer, i.e. a type test is
performed during runtime. For blocks that have been created with the
block property "optimized", sub-functions that were previously
programmed with an ANY pointer can now be resolved with a VARIANT
pointer. The VARIANT data type is used to transfer structures to system
function blocks.

Procedure

- Create an SCL function block and name it "FIFOQueue".

- Declare the block interface as follows:

| Declaration | Parameters | Data type | Comment |
|---|---|---|---|
| Input | request | BOOL | The instruction is executed when a positive signal edge is detected at the "request" parameter. |
| mode | BOOL | 0 = The first entry in the ring buffer is returned. 1 = An entry is written at the last position in the ring buffer. | |
| initialValue | VARIANT | Value with which the ARRAY of the ring buffer is initialized. | |
| Output | error | INT | Error information |
| InOut | item | VARIANT | The entry that is either returned from the ring buffer or written to the ring buffer. |
| buffer | VARIANT | An ARRAY that is used as a ring buffer. | |
| Static | edgeupm | BOOL | Edge memory bit in which the RLO of the previous query is saved. |
| firstItemIndex | INT | Index of the oldest entry in the ring buffer | |
| nextEmptyItemIndex | INT | Index of the next free entry in the ring buffer | |
| Temp | edgeup | BOOL | Result of edge evaluation |
| internalError | INT | Error information | |
| newFirstItemIndex | INT | Variable index | |
| newNextEmptyItemIndex | INT | Variable index | |
| bufferSize | UDINT | Number of ARRAY elements in the ring buffer | |

- Create the following program code in the "FIFOQueue" function block:

| |
|---|
| (* This program code section is only executed once after a positive signal edge. If there is no change in the signal state of the result of logic operation, the program processing of the "FIFOQueue" FB is terminated. *) |
| #edgeup := #request & NOT #edgeupm; |
| #edgeupm := #request; |
| IF NOT (#edgeup) THEN |
| RETURN; |
| END_IF; |
| |
| |
| // ------Validation of whether all parameter inputs are valid.---- |
| (* This program code section checks whether the ring buffer is an ARRAY. If so, the number of the ARRAY elements is read out. If it is not an ARRAY, the program execution is terminated at this point and the error code "-10" is output. *) |
| IF NOT (IS_ARRAY(#buffer)) THEN |
| #error := -10; |
| RETURN; |
| ELSE |
| #bufferSize := CountofElements(#buffer); |
| END_IF; |
| |
| (* This program code section checks whether the data type of the ARRAY elements matches the data type of the entry (tag #item). If the data types do not match, the program execution is terminated at this point and the error code "-11" is output. *) |
| IF NOT (TypeOf(#item) = TypeOfElements(#buffer)) THEN |
| #error := -11; |
| RETURN; |
| END_IF; |
| |
| (* This program code section checks whether the initial value of the ring buffer matches the entry (tag #item). If the data types do not match, the program execution is terminated at this point and the error code "-12" is output. *) |
| IF NOT (TypeOf(#item) = TypeOf(#initialValue)) THEN |
| #error := -12; |
| RETURN; |
| END_IF; |
| |
| (* This program code section checks whether the variable indices are within the ARRAY limits. If this is not the case, the program execution is terminated at this point and either error code "-20" or "-21" is output depending on the index. *) |
| IF (#nextEmptyItemIndex >= #bufferSize) THEN |
| #error := -20; |
| RETURN; |
| END_IF; |
| IF (#firstItemIndex >= #bufferSize) THEN |
| #error := -21; |
| RETURN; |
| END_IF; |
| |
| |
| //-----------Program code execution, depending on the Mode parameter------------- |
| // The execution of the instructions depends on the signal state of the Mode parameter. |
| IF #mode = 0 THEN |
| |
| // If the Mode parameter has the signal state "0", the first entry from the passed ring buffer is returned. |
| (* This program code section checks whether the ring buffer is empty. If this is the case, program execution is terminated at this point and the error code "-40" is output. *) |
| IF (#firstItemIndex = -1) THEN |
| #error := -40; |
| RETURN; |
| END_IF; |
| |
| // This program code section returns the first entry of the ring buffer. |
| #internalError := MOVE_BLK_VARIANT(SRC := #buffer, |
| COUNT := 1, |
| SRC_INDEX := #firstItemIndex, |
| DEST_INDEX := 0, |
| DEST => #item); |
| |
| IF (#internalError = 0) THEN |
| (* This program code section checks whether the ring buffer contains ARRAY elements. If it does, the first entry is passed on and the index is incremented by 1. *) |
| #internalError := MOVE_BLK_VARIANT(SRC := #initialValue, |
| COUNT := 1, |
| SRC_INDEX := 0, |
| DEST_INDEX := #firstItemIndex, |
| DEST => #buffer); |
| |
| // This program code section calculates the new index of the first entry. |
| #newFirstItemIndex := #firstItemIndex +1; |
| #newFirstItemIndex := #newFirstItemIndex MOD UDINT_TO_INT(#bufferSize); |
| |
| // This program section checks whether the ring buffer is empty. |
| IF (#nextEmptyItemIndex = #newFirstItemIndex) THEN |
| // If the ring buffer is empty, the index is set to 0. |
| #firstItemIndex := -1; |
| #nextEmptyItemIndex := 0; |
| ELSE |
| // The index of the first entry is changed. |
| #firstItemIndex := #newFirstItemIndex; |
| END_IF; |
| END_IF; |
| ELSE |
| |
| |
| // If the Mode parameter has the signal state "1", the entry is written to the passed ring buffer. |
| (* This program code section checks whether the ring buffer is full. If this is the case, program execution is terminated at this point and the error code "-50" is output. *) |
| IF (#nextEmptyItemIndex = #firstItemIndex) THEN |
| #error := -50; |
| RETURN; |
| END_IF; |
| |
| // This program code section writes the entry to the ring buffer. |
| #internalError := MOVE_BLK_VARIANT(SRC := #item, |
| COUNT := 1, |
| SRC_INDEX := 0, |
| DEST_INDEX := #nextEmptyItemIndex, |
| DEST => #buffer); |
| |
| IF (#internalError = 0) THEN |
| // This program code section increments the index by 1 and calculates the new empty entry index. |
| #newNextEmptyItemIndex := #nextEmptyItemIndex +1; |
| #newNextEmptyItemIndex := #newNextEmptyItemIndex MOD #bufferSize; |
| #nextEmptyItemIndex := #newNextEmptyItemIndex; |
| |
| (* This program code section checks which index the "#firstItemIndex" tag has. If the number = -1, the ring buffer is initialized and the entry is written to the ring buffer. This is why the tag value "0" must be assigned. *) |
| IF (#firstItemIndex = -1) THEN |
| #firstItemIndex := 0; |
| END_IF; |
| END_IF; |
| END_IF; |
| |
| //-------------------------Local error handling---------------------------- |
| (* This program code section checks whether a local error has occurred. If this is the case, program execution is terminated at this point and the error code "-100" is output. *) |
| IF (#internalError > 0) THEN |
| #error := -100; |
| RETURN; |
| END_IF; |
| |
| // If no error occurred during program execution, the error code "0" is output. |
| #error := 0; |
Result

Call the SCL function block at the position in your program at which the FIFO queue is to run.
