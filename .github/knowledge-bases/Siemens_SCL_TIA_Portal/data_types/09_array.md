# 09 Array

# Basic information on ARRAY

| Basic information on ARRAY |
|---|
Description

A
tag of the ARRAY data type represents a data structure that consists of
a fixed number of components of the same data type. All data types
except ARRAY are permitted for the components.

When
you create an ARRAY tag the index limits are defined in square brackets
and the data type is defined after the keyword "of". The ARRAY limits
can be either defined fixed using integers or global and local constants
or as formal parameters of a block, or defined variably using ARRAY[*].
The low limit must be smaller than or equal to the high limit. An ARRAY
may contain up to six dimensions, the limits of which can be specified
separated by a comma.

The structure of a one-dimensional tag of the ARRAY data type has, for example, the following form:

The maximum ARRAY limits depend on the following factors:

- Data type of the ARRAY component

- Memory reserve (only in blocks with optimized access)

You can find additional information under: Basic information on loading block extensions without reinitialization.

- Maximum size of the data block

- Maximum memory capacity of the CPU (you can find more information in the manual for the device)

The following table shows the properties of the ARRAY data type:

| Block property | Format | ARRAY limits | Data type |
|---|---|---|---|
| Standard | ARRAY[low limit..high limit] of | [-32 768..32 767] of | All data types except ARRAY Multi-instances |
| Optimized | [-2 147 483 648..2 147 483 647] of | | |
Various options are available for defining the ARRAY limits depending on the ARRAY that you declared.

| ARRAY limits | Global data block / tag table | Block interface |
|---|---|---|
| Using integers as fixed ARRAY limits | x | x |
| Using global constants as fixed ARRAY limits | x | x |
| Using local constants as fixed ARRAY limits | - | x |
| Using variable ARRAY limits ARRAY[*] | - | x |
| ARRAY of multi-instances | - | x |
For more information on the section of the block interface in which you can define an ARRAY or an ARRAY[*], refer to: Valid data types in the block interface

| Note Applies to CPUs of the S7-1500 series For a block with the "Optimized block access" block property, an element of the BOOL data type requires 1 byte of memory. This is also true when you use an ARRAY of . An ARRAY[0..1] of BOOL, for example, thus requires 2 bytes in an optimized program block. |
|---|
Using integers as fixed ARRAY limits

You can use integers as fixed ARRAY limits:

- Example of a one-dimensional ARRAY

- Example of a three-dimensional ARRAY:

Using constants as fixed ARRAY limits

You can use local or global constants as fixed ARRAY limits:

- Fixed ARRAY limits for a one-dimensional ARRAY, consisting of two global user constants

- Fixed ARRAY limits for a one-dimensional ARRAY, consisting of two global user constants

- Fixed ARRAY limits for a two-dimensional ARRAY, consisting of global and local user constants

For more information on creating and using constants as ARRAY limits, refer to:

- Declaring local tags and constants in the block interface

- Examples of using constants

Using integers and global and local constants as fixed ARRAY limits

You
can also combine all three above-named options with each other and also
used integers and global and local constants mixed within an ARRAY as
ARRAY limits.

Using variable ARRAY limits ARRAY[*] (only in blocks with optimized access)

You
can use an ARRAY[*] to program blocks that can process an ARRAY with
flexible length. To do this, you declare variable ARRAY limits for the
parameters of a function or function block. ARRAY[*] is available in all
programming languages.

Using
the "LOWER_BOUND" and "UPPER_BOUND" instructions, you can read the low
and high limits of an ARRAY with variable limits during runtime.

| Note Availability of ARRAY[*] ARRAY[*] is available in optimized blocks for a CPU of the S7-1200 series as of firmware version >= 4.2, and for a CPU of the S7-1500 series as of firmware version >= 2.0. In functions (FC) you can use ARRAY[*] in all declaration subsections. In function blocks (FB) you can declare ARRAY[*] only as an in-out parameter in the "InOut" section. |
|---|
- Variable ARRAY limits for a one-dimensional ARRAY:

- Variable ARRAY limits for a one-dimensional ARRAY:

You can find additional information on the use of ARRAY[*] here:

- Transferring tags of the ARRAY / ARRAY[*] data type

- Declaring tags of the ARRAY data type in the block interface

Using multiple instances (only in blocks with optimized access)

You
can also create multi-instances as ARRAY, in order to be able, for
example, to use a variable index to address the individual
multi-instances during the processing of program loops:

For more information on creating and using multi-instances, refer to:

- Multi-instances

- Declaring multi-instances

See also

Overview of the valid data types Padding bytes when using structured data types Indirect addressing of ARRAY components (S7-1200, S7-1500)


# Structure of an ARRAY tag

