# 08 Struct

# Basic information on STRUCT

| Basic information on STRUCT |
|---|
Description

The
STRUCT data type represents a data structure that consists of a fixed
number of components of different data types. Structures can also be
nested and contain components of data type STRUCT or ARRAY. Structures
can be used to group data according to the process control system and to
transfer parameters as one data unit.

Structure
declarations that are used directly at the tag are called anonymous
structures. An anonymous structure can have the following form:

All of the subsequent explanations refer to this structure image.

Nesting depth and potential number of structures

Structures
(STRUCT) can be nested to a depth of 8 hierarchy levels. For S7-1500
series CPUs starting with firmware V4.0 and S7-1200 G2 series CPUs
starting from firmware V4.1, a nesting depth of 26 hierarchical levels
is possible. An ARRAY of STRUCT/UDT requires 3 hierarchical levels each.
When you use these data types, the maximum nesting depth is reduced
accordingly.

Call hierarchy

A
maximum of 252 structures (STRUCT) are permitted in one data block in
CPUs of the S7-1200/S7-1500 series. If you require other structures, use
PLC data types (UDT) instead of the "STRUCT" data type.

Using PLC data types (UDT)

Transferring a STRUCT for parameter supply

You can transfer the STRUCT data type as a parameter. You can find additional information on parameter supply with STRUCT here:

Transferring tags of the STRUCT data type

Disadvantages of anonymous structures

The
components of the structured tag can be identically addressed. This is
regardless of whether the declaration has been made using a PLC data
type or an anonymous structure.

The following disadvantages apply when using anonymous structures:

- Increased
maintenance costs: If an anonymous structure was copied multiple times,
then it must also have been changed multiple times during a change.

- Anonymous structures are not compatible with PLC data types (UDT) of the same structure

- Performance, since the matching types of all structural components are checked

- Increased memory requirement: Each anonymous structure is a separate object, whose description is loaded to the AS.

Example

If
you declare the tag of the data type STRUCT in a PLC data type (UDT),
more usage options are available to you (see figure on left). However,
you can also declare the tag directly with the data type STRUCT (see
figure on right).

Declaration of the structured tag "Motor" with or without PLC data type (UDT):

| Structured tag with PLC data type (UDT) | Structured tag without PLC data type (UDT) |
|---|---|
| | |
Processing of complex structures

A
series of instructions (e.g. "Serialize: Serialization", "Deserialize:
Deserialization", "CMP" (comparator) and "MOVE: Move value") can process
very large, complex structured tags. In doing so, the CPU analyzes the
form of the tag structure and executes the corresponding instruction for
each substructure contained in the total structure or for all contained
elementary components.

With
a very complex structure, this structure analysis may lead to an
unexpected increase in the run time of the corresponding instruction. In
addition to the complexity of structured tags specified in the
operation, the total number of anonymous structures declared in the
program also has an effect on the run time. A very large number of
different anonymous structure definitions can also increase the run
time.

Solution:

- Avoid anonymous structures. Use PLC data types instead.

- Avoid
multiple declaration of data structures that are structured very
similarly. Try to assemble these into a structure declaration.

- Avoid
the declaration of numerous individual tags in structures and data
blocks, if they have the same data type. Use the ARRAY data type in this
case, if possible.

See also

Declaring tags of STRUCT data type Overview of the valid data types Padding bytes when using structured data types


# Structure of a STRUCT tag

| Structure of a STRUCT tag |
|---|
Introduction

A
STRUCT tag always starts in a non-optimized block at a word limit, i.e.
at a byte with even address. The individual components are then located
in the order of their declaration in the memory. STRUCT tags occupy the
memory up to the next word limit.

Components
with BOOL data type start in the least significant bit. Components with
BYTE and CHAR data type start in the next byte. Components with
different data type start at a word limit. In optimized blocks the
structures are stored so that all components are aligned according to
their size. The order in the memory does not correspond to the display
in the editor.

A
nested structure is a structure that is a component of another
structure. A nesting depth of maximum 8 structures is possible. A
nesting depth of maximum 9 structures is possible in the "InOut"
section. The nesting depth is calculated including the highest structure
element (example: "Anna.Berta.Carla" corresponds to a nesting depth of
3).

For S7-1500
series CPUs starting with firmware V4.0, a nesting depth of 26
hierarchical levels is possible. An ARRAY of STRUCT/UDT requires 3
hierarchical levels each. When you use these data types, the maximum
nesting depth is reduced accordingly.

Call hierarchy

All components can be separately addressed. The individual names of components are separated by a dot.

Structure of a STRUCT tag with elementary and complex data types in the non-optimized memory area:

- Declaration of the "Motor" STRUCT tag

- Required memory of the "Motor" STRUCT tag


# Addressing STRUCT elements

| Addressing STRUCT elements |
|---|
Addressing elements in structures

You can access individual elements in a structure using the following syntax:

"<Blockname>".Structure.Element

<Namespace>.<Blockname>.Structure.Element

Examples

The following examples show the addressing of structured data type tags:

| Addressing | Explanation |
|---|---|
| "Global_DB".Motor.Valves | Addressing of the "Valves" element in the "Motor" structure of the global data block "Global_DB". Neither the accessing block nor the called block is located in a namespace. |
| myNamespace.Global_DB.Motor.Valves | Addressing of the "Valves" element in the "Motor" structure of the global data block "Global_DB". The "Global_DB" block is in the "myNamespace" namespace. |

| Note Calling and addressing blocks in namespaces Blocks located in namespaces are represented in the program code in IEC-compliant notation: The block name is not in quotation marks. The namespace precedes the block name, separated by a dot. You can find detailed information on the notation of namespaces under: Categorizing program elements in namespaces |
|---|


# Transferring tags of the STRUCT data type

| Transferring tags of the STRUCT data type |
|---|
Description

You
can also transfer individual components of a STRUCT tag as actual
parameters if the components correspond to the data type of the formal
parameter.

You
can also transfer complete structures as parameters. If a block has an
input parameter of the STRUCT data type, you must transfer a STRUCT with
identical structure as the actual parameter. This means that the names
and data types of all structure components have to be identical.

Structures
and user-defined PLC data types can be assigned to one another if they
have identical structures. This means that the data types and the order
of all structure components must be identical. In nested structures, the
data types and the order of the lower-level structures and their
components must also match.

Two
different PLC data types can also be assigned to one another if the
data types and the order of all structure components including the
lower-level structures are identical. The names of the PLC data types do
not have to match.

User-defined PLC data types and structures cannot be assigned to system data types.

| Note We recommend that you program structures as PLC data types (UDT). PLC data types (UDT) make programming easier, since they can be used repeatedly and changed centrally. |
|---|
See also

Rules for supplying block parameters

ARRAY