| Structure of an ARRAY tag |
|---|
Introduction

With
non-optimized blocks, an ARRAY tag never starts at a word limit, i.e.
at a byte with even address. ARRAY tags occupy the memory up to the next
word limit.

In
optimized block the ARRAY requires as much space as the widest element
of the structure. This means, for example, that an ARRAY of BYTE is
located at a Byte limit and an ARRAY of LREAL is located at an 8-byte
limit.

Structure of an ARRAY tag in the one-dimensional array:

Components
with BOOL data type start in the least significant bit. Components with
BYTE and CHAR data type start in the right byte. The individual
components are listed in order.

Structure of an ARRAY tag in the multidimensional array:

In
multidimensional arrays, the components are stored line-by-line
(dimension-by-dimension), starting with the first dimension. In bit and
byte components a new dimension always starts at the next byte. In
components of other data types a new dimension always starts in the next
word (in the next even byte) in non-optimized blocks.

In optimized blocks each dimension requires as much space as the first dimension.


# Addressing ARRAY components

| Addressing ARRAY components |
|---|
Introduction

ARRAY
components are addressed using fixed of variable index. The components
of an ARRAY tag can be treated like tags of the same data type.

The
index of the component is specified in square brackets. The index
includes an integer value (fixed index) or a tag (variable index) for
each ARRAY dimension.

Addressing of ARRAY components using fixed index

The addressing of an ARRAY component using fixed index has the following form:

Addressing ARRAY components using variable index

An
ARRAY component can also be addressed with a tag the value of which is
only calculated during runtime. The tag can be an absolute or symbolic
addressed global or local tag of integer data type. This addressing is
also possible with multidimensional ARRAYs and with the addressing of
sub-arrays. (<ArrayName>[i,j,k...])

A
change of the tags in the called block has no effect on an ARRAY
component that is created as actual parameter at an in/out parameter and
addressed using a variable index. The value is written back to the same
ARRAY component, transferred during the call, from which it was read.

The addressing of an ARRAY component using an index tag has the following form:

For more information on the indirect addressing of ARRAY components, refer to:

- Indirect indexing of ARRAY components

- Programming recommendations:Indirect addressing of ARRAY components

Error handling for ARRAY access

Access
errors result when you access an element during runtime which is
located outside the declared ARRAY limits. The various CPU families
react differently to violations of the ARRAY limits:

- S7-300/400

- The CPU changes to "STOP" mode.

- You can program the program execution error OB (OB 85) to prevent this.

- In
SCL, you also have the option of enabling the attribute "Check ARRAY
limits" in the block properties. This causes the enable output ENO to be
set to FALSE in the case of ARRAY access errors.

- S7-1200

- The CPU generates a diagnostic buffer entry and remains in "RUN" mode.

- S7-1500

- The CPU changes to "STOP" mode.

- You can program the programming error OB (OB 121) to prevent this.

- You
also have the option of programming the local error handling with the
instructions "GET_ERROR: Get error locally" or "GET_ERROR_ID: Get error
ID locally".

| Note Monitoring ARRAY access errors with ENO The enable output ENO is not set to the signal state FALSE if the ARRAY limits are violated during execution of an instruction. The only exception is SCL blocks on CPUs of the S7-300/400 series for which the block property "Check ARRAY limits" is set. |
|---|


# Transferring tags of the ARRAY / ARRAY[*] data type

| Transferring tags of the ARRAY / ARRAY[*] data type |
|---|
Transferring tags of the ARRAY data type

You
can also transfer individual elements of an ARRAY as actual parameter
if the element corresponds to the data type of the formal parameter.

You
can transfer tags of the ARRAY data type as parameters. If a block has
an input parameter of ARRAY data type, you must pass an ARRAY with
identical structure as the actual parameter. This means that the data
type, the number of dimensions and the number of field components must
be identical.

ARRAYs
can be assigned to one another if they have an identical structure.
This means that the data type, the number of dimensions and the number
of array components must be identical. The names of the ARRAYs do not
have to match.

Transferring tags of the ARRAY data type[*]

You
can use ARRAY[*] to declare ARRAYs with variable limits at the
parameters of a function or function block. When you create the block
you can define the limits of the ARRAY that will be transferred later
during runtime after the call during runtime.

The
following figure shows two calls of a block with an input parameter of
the ARRAY[*] data type. ARRAYs of different length are transferred with
each call.

Applicable rules when transferring ARRAYs with flexible limits

Create the function "BlockWithArrayStarIn_FC" for the example so that it can be called later:

The
assignment of ARRAY[*] to ARRAY[*] is permitted if the number of
dimensions and the data type match. However, you cannot transfer
individual ARRAY components in this process:

- Declare the function block "BlockCaller_FB" and call the function "BlockWithArrayStarIn_FC":

The
assignment of an ARRAY with known limits to an ARRAY[*] is permitted if
the number of dimensions and the data type match. Here, you can also
assign individual ARRAY components.

- Declare the function block "BlockCallerFixLimits_FB" and call the function "BlockWithArrayStarIn_FC" twice:

The assignment of ARRAY[*] to VARIANT is permitted. Here, you can also assign individual ARRAY components.

- Create the function "BlockWithVariantIn_FC" so that it can be called:

- Declare the function "BlockWithArrayStarInVariant_FC" and call the function "BlockWithVariantIn_FC":​

The assignment of ARRAY[*] to ARRAYs with fixed limits is not permitted.

| Note Block parameters of the ARRAY[*] type must be supplied with an actual parameter. |
|---|
See also

Rules for supplying block parameters


# Examples of how to use ARRAYs

Example of a multi-dimensional ARRAY
| Example of a multi-dimensional ARRAY |
|---|
Description

Tags
of the ARRAY data type can contain up to 6 dimensions. The same rules
apply as for one-dimensional ARRAYs. The dimension areas are written in
the declaration in square brackets, each separated by a comma. In
multidimensional arrays, the components are stored starting with the
first dimension.

The following table shows the declaration of a two-dimensional tag of the ARRAY data type:

| Name | Data type | Value | Comment |
|---|---|---|---|
| Betr_Temp | ARRAY[1..2, 1..3] of INT | 1,1,4(0) | Two- dimensional tag of the ARRAY data type with 6 components The first two components are assigned the value "1". The remaining four components are assigned the value "0". |
The following figure shows the structure of the declared tag of the ARRAY data type:

Access to the components

The
values of the individual components are accessed via an index. You can
use a constant or a tag for the index. The index of the first component
is, for example, [1,1] and the index of the fourth array component is
[2,1]. For example, you need to declare "Station[2,1]" in the program to
enable access to the value of the fourth component.

Example for calculating the scalar product of two vectors with ARRAY[*]
| Example for calculating the scalar product of two vectors with ARRAY[*] |
|---|
Description

The scalar product is a mathematical link that assigns a number to two vectors (scalar).

The scalar product of two vectors results in a scalar variable and is defined by:

Here ∝ is the angle between the two vectors and .

An example for calculating the scalar product is:

In this case, the result is the number 22.

In
the following programming example, you see how you can calculate the
scalar product of two vectors with flexible ARRAY bounds using ARRAY[*].
Here, the function "ScalarProduct_FC" serves as a template for
calculating the individual scalar products.

You need the following objects for the programming example:

- Two data blocks and a PLC data type (UDT) for managing the vector data.

- Function that contains the program code for calculating the scalar product.

- The two instructions "LOWER_BOUND" and "UPPER_BOUND" to read out the ARRAY bounds.

- Organization block for calculating the scalar products

Procedure

In
this example vectors, that is to say ARRAYs with 1 dimension, are used.
Other calculations, such as matrix multiplications, can of course work
with multi-dimensional ARRAYs.

To calculate the scalar products, follow these steps:

- Create the PLC data type (UDT) "VectorArrays_UDT":

The
two ARRAYs "VectorD5Coordinates" and "VectorE13Coordinates" provide a
data basis with which you can then calculate scalar products.

- Create the "VectorArrays1_DB" data block on the basis of the "VectorArrays_UDT" PLC data type:

- Create
the second "VectorArrays2_DB" data block. Besides the vectors from the
"VectorArrays_UDT" PLC data type, it also contains two other vectors:

You have now created the data basis for calculating the scalar products.

- Create the "ScalarProduct_FC" function as a template for creating the calculation procedure for calculating the scalar product:

The block interface:

Program code:

The
upper and lower ARRAY bounds of vector 1 and vector 2 are queried in
rows 1–4. It is then known how many coordinates the two ARRAYs of the
vectors have. As the scalar product cannot be established until the
number of coordinates of the two vectors that you wish to multiply is
equal, rows 6 to 9 are required

If
the two lower or upper bounds of the ARRAYs are not the same, the
"ScalarProduct_FC" function produces the function value "-1" and the
program block is exited (RETURN).

If
the two lower or upper bounds of the ARRAY are the same, the #Sum tag
in initialized (row 10) with the value "0" and the calculation of the
scalar product is executed (rows 11 - 13).

- Create
the "Main_OB" organization block with the event class "Program cycle".
The "ScalarProduct_FC" function created in step 4 now serves as a
template for calculating scalar products in "Main_OB":

The block interface:

Program code:

Result

The results of the individual scalar product calculations are written in the tags #Result1 -5.

Pointer
