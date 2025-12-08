# SCL Instruction Details Reference

Comprehensive RAG-optimized documentation of Siemens SCL instruction details for TIA Portal programming. This reference includes detailed implementation guides with parameters, examples, and metadata.

## Quick Navigation

### Categories

- **Arithmetic** (30 instructions)
- **Bit Operations** (13 instructions)
- **Comparison & Logic** (6 instructions)
- **Counter** (9 instructions)
- **Edge Detection** (5 instructions)
- **General Instructions** (23 instructions)
- **Memory & Data** (33 instructions)
- **Selection & Routing** (1 instructions)
- **String Operations** (14 instructions)
- **Timer & Delay** (31 instructions)

## Instruction Categories

### Arithmetic

- `ABS`
- `ACOS`
- `ASIN`
- `ATAN`
- `CASE`
- `COS`
- `EXP`
- `FIND`
- `GetInstancePath`
- `GetSymbolForReference`
- `LN`
- `MAX`
- `MID`
- `MIN`
- `MUX`
- `RD_LOC_T`
- `RD_SYS_T`
- `READ_BIG`
- `READ_LITTLE`
- `RETURN`
- `ResolveSymbols`
- `SET_TIMEZONE`
- `SIN`
- `SQRT`
- `TAN`
- `T_ADD`
- `T_COMBINE`
- `T_SUB`
- `UNSCALE`
- `WR_SYS_T`

### Bit Operations

- `BCDCPL`
- `DECO`
- `ENCO`
- `ENDIS_PW`
- `GET_ERROR`
- `GET_ERR_ID`
- `IF`
- `LEAD_LAG`
- `ROL`
- `SEG`
- `SHL`
- `SHR`
- `SMC`

### Comparison & Logic

- `CEIL`
- `EXIT`
- `LIMIT`
- `MoveFromResolvedSymbol`
- `MoveToResolvedSymbol`
- `SCALE_X`

### Counter

- `BITSUM`
- `CTU`
- `Deserialize`
- `FOR`
- `GATHER_BLK`
- `GetSymbolPath`
- `RTM`
- `S_CUD`
- `Serialize`

### Edge Detection

- `CTD`
- `MCAT`
- `RE_TRIGR`
- `S_CD`
- `S_CU`

### General Instructions

- `AssignmentAttempt`
- `CONTINUE`
- `FILL`
- `FRAC`
- `GOTO`
- `GetSymbolName`
- `INIT_RD`
- `NORM_X`
- `REF`
- `REPEAT`
- `ROUND`
- `RUNTIME`
- `SHUT_DOWN`
- `SNC_RTCB`
- `SQR`
- `SWAP`
- `TIME_TCK`
- `TRUNC`
- `T_DIFF`
- `UFILL_BLK`
- `UMOVE_BLK`
- `WHILE`
- `WR_LOC_T`

### Memory & Data

- `BLKMOV`
- `Chars_TO_Strg`
- `DB_ANY_TO_Variant`
- `FILL_BLK`
- `GATHER`
- `GetInstanceName`
- `IS_ARRAY`
- `JOIN`
- `LOWER_BOUND`
- `MOVE_BLK`
- `MOVE_BLK_Variant`
- `MoveResolvedSymbolsFromBuffer`
- `MoveResolvedSymbolsToBuffer`
- `POKE`
- `POKE_BLK`
- `POKE_BOOL`
- `ReadFromArrayDB`
- `ReadFromArrayDBL`
- `SCATTER`
- `SCATTER_BLK`
- `SPLIT`
- `Strg_TO_Chars`
- `TypeOf`
- `TypeOfDB`
- `TypeOfElements`
- `UBLKMOV`
- `UPPER_BOUND`
- `VariantGet`
- `Variant_TO_DB_ANY`
- `WRITE_BIG`
- `WRITE_LITTLE`
- `WriteToArrayDB`
- `WriteToArrayDBL`

### Selection & Routing

- `SEL`

### String Operations

- `ATH`
- `CONCAT`
- `CONVERT`
- `DELETE`
- `FLOOR`
- `HTA`
- `INSERT`
- `LEFT`
- `LEN`
- `REPLACE`
- `RIGHT`
- `SCALE`
- `STRG_VAL`
- `S_MOVE`

### Timer & Delay

- `CTUD`
- `CountOfElements`
- `DCAT`
- `DEMUX`
- `DRUM`
- `F_TRIG`
- `GetBlockName`
- `IMC`
- `MAX_LEN`
- `PEEK`
- `PEEK_BOOL`
- `PRESET_TIMER`
- `RESET_TIMER`
- `R_TRIG`
- `STP`
- `S_COMP`
- `S_CONV`
- `S_ODT`
- `S_ODTS`
- `S_OFFDT`
- `S_PEXT`
- `S_PULSE`
- `TOF`
- `TON`
- `TONR`
- `TP`
- `T_COMP`
- `T_CONV`
- `VAL_STRG`
- `VariantPut`
- `WAIT`

---

## Detailed Instruction Reference

### ABS

**Type:** INSTRUCTION
**Category:** Arithmetic
**Difficulty Level:** Beginner
**Tags:** abs, arithmetic, input, value

#### Description

The function calculates the absolute value of the input value and saves the result to the specified operand. It can be applied in scenarios that require the absolute value of a variable.

#### Parameters

**Inputs:**

- **<expression>** (`SINT, INT, DINT, LINT, floating point`): Input value.

#### Example Code

```scl
Result1 := ABS(Value);
```

#### Additional Information

The result has the same data type as the input value.

---

### ACOS

**Type:** INSTRUCTION
**Category:** Arithmetic
**Difficulty Level:** Beginner
**Tags:** acos, arithmetic, value

#### Description

The function calculates the angle value corresponding to a cosine value, which can be applied to determine the angle corresponding to a cosine value that is a floating point number between -1 and +1.

#### Parameters

**Inputs:**

- **<expression>** (`float`): Cosine value.

#### Example Code

```scl
#Result := ACOS(Value);
```

#### Additional Information

The result range is between 0 and +π.

---

### ASIN

**Type:** INSTRUCTION
**Category:** Arithmetic
**Difficulty Level:** Beginner
**Tags:** arithmetic, asin, value

#### Description

This function calculates the angle value corresponding to a sine value, applicable in situations where an angle value is required, especially when the sine value is known and is within the range of -1 to +1.

#### Parameters

**Inputs:**

- **<expression>** (`float`): Sine value.

#### Example Code

```scl
#Result := ASIN(Value);
```

#### Additional Information

The result range is between -π/2 and +π/2.

---

### ATAN

**Type:** INSTRUCTION
**Category:** Arithmetic
**Difficulty Level:** Beginner
**Tags:** arithmetic, atan, value

#### Description

The function calculates the angle corresponding to the tangent value, applicable in scenarios where the inverse tangent value is needed.

#### Parameters

**Inputs:**

- **<expression>** (`float`): Tangent value.

#### Example Code

```scl
#Result := ATAN(Value);
```

#### Additional Information

Result range is between -π/2 and +π/2.

---

### CASE

**Type:** INSTRUCTION
**Category:** Arithmetic
**Difficulty Level:** Beginner
**Tags:** arithmetic, case, instruction, operation, value

#### Description

The function is to create multiple branches and execute one of the sequences of instructions based on the value of an expression. It can be applied in scenarios that require multiple conditional checks and different operations.

#### Example Code

```scl
Provided SCL example code demonstrating how to use the CASE instruction for multi-branch selection.
```

#### Additional Information

The CASE instruction can be nested by replacing a block of instructions with CASE, and ELSE is an optional syntax part.

---

### COS

**Type:** INSTRUCTION
**Category:** Arithmetic
**Difficulty Level:** Beginner
**Tags:** arithmetic, cos, input, value

#### Description

Function to calculate the cosine value of the input, applicable in scenarios needing the cosine of angle values in radians.

#### Parameters

**Inputs:**

- **<expression>** (`float`): Input value (angle value in radians).

#### Example Code

```scl
Result := COS(Value);
```

---

### EXP

**Type:** INSTRUCTION
**Category:** Arithmetic
**Difficulty Level:** Beginner
**Tags:** arithmetic, exp, value

#### Description

The function calculates the exponential value using base e and stores the result in the specified operand. It can be applied in scenarios where exponential values need to be computed.

#### Parameters

**Inputs:**

- **<expression>** (`float`): Input value.

#### Example Code

```scl
#Result1 := EXP(#Value);
```

---

### FIND

**Type:** INSTRUCTION
**Category:** Arithmetic
**Difficulty Level:** Beginner
**Tags:** arithmetic, find, string

#### Description

The function is to find a specific character or substring within a string and return the position of its first occurrence, applicable in scenarios where locating a specific character or substring within a string is needed.

#### Parameters

**Inputs:**

- **IN1** (`STRING`): WSTRING, D, L, or constant, the string to be searched.
- **IN2** (`STRING`): WSTRING, D, L, or constant, the string to search for.

#### Example Code

```scl
#result := FIND(IN1 := #inputSTRING, IN2 := #STRINGsearchedFor);
```

#### Additional Information

The FIND instruction outputs the position of the first occurrence of the specified value when searching; if there are no matches, it outputs 0.

---

### GetInstancePath

**Type:** INSTRUCTION
**Category:** Arithmetic
**Difficulty Level:** Beginner
**Tags:** arithmetic, get, instance, path

#### Description

The function is to query the composite global name of the block instance, applicable in scenarios where the global name of the block instance needs to be retrieved.

#### Parameters

**Inputs:**

- **SIZE** (`DINT`): Limit on the number of characters for the output parameter.

**Outputs:**

- **OUT** (`WSTRING`): D, L, the global name of the read block instance.

#### Example Code

```scl
Provides SCL example code demonstrating how to use the SHL instruction for left shift operations.
```

#### Additional Information

The GetInstancePath instruction may increase code memory space requirements and extend program runtime.

---

### GetSymbolForReference

**Type:** INSTRUCTION
**Category:** Arithmetic
**Difficulty Level:** Advanced
**Tags:** arithmetic, for, get, reference, symbol

#### Description

The function determines the name of an indirectly addressed object, applicable in scenarios where obtaining the symbol name of an object is needed for further processing.

#### Parameters

**Inputs:**

- **execute** (`Bool`): Control parameter: starts the job on the rising edge.
- **objectRef** (`Reference`): Reference to the object whose name is to be determined.
- **size** (`DInt`): Defines the length for name truncation.

**Outputs:**

- **done** (`Bool`): The job has been executed with no errors.
- **busy** (`Bool`): The job is not yet completed.
- **error** (`Bool`): An error occurred during processing.
- **status** (`Int`): The job processing status or error information.
- **reliability** (`Int`): Reserved for future use.

#### Example Code

```scl
Provided SCL example code demonstrating how to use the SHL instruction for left shift operation.
```

#### Additional Information

GetSymbolForReference is an asynchronously executed instruction, and job execution can span multiple calls.

---

### LN

**Type:** INSTRUCTION
**Category:** Arithmetic
**Difficulty Level:** Beginner
**Tags:** arithmetic, input, value

#### Description

This function calculates the natural logarithm of the input value with base e, applicable in scenarios requiring the natural logarithm of a floating point number.

#### Parameters

**Inputs:**

- **<expression>** (`float`): Input value.

#### Example Code

```scl
#Result1 := LN(#Value);
```

#### Additional Information

If the input value is less than zero, an invalid floating point number is returned.

---

### MAX

**Type:** INSTRUCTION
**Category:** Arithmetic
**Difficulty Level:** Beginner
**Tags:** arithmetic, compare, input, max, value

#### Description

The function compares multiple input values and returns the maximum value, applicable in scenarios where the maximum value needs to be derived from several numbers.

#### Parameters

**Inputs:**

- **IN1** (`Integer, Float, TIME, TOD, DATE, DTL`): The first input value.
- **IN2** (`Integer, Float, TIME, TOD, DATE, DTL`): The second input value.
- **INn** (`Integer, Float, TIME, TOD, DATE, DTL`): Other inserted inputs (values to be compared).

#### Example Code

```scl
#Result := MAX(IN1 := #Value1, IN2 := #Value2, IN3 := #Value3);
```

#### Additional Information

The result is the maximum value among all inputs.

#### Related Functions

- `MIN`
- `LIMIT`


---

### MID

**Type:** INSTRUCTION
**Category:** Arithmetic
**Difficulty Level:** Beginner
**Tags:** arithmetic, mid, string

#### Description

The function is to extract characters from the middle of a string, applicable in scenarios where a substring at a specified position in the string is required.

#### Parameters

**Inputs:**

- **IN** (`STRING`): WSTRING, D, L or constant, a string.
- **L** (`BYTE`): INT, SINT, USINT, I, Q, M, D, L or constant, the length of the substring to extract.
- **P** (`BYTE`): INT, SINT, USINT, I, Q, M, D, L or constant, the position of the first character to extract.

#### Example Code

```scl
#result := MID(IN := #inputSTRING, L := #extractNumber, P := #startingPoint);
```

#### Additional Information

The MID instruction returns an empty string if P exceeds the length of the string during extraction.

#### Related Functions

- `CONCAT`
- `LEFT`
- `RIGHT`


---

### MIN

**Type:** INSTRUCTION
**Category:** Arithmetic
**Difficulty Level:** Beginner
**Tags:** arithmetic, compare, input, min, value

#### Description

The function compares multiple input values and returns the minimum value, which can be applied in scenarios that require comparing multiple values to obtain the minimum.

#### Parameters

**Inputs:**

- **IN1** (`integer, float, TIME, TOD, DATE, DTL`): The first input value.
- **IN2** (`integer, float, TIME, TOD, DATE, DTL`): The second input value.
- **INn** (`integer, float, TIME, TOD, DATE, DTL`): Other input values to compare.

#### Example Code

```scl
#Result := MIN(IN1 := #Value1, IN2 := #Value2, IN3 := #Value3);
```

#### Additional Information

The result is the minimum value among all inputs.

#### Related Functions

- `MAX`
- `LIMIT`


---

### MUX

**Type:** INSTRUCTION
**Category:** Arithmetic
**Difficulty Level:** Intermediate
**Tags:** arithmetic, data, input, instruction, mux, parameter, read, selection, value

#### Description

The function is multiplexing, capable of copying the selected input parameter values and issuing them. It is typically applied in scenarios requiring the selection of different input values based on various conditions. For example, when reading data from multiple sensors and selecting corresponding data based on sensor IDs, the MUX instruction can be utilized.

#### Parameters

**Inputs:**

- **K** (`integer`): Specifies the parameter for the content to be transmitted.
- **IN0** (`binary, integer, etc.`): The first input value.
- **IN1** (`binary, integer, etc.`): The second input value.
- **INn** (`binary, integer, etc.`): Optional input values.
- **INELSE** (`binary, integer, etc.`): The value to be copied when K<n.

#### Example Code

```scl
Provides SCL example code demonstrating how to use the MUX instruction for multiplexing operations.
```

#### Additional Information

All variables assigned with parameters must be of the same data type.

---

### RD_LOC_T

**Type:** INSTRUCTION
**Category:** Arithmetic
**Difficulty Level:** Beginner
**Tags:** arithmetic, read

#### Description

The function reads the current local time from the CPU clock and can be applied to scenarios where local time needs to be retrieved while considering daylight saving time and standard time transitions.

#### Parameters

**Outputs:**

- **OUT** (`DTL`): LDT, DTL, local time.

#### Example Code

```scl
RD_LOC_T(#outputLocTIME);
```

#### Additional Information

When outputting the local time, information related to time zones, start times (already set in the CPU clock configuration) for daylight saving time and standard time will be used.

---

### RD_SYS_T

**Type:** INSTRUCTION
**Category:** Arithmetic
**Difficulty Level:** Beginner
**Tags:** arithmetic, read

#### Description

The function reads the current date and time of the CPU clock (module time) and can be applied in scenarios that require obtaining system time.

#### Parameters

**Outputs:**

- **OUT** (`DTL`): Date and time of DT, LDT, and CPU.

#### Example Code

```scl
RD_SYS_T(#outputTIME);
```

#### Additional Information

The obtained value does not include information about the local time zone or daylight saving time.

---

### READ_BIG

**Type:** INSTRUCTION
**Category:** Arithmetic
**Difficulty Level:** Beginner
**Tags:** arithmetic, big, data, read, write

#### Description

This function reads data from storage in big-endian byte order and writes it into a single variable. It can be used in scenarios where byte sequence data needs to be read in big-endian format and converted to a specific data type.

#### Example Code

```scl
#TagResult := READ_BIG(SRC_ARRAY := #SourceField, DEST_VARIABLE => #DINTVariable, POS := #TagPos);
```

#### Additional Information

The SRC_ARRAY parameter must be an ARRAY of BYTE. The DEST_VARIABLE parameter must be a basic data type.

---

### READ_LITTLE

**Type:** INSTRUCTION
**Category:** Arithmetic
**Difficulty Level:** Beginner
**Tags:** arithmetic, data, little, read, write

#### Description

The function reads data in little-endian format and writes it to a single variable. It can be used in scenarios to read byte sequences from storage and convert them into basic data types.

#### Example Code

```scl
#TagResult := READ_LITTLE(SRC_ARRAY := #SourceField, DEST_VARIABLE => #DINTVariable, POS := #TagPos);
```

#### Additional Information

The variant of the SRC_ARRAY parameter must be an ARRAY of BYTE. The variant of the DEST_VARIABLE must be a basic data type.

---

### RETURN

**Type:** INSTRUCTION
**Category:** Arithmetic
**Difficulty Level:** Beginner
**Tags:** arithmetic, return

#### Description

The function is to terminate the program execution within the current processing block and continue execution in the calling block, applicable in situations where it is necessary to exit the current block upon meeting specific conditions.

#### Example Code

```scl
Provided SCL example code demonstrating how to use the RETURN instruction to exit the current block when specific conditions are met.
```

#### Additional Information

If the RETURN instruction appears at the end of the block, it can be skipped.

---

### ResolveSymbols

**Type:** INSTRUCTION
**Category:** Arithmetic
**Difficulty Level:** Beginner
**Tags:** arithmetic, resolve, symbols

#### Description

The function resolves multiple symbol variable names and receives references to the variables after execution, applicable to scenarios where dynamic resolution of variable references is required.

#### Example Code

```scl
ResolveSymbols_DB(execute := #Input_Execute, firstIndex := 0, lastIndex := 9, done => #Output_Done, busy => #Output_Busy, error => _bool_out_, status => _int_out_, nameList := MySrcDB.InOut_Symbols, referenceList := MyTargetDB.InOut_ResolvedSymbols);
```

#### Additional Information

Symbol variable names are transmitted in WSTRING format and must not exceed 254 UTF-16 characters in length. Elements within an array are supported, but a fixed index must be specified to access the elements.

---

### SET_TIMEZONE

**Type:** INSTRUCTION
**Category:** Arithmetic
**Difficulty Level:** Intermediate
**Tags:** arithmetic, conversion, parameter, timezone

#### Description

The function is to set the local time zone and daylight saving time/standard time conversion parameters, which can be applied to set the system time zone or perform time zone conversion in startup organization blocks.

#### Parameters

**Inputs:**

- **REQ** (`BOOL`): Execute function.
- **TimeZone** (`TimeTransformationRule`): Local time zone parameters and daylight saving time/standard time conversion parameters.

**Outputs:**

- **DONE** (`BOOL`): Status parameter.
- **BUSY** (`BOOL`): Status parameter.
- **ERROR** (`BOOL`): Status parameter.
- **STATUS** (`WORD`): Detailed error and status information.

#### Example Code

```scl
#SET_TIMEZONE_Instance(REQ := #execute,TimeZone := #timezone,DONE=>#statDone,BUSY=>#modeBUSY,ERROR=>#modeERROR,STATUS=>#statusTime);
```

#### Additional Information

This instruction needs to be called each time the time zone is changed. For example, it is recommended to call 'SET_TIMEZONE' when starting the OB.

---

### SIN

**Type:** INSTRUCTION
**Category:** Arithmetic
**Difficulty Level:** Beginner
**Tags:** arithmetic, input, sin, value

#### Description

This function calculates the sine of the input value, applicable in scenarios that require the sine of an angle value in radians.

#### Parameters

**Inputs:**

- **<expression>** (`float`): Input value (angle value in radians).

#### Example Code

```scl
#Result := SIN(#Value);
```

---

### SQRT

**Type:** INSTRUCTION
**Category:** Arithmetic
**Difficulty Level:** Beginner
**Tags:** arithmetic, input, sqrt, value

#### Description

This function calculates the square root of the input value and saves the result to the specified operand. It can be applied in scenarios where square root calculations are needed.

#### Parameters

**Inputs:**

- **<expression>** (`float`): Input value.

#### Example Code

```scl
Result1 := SQRT(#Value);
```

#### Additional Information

If the input value is less than zero, return invalid float.

---

### TAN

**Type:** INSTRUCTION
**Category:** Arithmetic
**Difficulty Level:** Beginner
**Tags:** arithmetic, input, tan, value

#### Description

The function calculates the tangent of the input value (input value is in radians) and can be applied in situations requiring the calculation of the tangent of an angle.

#### Parameters

**Inputs:**

- **<expression>** (`float`): Input value (angle value in radians).

#### Example Code

```scl
#Result := TAN(Value);
```

---

### T_ADD

**Type:** INSTRUCTION
**Category:** Arithmetic
**Difficulty Level:** Beginner
**Tags:** add, arithmetic, input, value

#### Description

The function adds two input time values and can be applied in scenarios where time information accumulation is required.

#### Parameters

**Inputs:**

- **IN1** (`TIME`): LTIME, the first number to be added.
- **IN2** (`TIME`): LTIME, the second number to be added.

#### Example Code

```scl
T_ADD(IN1 := #timeValTOD, IN2 := #timeValTIME);
```

#### Additional Information

During the calculation, the output parameter OUT may exceed its maximum value or fall below its minimum value. This error can be detected by evaluating the enable output ENO.

---

### T_COMBINE

**Type:** INSTRUCTION
**Category:** Arithmetic
**Difficulty Level:** Beginner
**Tags:** arithmetic, combine, value

#### Description

The function merges date values and time values to generate a combined date-time value, which can be applied in scenarios requiring the merging of date and time into a single timestamp.

#### Parameters

**Inputs:**

- **IN1** (`DATE`): Input variable for the date.
- **IN2** (`TOD`): Input variable for the time.

#### Example Code

```scl
CONCAT_DATE_TOD(IN1 := #valueDATE, IN2 := #valueTOD);
```

#### Additional Information

When using T_COMBINE in SCL programs, drag the instruction 'T_COMBINE' from the 'Instructions' task card into the SCL programming window, where the internal instructions CONCAT_DATE_TOD or CONCAT_DATE_LTOD will be displayed in the window.

---

### T_SUB

**Type:** INSTRUCTION
**Category:** Arithmetic
**Difficulty Level:** Beginner
**Tags:** arithmetic, input, operation, parameter, sub, value

#### Description

The function performs a subtraction operation on the time values of two input parameters and can be applied in situations requiring time difference calculations.

#### Parameters

**Inputs:**

- **IN1** (`TIME`): LTIME, the minuend.
- **IN2** (`TIME`): LTIME, the subtrahend.

#### Example Code

```scl
T_SUB(IN1 := #value1TOD, IN2 := #value2Time);
```

#### Additional Information

During the calculation, the output parameter OUT may exceed its maximum value or fall below its minimum value. This error can be detected by evaluating the enable output ENO.

---

### UNSCALE

**Type:** INSTRUCTION
**Category:** Arithmetic
**Difficulty Level:** Intermediate
**Tags:** arithmetic, signal, unscale, value

#### Description

The function of unscaling converts floating-point numbers to integers and can be applied to scenarios where analog signals or floating-point values need to be mapped to an integer range.

#### Parameters

**Inputs:**

- **IN** (`REAL`): The input value to be unscaled and converted to an integer.
- **HI_LIM** (`REAL`): Upper limit.
- **LO_LIM** (`REAL`): Lower limit.
- **BIPOLAR** (`BOOL`): Indicates whether the value of parameter IN should be interpreted as bipolar or unipolar.

**Outputs:**

- **OUT** (`INT`): The result of the instruction.

#### Example Code

```scl
UNSCALE(IN := #inputValue, HI_LIM := #maxLim, LO_LIM := #minLim, BIPOLAR := #bipolarIndicator, OUT => #resultValue);
```

#### Additional Information

The values of constants K1 and K2 depend on the signal state of parameter BIPOLAR. If the value of IN exceeds HI_LIM or is less than LO_LIM, an error is output and the result is set to the nearest limit value.

---

### WR_SYS_T

**Type:** INSTRUCTION
**Category:** Arithmetic
**Difficulty Level:** Beginner
**Tags:** arithmetic

#### Description

Function to set the date and time (module time) of the CPU clock, applicable in scenarios where the CPU clock time needs to be changed or set.

#### Parameters

**Inputs:**

- **IN** (`DTL`): Date and time in DT, LDT format.

#### Example Code

```scl
WR_SYS_T(#inputTIME);
```

#### Additional Information

The module time of the CPU clock will be used as a template for all time processing processes initiated by the CPU.

---

### BCDCPL

**Type:** INSTRUCTION
**Category:** Bit Operations
**Difficulty Level:** Beginner
**Tags:** bcdcpl, bit, bit-operations

#### Description

This function calculates the decimal complement of the 7-bit BCD number specified in the operand, applicable in scenarios requiring the complement of BCD encoding.

#### Parameters

**Inputs:**

- **Operand** (`Bit String`): 7-bit BCD number.

#### Example Code

```scl
Provided SCL example code demonstrating how to use the SHL instruction for left shift operations.
```

#### Additional Information

Calculate using the mathematical formula 10000000 (BCD encoded) - 7-bit BCD value.

---

### DECO

**Type:** INSTRUCTION
**Category:** Bit Operations
**Difficulty Level:** Beginner
**Tags:** bit, bit-operations, data, deco, input, value

#### Description

The function is for decoding, allowing the specified bit position in the input value to be set, which can be applied in scenarios that require bit manipulation of data, especially when specific bits need to be set based on the input value.

#### Parameters

**Inputs:**

- **IN** (`UINT`): The position of the bit to be set in the output value.

#### Example Code

```scl
Provides SCL example code demonstrating how to use the DECO instruction for decoding operations.
```

#### Additional Information

If the value of parameter IN is greater than 31, execute the instruction modulo 32.

---

### ENCO

**Type:** INSTRUCTION
**Category:** Bit Operations
**Difficulty Level:** Beginner
**Tags:** bit, bit-operations, enco, input, read, string, value

#### Description

The function is for encoding, reading the bit number of the least significant bit set in the input value, applicable in scenarios where it is necessary to encode the input bit string to obtain the position of the first bit set to 1 in the bit string.

#### Parameters

**Inputs:**

- **IN** (`bit string`): Input value.

#### Example Code

```scl
Provided SCL example code that demonstrates how to use the ENCO instruction for encoding operations.
```

#### Additional Information

If the value of the parameter IN is 0, the output OUT will be '0'.

---

### ENDIS_PW

**Type:** INSTRUCTION
**Category:** Bit Operations
**Difficulty Level:** Advanced
**Tags:** access, bit-operations, control

#### Description

This function is used to lock and unlock passwords for various access levels in the CPU and can be applied in scenarios that require control over different access level permissions, such as terminating existing legitimate connections or granting specific users access to the fail-safe CPU.

#### Parameters

**Inputs:**

- **REQ** (`BOOL`): Determines the current password status for each access level in the CPU. -- F_PWD, Input, BOOL, locks or unlocks the password for the access level 'full access including fail-safe (unprotected)'.
- **FULL_PWD** (`BOOL`): Locks or unlocks the password for the access level 'full access (unprotected)'.
- **R_PWD** (`BOOL`): Locks or unlocks the password for the access level 'read-only access'.
- **HMI_PWD** (`BOOL`): Locks or unlocks the password for the access level 'HMI access'.

**Outputs:**

- **F_PWD_ON** (`BOOL`): Current password status for the access level 'full access including fail-safe (unprotected)'.
- **FULL_PWD_ON** (`BOOL`): Current password status for the access level 'full access (unprotected)'.
- **R_PWD_ON** (`BOOL`): Current password status for the access level 'read-only access'.
- **HMI_PWD_ON** (`BOOL`): Current password status for the access level 'HMI access'.
- **RET_VAL** (`WORD`): Error information.

#### Example Code

```scl
Provides SCL example code demonstrating how to use the ENDIS_PW instruction to lock and unlock passwords.
```

#### Additional Information

By locking the passwords, existing legitimate connections can be terminated, and after locking, access to the fail-safe CPU can be granted to a select few users.

---

### GET_ERROR

**Type:** INSTRUCTION
**Category:** Bit Operations
**Difficulty Level:** Beginner
**Tags:** bit-operations, error

#### Description

The function retrieves local error information and can be applied in scenarios that require diagnosis and handling of error information.

#### Example Code

```scl
Provided SCL example code demonstrating how to use the GET_ERROR instruction to retrieve and handle error information.
```

#### Additional Information

Error information can only be stored in operands of the ErrorStruct system data type, and this data type can be inserted multiple times, but the name cannot be changed.

---

### GET_ERR_ID

**Type:** INSTRUCTION
**Category:** Bit Operations
**Difficulty Level:** Beginner
**Tags:** bit-operations

#### Description

The function is to obtain the local error ID, which can be applied in scenarios that require diagnosis and handling, such as obtaining error codes for appropriate error handling when errors occur in the program.

#### Example Code

```scl
Provides SCL example code that demonstrates how to use the GET_ERR_ID instruction to obtain and handle error IDs.
```

#### Additional Information

The error ID can only be stored in operands of the WORD data type.

---

### IF

**Type:** INSTRUCTION
**Category:** Bit Operations
**Difficulty Level:** Beginner
**Tags:** bit-operations, control, selection

#### Description

The function is to control the branching of program flow based on conditions, applicable in scenarios that require conditional judgment and selection of different execution paths.

#### Example Code

```scl
Provided SCL example code showing how to use the IF instruction for conditional judgment and executing corresponding instructions.
```

#### Additional Information

The IF instruction can take various forms, including the IF THEN ELSE END_IF structure, and can nest any number of ELSIF and THEN combinations.

---

### LEAD_LAG

**Type:** INSTRUCTION
**Category:** Bit Operations
**Difficulty Level:** Intermediate
**Tags:** bit-operations, control, lag, signal

#### Description

The function processes analog signals using the 'lead and lag algorithm' and can be applied in compensators for dynamic feedforward control.

#### Parameters

**Inputs:**

- **IN** (`REAL`): The input value at the current sampling time to be processed.
- **SAMPLE_T** (`INT`): Sampling time.

**Outputs:**

- **OUT** (`REAL`): The result of the instruction.
- **ERR_CODE** (`WORD`): Error information.

#### Example Code

```scl
Provides SCL example code demonstrating how to use the SHL instruction for left shift operations.
```

#### Additional Information

The gain value for the GAIN parameter must be greater than zero. If the value of GAIN is less than or equal to zero, no calculation will be performed, and an error message will be output in ERR_CODE.

---

### ROL

**Type:** INSTRUCTION
**Category:** Bit Operations
**Difficulty Level:** Beginner
**Tags:** bit, bit-operations, data, parameter, rol

#### Description

This function rotates the content of parameter IN to the left by one bit and returns the result. It can be applied in scenarios where data bits need to be rotated to the left.

#### Parameters

**Inputs:**

- **IN** (`bit string/integer`): The value to be rotated.
- **N** (`USINT/UINT/UDINT/ULINT`): The number of positions to rotate the value (IN).

#### Example Code

```scl
#Result := ROL(IN := #valueToRotate, N := #numberBitPos);
```

#### Additional Information

If the value of parameter N is '0', the input IN value is returned as the result. If the value of parameter N is greater than the available bits, the operand value in IN will be rotated by the specified number of positions.

---

### SEG

**Type:** INSTRUCTION
**Category:** Bit Operations
**Difficulty Level:** Beginner
**Tags:** bit, bit-operations, seg

#### Description

The function converts the specified source word of four hexadecimal digits into an equivalent bit pattern for a 7-segment display, which can be used to generate bit patterns for 7-segment displays.

#### Parameters

**Inputs:**

- **IN** (`WORD`): Source word represented by four hexadecimal digits.

**Outputs:**

- **OUT** (`DWORD`): Bit pattern for a 7-segment display.

#### Example Code

```scl
SCL example code is provided, demonstrating how to use the SHL instruction for left shift operations.
```

#### Additional Information

The result of the instruction is output as a double word in the OUT parameter.

---

### SHL

**Type:** INSTRUCTION
**Category:** Bit Operations
**Difficulty Level:** Beginner
**Tags:** bit, bit-operations, operation, parameter, shl, string

#### Description

The function is to shift the contents of the parameters to the left bit by bit, applicable in scenarios where left shift operations on bit strings or integers are needed.

#### Parameters

**Inputs:**

- **IN** (`Bit string or integer`): The value to be shifted.
- **N** (`USINT, UINT, etc.`): The number of bits to shift the value (IN).

#### Example Code

```scl
#Result := SHL(IN := #in_byte, N := #n); Used to shift the operand #in_byte to the left by #n bits. The result of this instruction is returned as the function value in the 'Result' operand.
```

#### Additional Information

The bits that are vacated in the result due to the shift will be filled with 0s.

---

### SHR

**Type:** INSTRUCTION
**Category:** Bit Operations
**Difficulty Level:** Beginner
**Tags:** bit, bit-operations, parameter, shr

#### Description

The function is to shift the content of the parameter bit by bit to the right, applicable in scenarios where right bit manipulation is required.

#### Parameters

**Inputs:**

- **IN** (`Bit string or integer`): The value to be shifted.
- **N** (`USINT, UINT, etc.`): The number of bits to shift the value (IN).

#### Example Code

```scl
#Result := SHR(IN := #in_byte, N := #n);  This is used to right shift the operand #in_byte by #n bits. The result of this instruction is returned as the function value in the 'Result' operand.
```

#### Additional Information

When shifting unsigned values, the vacated bits on the left are filled with zeros; when shifting signed values, the sign bit's status is used to fill the vacated bits.

---

### SMC

**Type:** INSTRUCTION
**Category:** Bit Operations
**Difficulty Level:** Intermediate
**Tags:** bit, bit-operations, compare, control, input, signal, smc, state

#### Description

The function compares a scanned matrix and can be used to match the signal status of input bits with a comparison mask, commonly used to find the matching step number based on the state of input bits for program flow control.

#### Parameters

**Inputs:**

- **IN_BIT0 to IN_BIT15** (`BOOL`): Compares the input bits with the mask bits.

**Outputs:**

- **OUT** (`BOOL`): Signal status '1' indicates a match was found.
- **OUT_STEP** (`BYTE`): Contains the step number with the matching mask.
- **ERR_CODE** (`WORD`): Error information.

#### Example Code

```scl
Provides SCL example code that demonstrates how to use the SHL instruction for left shift operations.
```

#### Additional Information

If a match is found, the signal status of parameter OUT is set to '1', and the step number with the matching mask is written to parameter OUT_STEP. If multiple steps have matching masks, parameter OUT_STEP only indicates the first step found. If no match is found, the signal status of parameter OUT is set to '0'.

---

### CEIL

**Type:** INSTRUCTION
**Category:** Comparison & Logic
**Difficulty Level:** Beginner
**Tags:** ceil, comparison-logic, value

#### Description

The function rounds a floating point number up to the nearest integer, which can be applied in scenarios where it is necessary to adjust a floating point value to the closest integer that is greater than or equal to that value.

#### Parameters

**Inputs:**

- **expression** (`float`): Input value.

#### Example Code

```scl
CEIL(#inputValue);
```

#### Additional Information

The function value can be greater than or equal to the input value.

---

### EXIT

**Type:** INSTRUCTION
**Category:** Comparison & Logic
**Difficulty Level:** Beginner
**Tags:** comparison-logic, exit

#### Description

The function is used to cancel the execution of FOR, WHILE, or REPEAT loops at any time, regardless of whether conditions are met, and can be applied in scenarios where there is a need to prematurely terminate a loop before completion.

#### Example Code

```scl
Provided SCL example code demonstrates how to use the EXIT instruction to exit a loop when specific conditions are met.
```

#### Additional Information

The EXIT instruction will affect the program loop in which it is located.

---

### LIMIT

**Type:** INSTRUCTION
**Category:** Comparison & Logic
**Difficulty Level:** Beginner
**Tags:** comparison-logic, limit, parameter, value

#### Description

The function restricts the value of the IN parameter to be between the values of MN and MX, which can be applied in scenarios requiring range limits on a value.

#### Parameters

**Inputs:**

- **MN** (`Integer, Float, TIME, TOD, DATE, DTL`): Lower limit.
- **IN** (`Integer, Float, TIME, TOD, DATE, DTL`): Input value.
- **MX** (`Integer, Float, TIME, TOD, DATE, DTL`): Upper limit.

#### Example Code

```scl
#Result := LIMIT(MN := #Minimum, IN := #Value, MX := #Maximum);
```

#### Additional Information

If MN is greater than MX, the result will be the value of the IN parameter, and ENO will be '0'.

#### Related Functions

- `MIN`
- `MAX`


---

### MoveFromResolvedSymbol

**Type:** INSTRUCTION
**Category:** Comparison & Logic
**Difficulty Level:** Beginner
**Tags:** comparison-logic, from, move, read, resolved, symbol, value, write

#### Description

This function reads the value of a variable referenced by a resolved symbol and writes it to the target variable. It can be used in SCL programming when assigning the value of a resolved symbol reference to a target variable.

#### Example Code

```scl
MoveFromResolvedSymbol(SRC := MySrcDB.Input_ResolvedSymbol, DST => MyTargetDB.Output_Variant);
```

#### Additional Information

The variable must have been resolved using the ResolveSymbols instruction beforehand. The data types of the source and target variables must be the same.

---

### MoveToResolvedSymbol

**Type:** INSTRUCTION
**Category:** Comparison & Logic
**Difficulty Level:** Beginner
**Tags:** comparison-logic, move, read, resolved, symbol, value, write

#### Description

This function reads the variable value and writes it into the target variable referenced by the resolved symbol. It can be applied in scenarios within SCL programming where the value of a resolved variable needs to be passed to another variable.

#### Example Code

```scl
MoveToResolvedSymbol(SRC := MySrcDB.Input_Variant, DST => MyTargetDB.Output_ResolvedSymbol);
```

#### Additional Information

The variables must have been resolved using the ResolveSymbols instruction beforehand. The data types of the source variable and the target variable must be the same.

---

### SCALE_X

**Type:** INSTRUCTION
**Category:** Comparison & Logic
**Difficulty Level:** Intermediate
**Tags:** comparison-logic, value

#### Description

This function maps a float to a specified value range for scaling, and can be applied in scenarios that require proportional transformation and range limitation of floating point values.

#### Parameters

**Inputs:**

- **EN** (`BOOL`): Enable input.
- **MIN** (`Integer or Float`): Lower limit of the value range.
- **VALUE** (`Float`): Value to be scaled.
- **MAX** (`Integer or Float`): Upper limit of the value range.

**Outputs:**

- **ENO** (`BOOL`): Enable output.

#### Example Code

```scl
SCALE_X(MIN := #minLim, VALUE := #inputValue, MAX := #maxLim);
```

#### Additional Information

The calculation is done using the formula OUT = [VALUE * (MAX - MIN)] + MIN. If the enable input EN signal state is '0' or the value of MIN is greater than or equal to MAX, the enable output ENO will return the signal state '0'.

---

### BITSUM

**Type:** INSTRUCTION
**Category:** Counter
**Difficulty Level:** Beginner
**Tags:** bit, bitsum, counter

#### Description

This function counts the number of bits set to '1' in the operand, applicable for situations where the count of 1's in a DWORD type operand needs to be determined.

#### Parameters

**Inputs:**

- **Operand** (`DWORD`): The operand for which to count the number of bits set to 1.

#### Example Code

```scl
BITSUM(#inputValue);
```

#### Additional Information

No other useful information provided in the documentation.

---

### CTU

**Type:** INSTRUCTION
**Category:** Counter
**Difficulty Level:** Intermediate
**Tags:** counter, ctu, instruction, parameter, signal, state, value

#### Description

This function increments the value of the CV parameter using the 'Count Up' instruction when the signal state of CU transitions from '0' to '1'. It can be applied in scenarios that require counting or tracking the number of occurrences of events, such as counting products on a production line or tracking the number of times a machine operates.

#### Parameters

**Inputs:**

- **CU** (`BOOL`): Count input.
- **R** (`BOOL`): Reset input.
- **PV** (`INTEGER`): Target value for the output Q.

**Outputs:**

- **Q** (`BOOL`): Status of the counter.
- **CV** (`INTEGER, CHAR, WCHAR, DATE`): Current value of the counter.

#### Example Code

```scl
IEC_COUNTER_DB.CTU(CU := Start, R := Reset, PV := PresetValue, Q => Status, CV => CounterValue);
```

#### Additional Information

The counter value increments until it reaches the upper limit of the data type.

#### Related Functions

- `CTD`
- `CTUD`


---

### Deserialize

**Type:** INSTRUCTION
**Category:** Counter
**Difficulty Level:** Beginner
**Tags:** array, counter, data, deserialize, instruction

#### Description

The function allows using the 'Deserialize' instruction to reverse-convert PLC data types (UDT), STRUCT, or ARRAY into their sequential representation and populate all content. It can be applied when needing to convert serialized data structures back to their original form.

#### Parameters

**Inputs:**

- **SRC_ARRAY** (`ARRAY[*] of BYTE or ARRAY of CHAR`): An ARRAY of BYTE or ARRAY of CHAR used to hold the data stream that will be deserialized.

#### Example Code

```scl
No example code, but it is typically used when needing to convert a serialized data structure back to its original form.
```

#### Additional Information

Ensure there is sufficient storage space before conversion, and the data type of SRC_ARRAY must be an ARRAY of BYTE or ARRAY of CHAR.

---

### FOR

**Type:** INSTRUCTION
**Category:** Counter
**Difficulty Level:** Beginner
**Tags:** array, counter, data, for, operation

#### Description

The function is to repeatedly execute the program loop in a counting loop, applicable in scenarios requiring repeated operations, such as processing array elements, batch data processing, etc.

#### Example Code

```scl
Provides SCL example code demonstrating how to use the FOR instruction for looping operations.
```

#### Additional Information

FOR loops can be nested, and care should be taken to avoid infinite loops while writing. Pay attention to the data type and value range of the loop variable.

---

### GATHER_BLK

**Type:** INSTRUCTION
**Category:** Counter
**Difficulty Level:** Beginner
**Tags:** array, bit, blk, counter, data

#### Description

The function combines the individual bits from an array or structure that only contains Boolean elements into one or more elements in a bit sequence array. It can be applied in scenarios where BOOL arrays or bit information from PLC data types are aggregated into an ARRAY of <bit sequences>.

#### Example Code

```scl
GATHER_BLK(IN := #SourceArrayBool[0], COUNT_OUT := #CounterOutput, OUT => #DestinationArrayWord[2]);
```

#### Additional Information

If the lower limit of the source ARRAY is not '0', the index must always start restricted to BYTE, WORD, DWORD, or LWORD.

---

### GetSymbolPath

**Type:** INSTRUCTION
**Category:** Counter
**Difficulty Level:** Beginner
**Tags:** counter, get, parameter, path, symbol

#### Description

The function is used to query the actual parameter name from the start of the call path, applicable in scenarios where there is a need to obtain the actual names of parameters passed in a function or method call.

#### Parameters

**Inputs:**

- **VARIABLE** (`PARAMETER`): Select the formal parameter. The name of the corresponding actual parameter will be read at the start of the call path.
- **SIZE** (`DINT`): Output parameter limiting the number of characters.

**Outputs:**

- **OUT** (`WSTRING`): Output the variable name from which the input parameters originate.

#### Example Code

```scl
Provides SCL example code demonstrating how to use the SHL instruction for left shift operations.
```

#### Additional Information

The GetSymbolPath instruction may increase code storage space requirements and prolong program execution time.

---

### RTM

**Type:** INSTRUCTION
**Category:** Counter
**Difficulty Level:** Intermediate
**Tags:** bit, counter, operation, read, rtm

#### Description

Functionality for setting, starting, stopping, and reading operations of the 32-bit runtime hour counter of the CPU. It can be applied in scenarios where monitoring device runtime is required.

#### Parameters

**Inputs:**

- **NR** (`RTM`): The number of the runtime hour counter.
- **MODE** (`BYTE`): Job ID.
- **PV** (`DINT`): The new value for the runtime hour counter.

**Outputs:**

- **CQ** (`BOOL`): The status of the runtime hour counter.
- **CV** (`DINT`): The current value of the runtime hour counter.

#### Example Code

```scl
Provides SCL example code demonstrating how to use the SHL instruction for left shift operations.
```

#### Additional Information

The runtime hour counter can also be stopped or restarted during the execution of the user program, but this may result in incorrect saved values.

---

### S_CUD

**Type:** INSTRUCTION
**Category:** Counter
**Difficulty Level:** Advanced
**Tags:** counter, cud, input, operation, parameter, signal, state, value

#### Description

This function assigns parameters and increments/decrements the count. It can be applied to perform count operations on a specified counter based on the states of input signals CU and CD. When the counter value reaches the upper limit of 999 or the lower limit of 0, the counter value will no longer change.

#### Parameters

**Inputs:**

- **C_NO** (`COUNTER, INT`): Counter operation.
- **CU** (`BOOL`): Increment count input.
- **CD** (`BOOL`): Decrement count input.
- **S** (`BOOL`): Input for presetting the counter.
- **PV** (`WORD`): Preset BCD format counter value.
- **R** (`BOOL`): Reset input.

**Outputs:**

- **Q** (`BOOL`): Counter status.
- **CV** (`WORD`): Current counter value.

#### Example Code

```scl
Result := S_CD(C_NO := Counter_1, CU := CU, CD := CD, S := 1, PV := PresetValue, R := Reset, Q => Status, CV => Value);
```

#### Additional Information

The counter value stops changing when it reaches the upper limit of 999 or the lower limit of 0.

---

### Serialize

**Type:** INSTRUCTION
**Category:** Counter
**Difficulty Level:** Beginner
**Tags:** array, counter, data, serialize

#### Description

This function converts multiple PLC data types (such as UDT, STRUCT, or ARRAY of <data type>) into a sequential representation for temporary storage and transmission of structured data items to other CPUs. It can be applied in scenarios where complex data structures need to be transmitted between different CPUs, provided the data size does not exceed 64 KB.

#### Example Code

```scl
No specific example code.
```

#### Additional Information

The padding data in the source data area is not defined in the target array. The standard storage area has a capacity of 64 KB, and structures larger than 64 KB cannot be serialized.

---

### CTD

**Type:** INSTRUCTION
**Category:** Edge Detection
**Difficulty Level:** Intermediate
**Tags:** counter, ctd, edge, edge-detection, instruction, parameter, rising, signal, state, value

#### Description

This function is a decrement count instruction used to reduce the value of the CV parameter. When the signal state of parameter CD changes from '0' to '1' (rising edge), this instruction is executed to decrease the current counter value CV by '1'. This instruction can be applied in scenarios where counting events is required or when the count value needs to be decremented upon reaching specific conditions.

#### Parameters

**Inputs:**

- **CD** (`BOOL`): Count input.
- **LD** (`BOOL`): Load input.
- **PV** (`Integer`): Preset value to set output CV when LD = 1.

**Outputs:**

- **Q** (`BOOL`): Counter status.
- **CV** (`Integer, CHAR, WCHAR, DATE`): Current counter value.

#### Example Code

```scl
IEC_SCOUNTER_DB.CTD(CD := Start, LD := Load, PV := PresetValue, Q => Status, CV => CounterValue);
```

#### Additional Information

The counter value decreases until it reaches the lower limit of the data type.

#### Related Functions

- `CTU`
- `CTUD`


---

### MCAT

**Type:** INSTRUCTION
**Category:** Edge Detection
**Difficulty Level:** Advanced
**Tags:** control, edge-detection, input, mcat, timing

#### Description

The function is used to start timing when receiving an open command input (either open or close). If it exceeds the preset time before feedback is received, the corresponding alarm is triggered. This can be applied in scenarios requiring control of devices to complete opening or closing actions within a specified time.

#### Parameters

**Inputs:**

- **O_CMD** (`BOOL`): "Open" command input.
- **C_CMD** (`BOOL`): "Close" command input.
- **S_CMD** (`BOOL`): "Stop" command input.
- **O_FB** (`BOOL`): Feedback input when opened.
- **C_FB** (`BOOL`): Feedback input when closed.

**Outputs:**

- **OO** (`BOOL`): "Open" output.
- **CO** (`BOOL`): "Close" output.
- **OA** (`BOOL`): Alarm output when opened.
- **CA** (`BOOL`): Alarm output when closed.
- **Q** (`BOOL`): Signal status "0" indicates an error state.

#### Example Code

```scl
SCL example code is provided, demonstrating how to use the SHL instruction for left shift operations.
```

#### Additional Information

The instruction's response to various input conditions is detailed, listing changes in output parameters under different situations.

---

### RE_TRIGR

**Type:** INSTRUCTION
**Category:** Edge Detection
**Difficulty Level:** Beginner
**Tags:** edge-detection, trigr

#### Description

Function is to reset the cycle monitoring time, applicable in scenarios requiring re-triggering of the CPU's cycle time monitoring.

#### Parameters

**Inputs:**

- **MODE** (`UINT`): Specifies the mode for shutting down or restarting.
- **COMMENT** (`STRING`): Specifies the reason for the restart.

#### Example Code

```scl
RE_TRIGR();
```

#### Additional Information

This instruction does not take any parameters and does not provide error information; it is used to re-trigger the CPU cycle time monitoring.

---

### S_CD

**Type:** INSTRUCTION
**Category:** Edge Detection
**Difficulty Level:** Advanced
**Tags:** counter, edge, edge-detection, instruction, rising, signal, value

#### Description

This function serves as a decrement count instruction, applicable in scenarios where it is necessary to decrement the counter value based on the rising edge of a certain signal.

#### Parameters

**Inputs:**

- **C_NO** (`COUNTER, INT`): Counter operation.
- **CD** (`BOOL`): Decrement count input.
- **S** (`BOOL`): Input terminal for presetting the counter.
- **PV** (`WORD`): Preset value of the counter in BCD format.
- **R** (`BOOL`): Reset input.

**Outputs:**

- **Q** (`BOOL`): Counter status.
- **CV** (`WORD`): Current counter value.

#### Example Code

```scl
Result := S_CD(C_NO := Counter_1, CD := Start, S := 1, PV := PresetValue, R := Reset, Q => Status, CV => Value);
```

#### Additional Information

The counter stops decrementing when the counter value reaches the lower limit of 0.

---

### S_CU

**Type:** INSTRUCTION
**Category:** Edge Detection
**Difficulty Level:** Advanced
**Tags:** counter, edge, edge-detection, parameter, rising, signal, state, value

#### Description

This function increments the specified counter when the CU parameter's signal state changes from '0' to '1' (rising edge). It can also stop counting after reaching 999, making it suitable for scenarios that require event counting or incrementing counter values at specific moments.

#### Parameters

**Inputs:**

- **C_NO** (`COUNTER, INT`): Counter operation.
- **CU** (`BOOL`): Count input.
- **S** (`BOOL`): Input for presetting the counter.
- **PV** (`WORD`): Preset BCD format counter value.
- **R** (`BOOL`): Reset input.

**Outputs:**

- **Q** (`BOOL`): Counter status.
- **CV** (`WORD`): Current counter value.

#### Example Code

```scl
Result := S_CU(C_NO := Counter_1, CU := Start, S := 1, PV := PresetValue, R := Reset, Q => Status, CV => Value);
```

#### Additional Information

The counter stops increasing after reaching the upper limit of 999.

---

### AssignmentAttempt

**Type:** INSTRUCTION
**Category:** General Instructions
**Difficulty Level:** Beginner
**Tags:** assignment, attempt, general-instructions, value

#### Description

The function is for assigning values to reference variables and can be applied in scenarios where values need to be assigned to variables in SCL.

#### Example Code

```scl
The block interface is designed as follows.
```

#### Additional Information

In SCL, NULL can also be assigned during an assignment attempt, specifically setting references to NULL.

---

### CONTINUE

**Type:** INSTRUCTION
**Category:** General Instructions
**Difficulty Level:** Beginner
**Tags:** continue, general-instructions

#### Description

The function is used to end the current program execution of a FOR, WHILE, or REPEAT loop and re-evaluate the conditions for continuing the loop, applicable for skipping the remaining part of the current loop when specific conditions are met.

#### Example Code

```scl
Provides SCL example code demonstrating how to use the CONTINUE instruction to skip the remaining part of the current loop when specific conditions are met.
```

#### Additional Information

The CONTINUE instruction affects the program loop in which it is located.

---

### FILL

**Type:** INSTRUCTION
**Category:** General Instructions
**Difficulty Level:** Beginner
**Tags:** data, fill, general-instructions

#### Description

The function fills the target area with data from the source area until the target area is full, applicable in scenarios requiring the copying of content from one storage area to another.

#### Parameters

**Inputs:**

- **BVAL** (`Variant`): The specified storage area (source area) from which the content will be used to fill the target area specified in the BLK parameter.

**Outputs:**

- **BLK** (`Variant`): The specified storage area to be filled with data from the source area.

#### Example Code

```scl
SCL example code is provided to demonstrate how to use the FILL instruction to fill data.
```

#### Additional Information

The source and target areas must not overlap, and there are specific movement rules.

---

### FRAC

**Type:** INSTRUCTION
**Category:** General Instructions
**Difficulty Level:** Beginner
**Tags:** frac, general-instructions

#### Description

The function returns the decimal part of a number and can be applied in scenarios where the decimal part of a float number is needed.

#### Parameters

**Inputs:**

- **<expression>** (`float`): Input value.

#### Example Code

```scl
#Result1 := FRAC(Value);
```

---

### GOTO

**Type:** INSTRUCTION
**Category:** General Instructions
**Difficulty Level:** Beginner
**Tags:** general-instructions, goto

#### Description

The function allows the program to continue execution from a specified point marked by a jump label, applicable in scenarios requiring unconditional jumps within the program.

#### Example Code

```scl
Provided SCL example code demonstrating how to use the GOTO instruction for program jumping.
```

#### Additional Information

Jump labels and the GOTO instruction must be in the same block, and the jump label name can only be specified once.

---

### GetSymbolName

**Type:** INSTRUCTION
**Category:** General Instructions
**Difficulty Level:** Beginner
**Tags:** general-instructions, get, input, name, parameter, read, symbol

#### Description

Functionality to read the variable name of the input parameter, applicable in scenarios where variable names need to be retrieved.

#### Parameters

**Inputs:**

- **VARIABLE** (`PARAMETER`): Selects the local interface to read the name of the input parameter.
- **SIZE** (`DINT`): Limit value for the output character count in the OUT parameter.

#### Example Code

```scl
SCL example code provided to demonstrate how to use the SHL instruction for left shift operations.
```

#### Additional Information

The GetSymbolName instruction may lead to increased code memory requirements and longer program execution time.

---

### INIT_RD

**Type:** INSTRUCTION
**Category:** General Instructions
**Difficulty Level:** Beginner
**Tags:** data, general-instructions

#### Description

The function is to initialize all retained data, which can be applied to reset all retained data in the startup OB.

#### Parameters

**Inputs:**

- **Operand** (`BOOL`): If the signal status of input 'REQ' is '1', reset all retained data.

**Outputs:**

- **RET_VAL** (`INT`): Error information.

#### Example Code

```scl
Provides SCL example code demonstrating how to use the INIT_RD instruction to reset all retained data.
```

#### Additional Information

The execution time of this instruction exceeds the duration of the program cycle, so it can only be executed in the startup OB.

---

### NORM_X

**Type:** INSTRUCTION
**Category:** General Instructions
**Difficulty Level:** Intermediate
**Tags:** general-instructions, input, value

#### Description

The function maps the input value to a linear scale for normalization, applicable in scenarios where a value needs to be normalized according to a specified range.

#### Parameters

**Inputs:**

- **EN** (`BOOL`): Enable input.
- **MIN** (`integer or float`): Lower limit of the value range.
- **VALUE** (`integer or float`): The value to be normalized.
- **MAX** (`integer or float`): Upper limit of the value range.

**Outputs:**

- **ENO** (`BOOL`): Enable output.

#### Example Code

```scl
NORM_X(MIN := #minLim, VALUE := #inputValue, MAX := #maxLim);
```

#### Additional Information

The calculation is performed using the formula OUT = (VALUE - MIN) / (MAX - MIN). If the enable input signal EN is '0' or the value of MIN is greater than or equal to MAX, the enable output ENO returns a signal state of '0'.

---

### REF

**Type:** INSTRUCTION
**Category:** General Instructions
**Difficulty Level:** Beginner
**Tags:** general-instructions, ref

#### Description

The function allows the use of the REF() keyword to specify the variable that the reference points to, applicable in situations where references need to be declared in the block interface and variables assigned in program code.

#### Parameters

**Inputs:**

- **Expression** (`Bit sequence, integer, floating point, etc.`): The variable that the reference will point to.

#### Example Code

```scl
Provided SCL example code that demonstrates how to declare references in the block interface and assign the corresponding variables in the program code.
```

#### Additional Information

Before using REF(), a reference must be declared in the block interface, and the specified variable's data type must exactly match the data type of the declared reference.

---

### REPEAT

**Type:** INSTRUCTION
**Category:** General Instructions
**Difficulty Level:** Beginner
**Tags:** general-instructions, repeat

#### Description

The function is used to repeatedly execute a program loop until a certain condition is met, applicable in scenarios where actions need to be repeated until specific conditions are fulfilled.

#### Example Code

```scl
Provided SCL example code demonstrating how to use the REPEAT instruction for looping operations.
```

#### Additional Information

Even if the termination condition is met, the REPEAT instruction executes only once and can control the execution of loops through the CONTINUE and EXIT instructions.

---

### ROUND

**Type:** INSTRUCTION
**Category:** General Instructions
**Difficulty Level:** Beginner
**Tags:** general-instructions, input, round, value

#### Description

The function rounds the input value to the nearest integer. If the input value is exactly between an even and an odd number, the even number is chosen. It can be applied in scenarios where floating-point numbers need to be rounded.

#### Parameters

**Inputs:**

- **expression** (`float`): The input value to be rounded.

#### Example Code

```scl
ROUND(#inputValToRound);
```

#### Additional Information

If the input value is exactly between an even and an odd number, the even number is chosen.

---

### RUNTIME

**Type:** INSTRUCTION
**Category:** General Instructions
**Difficulty Level:** Beginner
**Tags:** general-instructions, runtime

#### Description

The function measures the program's execution time and can be applied in scenarios where precise measurement of program block execution time is needed.

#### Parameters

#### Example Code

```scl
RUNTIME(#memory);
```

#### Additional Information

This instruction uses an internal high-frequency counter to measure time. If the counter overflows, the return value of this instruction will be <= 0.0.

---

### SHUT_DOWN

**Type:** INSTRUCTION
**Category:** General Instructions
**Difficulty Level:** Beginner
**Tags:** down, general-instructions

#### Description

The function is to shut down the target system, including the CPU and Windows, and can be applied in scenarios requiring safe shutdown or restart of the system.

#### Parameters

**Inputs:**

- **MODE** (`UINT`): Specifies the mode for shutdown or restart.
- **COMMENT** (`STRING`): Specifies the reason for the restart.

#### Example Code

```scl
Provides SCL example code demonstrating how to use the SHUT_DOWN instruction to shut down or restart the system.
```

#### Additional Information

Different shutdown or restart operations are performed based on the value of the MODE parameter.

---

### SNC_RTCB

**Type:** INSTRUCTION
**Category:** General Instructions
**Difficulty Level:** Beginner
**Tags:** general-instructions, rtcb

#### Description

The function synchronizes the clock slaves, transferring the date and time of the master clock from a specific bus segment to all clock slaves in that bus segment. It can be applied in scenarios where it is necessary to synchronize the date and time of the master clock with the slaves.

#### Parameters

**Outputs:**

- **RET_VAL** (`INT`): If an error occurs during execution, the return value will contain the error code.

#### Example Code

```scl
SCL example code is provided, demonstrating how to use the SHL instruction for left shift operations.
```

#### Additional Information

Synchronization can only succeed if 'SNC_RTCB' is called on a CPU that is designated as the master clock for at least one bus segment.

---

### SQR

**Type:** INSTRUCTION
**Category:** General Instructions
**Difficulty Level:** Beginner
**Tags:** general-instructions, input, sqr, value

#### Description

This function calculates the square of the input value and stores the result in the specified operand, which can be applied in scenarios that require numerical square calculations.

#### Parameters

**Inputs:**

- **<expression>** (`Real`): Input value.

#### Example Code

```scl
Result1 := SQR(#Value);
```

#### Additional Information

The result is the square of the input value.

---

### SWAP

**Type:** INSTRUCTION
**Category:** General Instructions
**Difficulty Level:** Beginner
**Tags:** data, general-instructions, input, swap, value

#### Description

This function can change the order of bytes in the input value and store the result in the specified operand. It can be applied in situations where a change of data byte order is needed.

#### Example Code

```scl
Result := SWAP(Value);
```

#### Additional Information

No specific additional information.

---

### TIME_TCK

**Type:** INSTRUCTION
**Category:** General Instructions
**Difficulty Level:** Beginner
**Tags:** general-instructions, read, tck

#### Description

The function is to read the CPU's system time, which can be applied in scenarios that require obtaining the current system time or calculating program run time.

#### Parameters

#### Example Code

```scl
Provides SCL example code demonstrating how to use the SHL instruction for left shift operations.
```

#### Additional Information

The system time is a time counter that starts counting from 0 up to a maximum value of 2147483647 ms. When overflow occurs, the system time will restart counting from '0'.

---

### TRUNC

**Type:** INSTRUCTION
**Category:** General Instructions
**Difficulty Level:** Beginner
**Tags:** general-instructions, input, trunc, value

#### Description

The function is used for truncating to an integer, directly extracting the integer part from the input value, applicable in scenarios where the integer part of a float is needed while ignoring the decimal part.

#### Parameters

**Inputs:**

- **Expression** (`Float`): Input value.

#### Example Code

```scl
TRUNC(#inputValue);
```

#### Additional Information

This instruction only selects the integer part of the input value, excluding decimal places.

---

### T_DIFF

**Type:** INSTRUCTION
**Category:** General Instructions
**Difficulty Level:** Beginner
**Tags:** diff, general-instructions, value

#### Description

This function calculates the difference between two time values and can be applied in scenarios where calculating the interval between two points in time is necessary.

#### Parameters

**Inputs:**

- **IN1** (`DTL`): DATE, TOD, minuend.
- **IN2** (`DTL`): DATE, TOD, subtrahend.

#### Example Code

```scl
T_DIFF(IN1 := #todvalue1, IN2 := #todvalue2);
```

#### Additional Information

If the time value in the IN2 input parameter is greater than the time value in the IN1 input parameter, a negative result will be output in the OUT output parameter.

---

### UFILL_BLK

**Type:** INSTRUCTION
**Category:** General Instructions
**Difficulty Level:** Beginner
**Tags:** blk, data, general-instructions, input, value

#### Description

The function is to fill a storage area with input values in a non-interruptible manner, applicable in scenarios that require continuous and uninterrupted filling of large amounts of data.

#### Example Code

```scl
UFILL_BLK(IN := #FillValue, COUNT := Count, OUT => #TargetArea[1]);
```

#### Additional Information

This move operation will not be interrupted by other tasks of the operating system. This instruction can be used to move up to 16 KB of data.

---

### UMOVE_BLK

**Type:** INSTRUCTION
**Category:** General Instructions
**Difficulty Level:** Beginner
**Tags:** blk, data, general-instructions, operation

#### Description

The function is to move data from one storage area to another, and the move operation cannot be interrupted. It can be applied in scenarios that require the secure and reliable transfer of large amounts of data (up to 16 KB).

#### Example Code

```scl
UMOVE_BLK(IN := #a_array[2], COUNT := Count, OUT => #b_array[1]);
```

#### Additional Information

This move operation cannot be interrupted by other tasks of the operating system. The CPU has specific limitations, allowing this instruction to move a maximum of 16 KB of data.

---

### WHILE

**Type:** INSTRUCTION
**Category:** General Instructions
**Difficulty Level:** Beginner
**Tags:** general-instructions, operation, while

#### Description

The function is to repeatedly execute a program loop while a condition is met, applicable in scenarios that require a set of operations to be repeated until a specific condition is satisfied.

#### Example Code

```scl
Provided SCL example code demonstrating how to use the WHILE instruction for looping operations.
```

#### Additional Information

WHILE loops can be nested and controlled through the CONTINUE and EXIT instructions.

---

### WR_LOC_T

**Type:** INSTRUCTION
**Category:** General Instructions
**Difficulty Level:** Beginner
**Tags:** general-instructions

#### Description

This function is used to set the date and time of the CPU clock and can be applied in scenarios requiring synchronization or setting system time.

#### Parameters

**Inputs:**

- **LOCTIME** (`DTL`): LDT, local time.
- **DST** (`BOOL`): Daylight Saving Time.

#### Example Code

```scl
WR_LOC_T(LOCTIME := #inputLocTIME, DST := #dstValue);
```

#### Additional Information

The granularity of time information for local time and system time depends on the specific product and is at least 1 millisecond.

---

### BLKMOV

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Beginner
**Tags:** blkmov, data, memory, memory-data

#### Description

Functionality is to move data from one memory area to another; it can be applied in scenarios where data blocks need to be copied in ascending address order.

#### Parameters

**Inputs:**

- **SRCBLK** (`Variant`): Specifies the memory area to be moved (source area).

**Outputs:**

- **DSTBLK** (`Variant`): Specifies the memory area to which the block will be moved (destination area).

#### Example Code

```scl
SCL sample code is provided to demonstrate how to use the BLKMOV instruction to copy data and handle potential errors.
```

#### Additional Information

The variables of this instruction are only applicable to memory areas where the 'Optimize Block Access' property is not activated. The source and destination areas must not overlap, and there are specific moving rules.

---

### Chars_TO_Strg

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Intermediate
**Tags:** array, chars, memory-data, strg, string

#### Description

This function copies a character array to a string or WSTRING type string, applicable in scenarios where there is a need to convert a character array into a string type for further processing.

#### Parameters

**Inputs:**

- **CHARS** (`Variant`): The source for the copy operation.
- **PCHARS** (`DINT`): The position in the array of (W)CHAR / BYTE / WORD from which to start copying characters.
- **CNT** (`UINT`): The number of characters to copy.

**Outputs:**

- **STRG** (`STRING`): The target of the copy operation in WSTRING.

#### Example Code

```scl
Chars_TO_Strg(Chars := inputArrayCHARS,pChars := pointerCHARS,Cnt := countCHARS,Strg=>outputSTRG);
```

#### Additional Information

The copy operation only supports ASCII characters. If the length of the string is less than the number of characters in the source domain, the maximum number of characters will be written in the string.

---

### DB_ANY_TO_Variant

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Beginner
**Tags:** data, memory-data, read, variant

#### Description

The function generates a Variant variable from the data block, applicable in scenarios where data blocks need to be read and converted to Variant types.

#### Parameters

**Inputs:**

- **IN** (`DB_ANY`): The data block whose number is to be read.

**Outputs:**

- **ERR** (`INT`): Error information.

#### Example Code

```scl
DB_ANY_TO_Variant(in := #nbrOfDB, err => #error);
```

#### Additional Information

If the conditions are met, this instruction is executed. If not met or the data block does not exist, the value NULL is output in the RET_VAL parameter.

---

### FILL_BLK

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Beginner
**Tags:** blk, input, memory, memory-data, value

#### Description

The function fills a storage area with the input value starting from a specified address. It can be applied in scenarios where a specific value needs to be filled into a designated storage area, such as initializing a block of memory.

#### Example Code

```scl
FILL_BLK(IN := #FillValue, COUNT := Count, OUT => #TargetArea[1]);
```

#### Additional Information

This instruction can only be executed when the data types of the source range and the target range are the same. If the copied data exceeds the elements in the OUT output, unexpected results will be returned.

---

### GATHER

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Beginner
**Tags:** array, bit, data, gather, memory-data

#### Description

The function combines individual bits into a bit sequence and can be applied to combine bits from ARRAY of BOOL, anonymous STRUCT, or PLC data types that contain only boolean elements into a single bit sequence.

#### Example Code

```scl
GATHER(IN := #SourceArray, OUT => #DestinationWord);
```

#### Additional Information

Multidimensional ARRAY of BOOL does not support this instruction. The number of elements contained in ARRAY, STRUCT, or PLC data types must exactly match the number specified by the bit sequence.

---

### GetInstanceName

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Beginner
**Tags:** data, get, instance, memory-data, name, read

#### Description

This function reads the name of the background data block in a function block, applicable when there is a need to obtain or process the name of the background data block in the program.

#### Parameters

**Inputs:**

- **SIZE** (`DINT`): Output character count limit at the OUT parameter.

**Outputs:**

- **OUT** (`WSTRING`): D, L, the name of the background data block being read.

#### Example Code

```scl
SCL example code is provided, demonstrating how to use the SHL instruction for a left shift operation.
```

#### Additional Information

The GetInstanceName instruction may increase code memory space requirements and prolong program execution time.

---

### IS_ARRAY

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Beginner
**Tags:** array, data, memory-data, state

#### Description

This function checks whether the Variant points to a variable of the ARRAY data type. It can be used in scenarios where it is necessary to determine if a certain Variant variable is of array type and to handle it accordingly within an IF statement.

#### Parameters

**Inputs:**

- **<operand>** (`Variant`): The operand for the ARRAY query.

#### Example Code

```scl
//other scl code here 
VAR_INPUT
VariantToArray : Variant;
END_VAR
IF IS_ARRAY(#VariantToArray) THEN 
#result := CountOfElements(#VariantToArray); 
END_IF;
```

#### Additional Information

Can only be used within an IF statement.

---

### JOIN

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Intermediate
**Tags:** array, data, join, memory-data, string

#### Description

The function is to concatenate multiple strings into an array using specified separators, applicable in scenarios that require integrating scattered string data into a single array format.

#### Parameters

**Inputs:**

- **Mode** (`DWORD`): Specifies the merging method (CSV or FSR).
- **RecSeparator** (`Variant`): The separator or padding character for the source string.
- **EndSeparator** (`Variant`): The separator for the end of the conversion.
- **SrcStruct** (`Variant`): Pointer to the source string.
- **Count** (`UDINT`): The number of strings to be joined.

#### Example Code

```scl
Provides SCL example code showing how to use the SHL instruction for left shift operations.
```

#### Additional Information

The JOIN instruction requires attention to the maximum length limit of the strings and the choice of separators when joining strings.

---

### LOWER_BOUND

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Beginner
**Tags:** array, bound, memory-data, read, value

#### Description

Function to read the lower bound of an ARRAY variable, applicable in scenarios where the lower bound value of a specific dimension of the array is needed.

#### Parameters

**Inputs:**

- **ARR** (`ARRAY[*]`): Array to read the variable lower bound.
- **DIM** (`UDINT`): The dimension of the array to read the variable lower bound.

#### Example Code

```scl
VAR_INPUT
ArrayA:ARRAY[*,*] of DInt;
END_VAR;
BEGIN
#Result := LOWER_BOUND(ARR := #ArrayA, DIM := 2); This instruction will read the variable lower bound value of #ArrayA from the second dimension. If the instruction is executed successfully, the result will be written to the operand 'Result'.
```

#### Additional Information

Refer to example code usage

---

### MOVE_BLK

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Beginner
**Tags:** array, blk, data, memory-data

#### Description

The function moves data from one storage area (source range) to another storage area (destination range), applicable in scenarios where elements from an array or data block need to be copied to another array or data block.

#### Parameters

**Inputs:**

- **IN** (`Variant`): SInt, Int, DInt, USInt, UInt, UDInt, Real, LReal Byte, Word, DWord, Time, Date, TOD, WChar
- **COUNT** (`UInt`): Number of elements copied. If no ARRAY is specified in the SRC or DEST parameters, set the value of the COUNT parameter to '1'.
- **OUT** (`SInt, Int, DInt, USInt, UInt, UDInt, Real, LReal Byte, Word, DWord, Time, Date, TOD, WChar`): Destination start address

#### Example Code

```scl
MOVE_BLK(IN := #a_array[2], COUNT := #countOfNumber, OUT => #b_array[1]);
```

#### Additional Information

This instruction can only be executed when the data types of the source and destination ranges are the same.

---

### MOVE_BLK_Variant

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Intermediate
**Tags:** array, data, memory-data, read, variant

#### Description

The function moves data of Variant type from one Variant type to another, applicable for scenarios requiring copying of Variant arrays or reading elements of Variant arrays.

#### Parameters

**Inputs:**

- **SRC** (`Variant`): The source block to be copied.
- **COUNT** (`UDINT`): The number of elements copied. If no ARRAY is specified in parameter SRC or DEST, the value of parameter COUNT is set to '1'.
- **SRC_INDEX** (`DINT`): Defines the first element to be copied: • The SRC_INDEX parameter is zero-based. If an ARRAY is specified in SRC, the integer in the SRC_INDEX parameter will specify the first element in the source region to be copied, regardless of the declared ARRAY limits. • If no ARRAY is specified in SRC or only a specific element of the ARRAY is specified, the value of the SRC_INDEX parameter is set to '0'.
- **DEST_INDEX** (`DINT`): Defines the starting point of the destination storage. • The DEST_INDEX parameter is zero-based. If an ARRAY is specified in DEST, the integer in the DEST_INDEX parameter will specify the first element in the destination range to be copied, regardless of the declared ARRAY limits. • If no ARRAY is specified in DEST, the value of the DEST_INDEX parameter is set to '0'.

**Outputs:**

- **DEST** (`Variant`): The target area where the content from the source block will be copied.

#### Example Code

```scl
Result := MOVE_BLK_Variant(SRC := #SrcField, COUNT := Count, SRC_INDEX := Src_Index, DEST_INDEX := Dest_Index, DEST => #DestField);
```

#### Additional Information

Regardless of how the ARRAY is later declared, parameters SRC_INDEX and DEST_INDEX always count from the lower limit '0'.

---

### MoveResolvedSymbolsFromBuffer

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Intermediate
**Tags:** buffer, data, from, instruction, memory-data, move, read, resolved, symbols, value, write

#### Description

The function reads values from the storage area and writes them into multiple resolved symbol values. It can be used in handling storage received from communication instructions (such as TRCV) and writes the received data into specified symbols.

#### Parameters

**Inputs:**

- **firstIndex** (`DINT`): The index of the first resolved symbol to be written in the target buffer.
- **lastIndex** (`DINT`): The index of the last resolved symbol to be written in the target buffer.
- **mode** (`DWORD`): Memory format, either BigEndian or LittleEndian.
- **src** (`Array of BYTE`): The source buffer from which values are read.
- **srcOffsets** (`Array of DINT`): The offsets of values in the source buffer.

#### Example Code

```scl
No specific example code, but it illustrates how to use the firstIndex and lastIndex parameters to limit the variables of resolved symbols that need to have values written, the mode parameter defines the memory format, the srcOffsets parameter specifies the offsets, the dst parameter contains references to resolved symbols, and the status parameter holds the copy status.
```

#### Additional Information

Ensure that the array limits of srcOffsets and dst match to include the offset for dst[i]. This instruction does not verify whether the specified offsets overlap, which may result in random value reads.

---

### MoveResolvedSymbolsToBuffer

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Beginner
**Tags:** buffer, memory-data, move, read, resolved, symbols, value, write

#### Description

The function reads values from resolved symbols and writes them into a buffer. It can be applied in scenarios where multiple resolved symbol values need to be stored in a designated storage area.

#### Example Code

```scl
MoveResolvedSymbolsToBuffer(firstIndex := 2, lastIndex := 7, src := MySrcDB.Input_ResolvedSymbols, dstOffsets := #Input_Offset, mode := 2#0, dst := MyTargetDB.InOut_Buffer, status := #InOut_Status);
```

#### Additional Information

The value of the mode parameter is used to define the storage format in the dst parameter. The status parameter is an INT array used to store the copy status.

---

### POKE

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Beginner
**Tags:** data, memory-data, parameter, poke, write

#### Description

The function is used to write a storage address into a standard storage area without specifying a data type. It can be applied to directly write data to a specific storage area in a program, particularly when data type is not a concern, such as writing configuration parameters or directly manipulating hardware addresses.

#### Example Code

```scl
POKE(AREA := Area, DBNUMBER := DBNumber, BYTEOFFSET := Byte, VALUE := Value);
```

#### Additional Information

If you want to write to an input, output, or bit storage area, the value of the DBNUMBER parameter must be set to '0', otherwise the instruction will be invalid.

---

### POKE_BLK

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Beginner
**Tags:** blk, data, instruction, memory-data, write

#### Description

The function uses the 'write storage area' instruction to write a storage area into different standard storage areas without specifying a data type, applicable in scenarios that require copying or moving data between different data blocks.

#### Example Code

```scl
POKE_BLK(AREA_SRC := Source_Area, DBNUMBER_SRC := Source_DBNumber, BYTEOFFSET_SRC := Source_Byte, AREA_DEST := Destination_Area, DBNUMBER_DEST := Destination_DBNumber, BYTEOFFSET_DEST := Destination_Byte, COUNT := Count);
```

#### Additional Information

If you want to write the storage address into input, output, or bit storage areas, you must set the value of the DBNUMBER parameter to '0'; otherwise, the instruction will be invalid.

---

### POKE_BOOL

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Beginner
**Tags:** bit, bool, data, memory-data, write

#### Description

The function writes a storage bit to a standard storage area and can be used to manipulate storage bits without needing to specify a data type.

#### Example Code

```scl
POKE_BOOL(AREA := Area, DBNUMBER := DBNumber, BYTEOFFSET := Byte, BITOFFSET := Bit, VALUE := Value);
```

#### Additional Information

To write a storage bit to an input, output, or bit storage area, the value of the DBNUMBER parameter must be set to '0'; otherwise, the instruction will be invalid.

---

### ReadFromArrayDB

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Beginner
**Tags:** array, data, from, memory-data, read

#### Description

The function reads an element from the ARRAY DB block referenced by the index, and can be applied in scenarios where specific position elements need to be read from an ARRAY data block in Siemens SCL programming.

#### Example Code

```scl
TagResult := ReadFromArrayDB(DB := ArrayDB, INDEX := 2, VALUE => TargetField);
```

#### Additional Information

The ARRAY data block contains only an ARRAY of <data type>. The elements of the ARRAY can be PLC data types or any other basic data types.

---

### ReadFromArrayDBL

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Beginner
**Tags:** array, data, dbl, from, memory, memory-data, read

#### Description

The function reads the element at the specified index from the ARRAY data block in load memory, applicable to scenarios where data needs to be read from a specific ARRAY DB block.

#### Example Code

```scl
ReadFromArrayDBL_DB(REQ := TagReg, DB := ArrayDB, INDEX := 2, VALUE := TargetField, BUSY => TagBusy, DONE => TagDone, ERROR => TagError);
```

#### Additional Information

If the ARRAY data block is specified with the block attribute 'store only in load memory', then the array data block will only be stored in load memory.

---

### SCATTER

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Beginner
**Tags:** array, bit, data, memory-data, operation, scatter

#### Description

The function is to parse variables of data types BYTE, WORD, DWORD, or LWORD into individual bits and store them in an ARRAY of BOOL, an anonymous STRUCT, or PLC data types that contain only Boolean elements. It can be applied in scenarios where a bit sequence needs to be decomposed into individual bits, such as performing bit-level operations on byte data.

#### Example Code

```scl
SCATTER(IN := #SourceWord, OUT => #DestinationArray);
```

#### Additional Information

Multidimensional ARRAY of BOOL does not support this instruction. The number of elements contained in an ARRAY, STRUCT, or PLC data type must exactly match the number specified by the bit sequence.

---

### SCATTER_BLK

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Beginner
**Tags:** array, bit, blk, memory-data

#### Description

The function decomposes the elements of a bit-sequence ARRAY into individual bits and can be applied in scenarios where BYTE, WORD, DWORD, or LWORD type arrays need to be broken down into single bits.

#### Example Code

```scl
SCATTER_BLK(IN := #SourceArrayWord[2], COUNT_IN := #CounterInput, OUT => #DestinationArrayBool[0]);
```

#### Additional Information

If the lower bound of the target ARRAY is not '0', the index must always start with BYTE, WORD, DWORD, or LWORD limits.

---

### SPLIT

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Intermediate
**Tags:** array, data, memory-data, split, string

#### Description

The function splits a character array into multiple strings based on specified delimiters, applicable for processing CSV and FSR formatted data.

#### Parameters

**Inputs:**

- **Mode** (`DWord`): Specifies the splitting method.
- **RecSeparator** (`Variant`): The delimiter in CSV format or the padding character in FSR format.
- **EndSeparator** (`Variant`): The delimiter at the end of the complete string.
- **SrcArray** (`Variant`): A pointer to the array to be read.

**Outputs:**

- **Count** (`UDInt`): The number of strings found.

#### Example Code

```scl
Provided SCL example code demonstrating how to use the SHL instruction for left shift operations.
```

#### Additional Information

When using the SPLIT instruction to split strings, different formatting methods and the choice of delimiters need to be considered.

---

### Strg_TO_Chars

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Beginner
**Tags:** array, chars, data, memory-data, strg, string

#### Description

The function copies a STRING or WSTRING type string to the corresponding character array, applicable in scenarios where string data needs to be converted to character array data.

#### Parameters

**Inputs:**

- **STRG** (`STRING`): WSTRING, the source for the copy operation.
- **PCHARS** (`DINT`): Location in the array of (W)CHAR / BYTE / WORD structure from where to start writing characters.

**Outputs:**

- **CNT** (`UINT`): Number of characters moved.

#### Example Code

```scl
Strg_TO_Chars(Strg := #inputSTRG,pChars := #pointerCHARS,Cnt=>#countCHARS,Chars := #myarrayCHARS);
```

#### Additional Information

This operation can only copy ASCII characters. If the number of characters in the target field is less than the number of characters in the source string, only up to the maximum length of the target field will be written.

---

### TypeOf

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Beginner
**Tags:** compare, data, instruction, memory-data, type

#### Description

The function checks the data type of the variable pointed to by a Variant or ResolvedSymbol variable and compares it, which can be used in IF or CASE instructions to determine whether the variable type matches the expected type.

#### Parameters

**Inputs:**

- **<operand>** (`binary number, integer, floating point, time, date and time, string, Variant, ResolvedSymbol`): The operand used for querying.

#### Example Code

```scl

//other scl code here 
VAR_INPUT
inputValue : Variant;
END_VAR
BEGIN
// here shows how to use `TypeOf` with Variant
 CASE TypeOf(#inputValue) OF 
Byte: // `Byte` is a predefined data type in SCL
//do something ; 
Word: // `Word` is a predefined data type in SCL 
//do something ; 
DWord: // `DWord` is a predefined data type in SCL 
//do something ;
END_CASE;
//other scl code here 

```

#### Additional Information

Can only be used in IF or CASE instructions, not allowed to assign to operands.

---

### TypeOfDB

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Beginner
**Tags:** data, memory-data, state, type

#### Description

The function is used to query the data type of a certain data block. It can be applied in SCL programming where there is a need to check the data block type addressed by a DB_ANY data type variable within IF or CASE statements.

#### Parameters

**Inputs:**

- **<operand>** (`DB_ANY`): The operand used for querying.

#### Example Code

```scl
IF TypeOfDB(#InputDBAny) = TO THEN ... END_IF;
```

#### Additional Information

Can only be used within IF or CASE statements.

---

### TypeOfElements

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Beginner
**Tags:** array, compare, data, elements, memory-data, operation, state, type

#### Description

This function checks the data type of the elements in the ARRAY of a Variant variable and compares them. It can be used in IF or CASE statements to query the data type of the variable pointed to by the Variant variable and perform conditional judgments and operations based on the query result.

#### Parameters

**Inputs:**

- **<Operand>** (`Variant`): Operand used for querying.

#### Example Code

```scl

// Other SCL code here 
VAR_INPUT
VariantToArray : Variant;
END_VAR
BEGIN
IF IS_ARRAY(#VariantToArray) AND TypeOfElements(#VariantToArray) = DInt THEN // `DInt` is a pre-defined SCL data type 
// Do something; 
END_IF;
```

#### Additional Information

Can only be used in IF or CASE statements, not allowed to assign to the operand.

---

### UBLKMOV

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Beginner
**Tags:** data, memory, memory-data, ublkmov

#### Description

The function is to perform an uninterruptible data movement in memory, applicable in scenarios that require highly reliable data transmission, ensuring that the data block is not interrupted during the moving process.

#### Parameters

**Inputs:**

- **SRCBLK** (`Variant`): Specifies the storage area to be moved (source area).

**Outputs:**

- **DSTBLK** (`Variant`): Specifies the storage area to move the block to (destination area).

#### Example Code

```scl
Provided SCL example code demonstrating how to use the UBLKMOV instruction to copy data and handle potential errors.
```

#### Additional Information

Similar to BLKMOV, but this move operation will not be interrupted by other tasks of the operating system, leading to an increased CPU interrupt response time.

---

### UPPER_BOUND

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Beginner
**Tags:** array, bound, memory-data, read, value

#### Description

The function reads the upper bound of an ARRAY variable and can be applied in scenarios where the upper bound value of a specific dimension of an array is needed.

#### Parameters

**Inputs:**

- **ARR** (`ARRAY[*]`): The array with a variable upper bound to be read.
- **DIM** (`UDINT`): The dimension of the array for which the variable upper bound is to be read.

#### Example Code

```scl
VAR_INPUT
ArrayA:ARRAY[*,*] of DInt; 
END_VAR;  
BEGIN 
#Result := UPPER_BOUND(ARR := #ArrayA, DIM := 2); This instruction will read the variable upper bound value of #ArrayA from the second dimension. If the instruction is executed successfully, the result will be written to the operand 'Result'.
```

#### Additional Information

Reference example code usage

---

### VariantGet

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Beginner
**Tags:** data, get, memory-data, read, value, variant, write

#### Description

The function reads the value of a Variant variable and writes it to another variable. It can be applied in scenarios where it is necessary to retrieve the value of a Variant type data and store it in a variable of known data type.

#### Parameters

**Inputs:**

- **SRC** (`Variant`): The variable to be read.
- **DST** (`bit string, integer, floating point, timer, datetime, string, ARRAY element, PLC data type`): Destination at which to write data.

#### Example Code

```scl

VAR_IN_OUT
VariantVal : Variant;
END_VAR

VAR_TEMP
tempVal : Int;
END_VAR
BEGIN
//other scl code here 
IF TypeOf(#VariantVal) = Int THEN 
VariantGet(SRC := #VariantVal, DST := #tempVal);
END_IF;
```

#### Additional Information

The data type of the DST parameter variable must match the data type pointed to by the Variant.

---

### Variant_TO_DB_ANY

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Beginner
**Tags:** any, data, memory-data, read, variant

#### Description

The function converts Variant to DB_ANY for querying the data block number of the variable to be read. It can be applied in scenarios that require reading data block information and handling errors.

#### Parameters

**Inputs:**

- **IN** (`Variant`): Variable to be read.

**Outputs:**

- **ERR** (`INT`): Error information.

#### Example Code

```scl
Variant_TO_DB_ANY(in := #inputSource, err => #error);
```

#### Additional Information

Executes this instruction if the condition is met; otherwise outputs '0' as the data block number.

---

### WRITE_BIG

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Beginner
**Tags:** array, big, data, memory-data, write

#### Description

The function writes data in big-endian format and can write the data of a single variable to a storage area. It is suitable for situations where data needs to be written from one variable to another array in big-endian byte order. For example, when the Variant of SRC_VARIABLE points to a basic data type, and the Variant of DEST_ARRAY is a BYTE array.

#### Example Code

```scl
#TagResult := WRITE_BIG(SRC_VARIABLE := #DINTVariable, DEST_ARRAY := #TargetField, POS := #TagPos);
```

#### Additional Information

The Variant of SRC_VARIABLE must point to a basic data type. The Variant of DEST_ARRAY must be an ARRAY of BYTE.

---

### WRITE_LITTLE

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Beginner
**Tags:** array, data, little, memory-data, value, write

#### Description

The function writes the data of a single variable into storage using little-endian byte order and can be applied to store the value of basic data type variables in a byte array in little-endian format.

#### Example Code

```scl
#TagResult := WRITE_LITTLE(SRC_VARIABLE := #DINTVariable, DEST_ARRAY := #TargetField, POS := #TagPos);
```

#### Additional Information

SRC_VARIABLE must be a variant pointing to a basic data type. DEST_ARRAY must be a variant of ARRAY of BYTE.

---

### WriteToArrayDB

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Beginner
**Tags:** array, data, memory-data, write

#### Description

The function writes the element referenced by the index into the ARRAY DB block type data block, applicable for situations where data needs to be written to the ARRAY data block.

#### Example Code

```scl
TagResult := WriteToArrayDB(DB := ArrayDB, INDEX := 2, VALUE := SourceField);
```

#### Additional Information

The ARRAY data block is a data block that only contains an ARRAY of <data type>. The elements of the ARRAY can be PLC data types or any other basic data types.

---

### WriteToArrayDBL

**Type:** INSTRUCTION
**Category:** Memory & Data
**Difficulty Level:** Beginner
**Tags:** array, data, dbl, memory, memory-data, write

#### Description

This function writes the indexed referenced element to a data block of type ARRAY DB that is stored in load memory. It can be applied in scenarios where data needs to be written to an ARRAY data block that is only stored in load memory.

#### Example Code

```scl
WriteToArrayDBL_DB(REQ := TagReg, DB := ArrayDB, INDEX := 2, VALUE := SourceField, BUSY => TagBusy, DONE => TagDone, ERROR => TagError);
```

#### Additional Information

If the ARRAY data block is specified with the block attribute 'Only stored in load memory', then the array data block will be stored only in the load memory.

---

### SEL

**Type:** INSTRUCTION
**Category:** Selection & Routing
**Difficulty Level:** Beginner
**Tags:** input, parameter, sel, selection-routing, value

#### Description

Function is to select one of the two input values based on the switch parameter. It can be applied in scenarios where different input values need to be chosen based on conditions.

#### Parameters

**Inputs:**

- **G** (`BOOL`): Switch.
- **IN0** (`Binary, Integer, etc.`): First input value.
- **IN1** (`Binary, Integer, etc.`): Second input value.

#### Example Code

```scl
Provides an SCL example code demonstrating how to use the SEL instruction to select an input value based on the switch parameter.
```

#### Additional Information

This instruction can only be executed when all parameter variables are of the same data type level.

---

### ATH

**Type:** INSTRUCTION
**Category:** String Operations
**Difficulty Level:** Beginner
**Tags:** ath, conversion, string, string-operations, value

#### Description

Function to convert an ASCII string to the corresponding hexadecimal number, applicable in scenarios requiring the conversion of string representations of hexadecimal numbers to values that can be used for calculations or display.

#### Parameters

**Inputs:**

- **IN** (`Variant`): Pointer to an ASCII string.
- **N** (`INT`): Number of ASCII characters to be converted.

**Outputs:**

- **OUT** (`Variant`): Converted hexadecimal number.

#### Example Code

```scl
Provided SCL example code demonstrating how to use the SHL instruction for left shift operations.
```

#### Additional Information

The ATH instruction only accepts the digits 0-9 and uppercase or lowercase letters A-F during conversion; other characters will be converted to 0.

---

### CONCAT

**Type:** INSTRUCTION
**Category:** String Operations
**Difficulty Level:** Beginner
**Tags:** concat, string, string-operations

#### Description

The function is to merge two strings, applicable to scenarios where two strings need to be concatenated.

#### Parameters

**Inputs:**

- **IN1** (`STRING`): WSTRING, D, L or constant, the first string.
- **IN2** (`STRING`): WSTRING, D, L or constant, the second string.

#### Example Code

```scl
#result := CONCAT(IN1 := #inputstring1, IN2 := #inputstring2);
```

#### Additional Information

The CONCAT instruction limits the result to the available length if it exceeds the length of the OUT parameter during merging.

#### Related Functions

- `MID`
- `LEFT`
- `RIGHT`


---

### CONVERT

**Type:** INSTRUCTION
**Category:** String Operations
**Difficulty Level:** Beginner
**Tags:** conversion, convert, data, string-operations, value

#### Description

The function converts the source value to the specified target data type and can be applied in scenarios where data type conversion is needed.

#### Parameters

**Inputs:**

- **Source Type** (`Binary, Integer, Floating Point, etc.`): The value to be converted.

**Outputs:**

- **Target Type** (`Binary, Integer, Floating Point, etc.`): The result of the conversion.

#### Additional Information

In the instruction functional box, you can specify the source data type and target data type for conversion.

---

### DELETE

**Type:** INSTRUCTION
**Category:** String Operations
**Difficulty Level:** Beginner
**Tags:** delete, string, string-operations

#### Description

Function to delete specific characters from a string, applicable in scenarios where there is a need to remove specified positions and quantities of characters from a string.

#### Parameters

**Inputs:**

- **IN** (`STRING`): WSTRING, D, L or constant, string.
- **L** (`BYTE`): INT, SINT, USINT, I, Q, M, D, L or constant, number of characters to delete.
- **P** (`BYTE`): INT, SINT, USINT, I, Q, M, D, L or constant, position of the first character to delete.

#### Example Code

```scl
#result := MID(IN := #inputSTRING, L := #extractNumber, P := #startingPoint);
```

#### Additional Information

The DELETE instruction, when deleting, will return an empty string or the original string if P or L is negative or exceeds the string length.

---

### FLOOR

**Type:** INSTRUCTION
**Category:** String Operations
**Difficulty Level:** Beginner
**Tags:** floor, string-operations, value

#### Description

The function rounds down a floating-point number to the nearest smaller integer, applicable in scenarios where it is necessary to convert floating-point values to the nearest smaller integer.

#### Parameters

**Inputs:**

- **expression** (`float`): Input value.

#### Example Code

```scl
FLOOR(#inputValue);
```

#### Additional Information

The function value can be equal to or less than the input value.

---

### HTA

**Type:** INSTRUCTION
**Category:** String Operations
**Difficulty Level:** Beginner
**Tags:** data, hta, read, string, string-operations

#### Description

The function converts hexadecimal numbers into their corresponding ASCII strings, which can be useful in scenarios where hexadecimal data stored in a variable needs to be converted into a readable ASCII string.

#### Parameters

**Inputs:**

- **IN** (`Variant`): The starting address of the hexadecimal number.
- **N** (`UINT`): The number of hexadecimal bytes to be converted.

**Outputs:**

- **OUT** (`Variant`): The storage address of the result.

#### Example Code

```scl
SCL example code is provided, demonstrating how to use the SHL instruction for left shift operations.
```

#### Additional Information

The HTA instruction will produce an ASCII string whose length is twice that of the input value during conversion.

---

### INSERT

**Type:** INSTRUCTION
**Category:** String Operations
**Difficulty Level:** Beginner
**Tags:** insert, string, string-operations

#### Description

The function is to insert characters into a string and can be applied in scenarios where a new string needs to be inserted at a specified position in the original string.

#### Parameters

**Inputs:**

- **IN1** (`STRING`): WSTRING, D, L, or constant, the original string.
- **IN2** (`STRING`): WSTRING, D, L, or constant, the string to be inserted.
- **P** (`BYTE`): INT, SINT, USINT, I, Q, M, D, L, or constant, the position to insert.

#### Example Code

```scl
#result := INSERT(IN1 := #input1_STRING, IN2 := #input2_STRING, P := #startingPoint);
```

#### Additional Information

The INSERT instruction, when inserting, if P exceeds the length of IN1, append IN2 after IN1.

---

### LEFT

**Type:** INSTRUCTION
**Category:** String Operations
**Difficulty Level:** Beginner
**Tags:** left, string, string-operations

#### Description

This function extracts characters from the left side of a string and can be applied in scenarios where the left portion or the first few characters of a string are needed.

#### Parameters

**Inputs:**

- **IN** (`STRING`): WSTRING, D, L or constant, string.
- **L** (`BYTE`): INT, SINT, USINT, I, Q, M, D, L or constant, the number of characters to extract.

#### Example Code

```scl
#result := LEFT(IN := #inputSTRING, L := #extractNumber);
```

#### Additional Information

The LEFT instruction returns the entire string if L is greater than the string length during extraction.

#### Related Functions

- `CONCAT`
- `MID`
- `RIGHT`


---

### LEN

**Type:** INSTRUCTION
**Category:** String Operations
**Difficulty Level:** Beginner
**Tags:** data, len, string, string-operations

#### Description

The function is to determine the current length of a (W)STRING data type variable, applicable in scenarios where string length needs to be obtained.

#### Parameters

**Inputs:**

- **IN** (`STRING`): WSTRING, D, L or constant, string.

#### Example Code

```scl
#strLength := LEN(#inputSTRING);
```

#### Additional Information

The LEN instruction can read the actual number of characters used in a string; the length of an empty string is zero.

---

### REPLACE

**Type:** INSTRUCTION
**Category:** String Operations
**Difficulty Level:** Intermediate
**Tags:** replace, string, string-operations

#### Description

The function replaces characters in a string, applicable in scenarios where specific characters or a specified number of characters in the string need to be replaced with other characters.

#### Parameters

**Inputs:**

- **IN1** (`STRING`): WSTRING, D, L or constant, the string in which characters are to be replaced.
- **IN2** (`STRING`): WSTRING, D, L or constant, the string containing the characters to be inserted.
- **L** (`BYTE`): INT, SINT, USINT, I, Q, M, D, L or constant, the number of characters to be replaced.
- **P** (`BYTE`): INT, SINT, USINT, I, Q, M, D, L or constant, the position of the first character to be replaced.

#### Example Code

```scl
#result := REPLACE(IN1 := #input1_STRING, IN2 := #input2_STRING, L := #replaceNumber, P := #startingPoint);
```

#### Additional Information

The REPLACE instruction returns an empty string if P or L are negative or zero during replacement.

---

### RIGHT

**Type:** INSTRUCTION
**Category:** String Operations
**Difficulty Level:** Beginner
**Tags:** right, string, string-operations

#### Description

The function extracts characters from the right side of the string, applicable in scenarios where all characters after a certain position in the string need to be obtained.

#### Parameters

**Inputs:**

- **IN** (`STRING`): WSTRING, D, L or constant, string.
- **L** (`BYTE`): INT, SINT, USINT, I, Q, M, D, L or constant, number of characters to extract.

#### Example Code

```scl
#result := RIGHT(IN := #inputSTRING, L := #extractNumber);
```

#### Additional Information

The RIGHT instruction returns the entire string if L is greater than the length of the string.

#### Related Functions

- `CONCAT`
- `MID`
- `LEFT`


---

### SCALE

**Type:** INSTRUCTION
**Category:** String Operations
**Difficulty Level:** Intermediate
**Tags:** conversion, scale, string-operations

#### Description

The function converts an integer to a scaled floating-point number within physical units, applicable in scenarios requiring the conversion and scaling of integers to physical units.

#### Parameters

**Inputs:**

- **IN** (`INT`): The input value to be scaled.
- **HI_LIM** (`REAL`): Upper limit.
- **LO_LIM** (`REAL`): Lower limit.
- **BIPOLAR** (`BOOL`): Indicates whether to interpret the IN parameter as bipolar or unipolar.

**Outputs:**

- **OUT** (`REAL`): The result of the instruction.

#### Example Code

```scl
SCALE(IN := #inputValue, HI_LIM := #maxLim, LO_LIM := #minLim, BIPOLAR := #bipolarIndicator, OUT => #resultValue);
```

#### Additional Information

The values of constants K1 and K2 depend on the signal state of the BIPOLAR parameter. If the value of IN exceeds K2 or is less than K1, an error is outputted.

---

### STRG_VAL

**Type:** INSTRUCTION
**Category:** String Operations
**Difficulty Level:** Intermediate
**Tags:** string, string-operations, val

#### Description

The function converts a string into an integer or floating-point number, applicable for converting text-formatted numbers into numeric types that can be used for calculations.

#### Parameters

**Inputs:**

- **IN** (`STRING`): WSTRING, the numeric string to be converted.
- **FORMAT** (`WORD`): The input format of the characters.
- **P** (`UINT`): Reference to the first character to be converted.

**Outputs:**

- **OUT** (`USINT`): SINT, UINT, INT, UDINT, DINT, REAL, LREAL, the conversion result.

#### Example Code

```scl
STRG_VAL(IN := #inputSTRING,FORMAT := #resultSformat,P := #pointerSTRG,OUT=>#outputVAL);
```

#### Additional Information

Valid characters for conversion include the digits '0' to '9', decimal points, decimal separators, scientific notation 'E' and 'e', as well as the plus and minus sign characters. If any invalid character is encountered, the conversion process will be aborted.

---

### S_MOVE

**Type:** INSTRUCTION
**Category:** String Operations
**Difficulty Level:** Beginner
**Tags:** data, move, parameter, string, string-operations, write

#### Description

The function writes the string content from parameter IN to the data area specified by parameter OUT, applicable for scenarios where the content of one string needs to be copied to another string.

#### Parameters

**Inputs:**

- **IN** (`STRING`): WSTRING, the source string.

**Outputs:**

- **OUT** (`STRING`): WSTRING, the target string.

#### Example Code

```scl
SCL example code is provided, showing how to use the SHL instruction for left shift operations.
```

#### Additional Information

To copy variables of data type ARRAY, you can use the instructions 'MOVE_BLK' and 'UMOVE_BLK'.

---

### CTUD

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Advanced
**Tags:** counter, ctud, instruction, parameter, signal, state, timer, timer-delay, value

#### Description

Function that uses the "Count Up/Down" instruction to increment and decrement the counter value of the CV parameter. Depending on the state of the signals CU and CD, the value of the parameter CV will increase or decrease accordingly. It can be applied in scenarios that require counting up or down, such as a counter on a production line, countdown timers for traffic lights, etc.

#### Parameters

**Inputs:**

- **CU** (`BOOL`): Count up input.
- **CD** (`BOOL`): Count down input.
- **R** (`BOOL`): Reset input.
- **LD** (`BOOL`): Load input.
- **PV** (`INTEGER`): Preset output value for QU / When LD = 1, preset output value for CV.

**Outputs:**

- **QU** (`BOOL`): State of the count up counter.
- **QD** (`BOOL`): State of the count down counter.
- **CV** (`INTEGER, CHAR, WCHAR, DATE`): Current counter value.

#### Example Code

```scl
IEC_COUNTER_DB.CTUD(CU := Start1, CD := Start2, LD := Load, R := Reset, PV := PresetValue, QU => CU_Status, QD => CD_Status, CV => CounterValue);
```

#### Additional Information

If CU and CD both have rising edges within one program cycle, the counter value remains unchanged.

#### Related Functions

- `CTU`
- `CTD`


---

### CountOfElements

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Beginner
**Tags:** array, count, elements, timer-delay

#### Description

The function queries the number of elements in the ARRAY pointed to by the Variant pointer, applicable in scenarios that require determining array length or validating the type of the Variant variable.

#### Parameters

**Inputs:**

- **<Operand>** (`Variant`): Variant array

#### Example Code

```scl
VAR_INPUT
VariantToArray : Variant;
END_VAR

VAR_TEMP
Result : UDInt;
END_VAR
BEGIN
//other SCL code here 
#Result := CountOfElements(#VariantToArray);
```

#### Additional Information

A Variant pointer may not point to an instance and thus may not point to multiple instances or an ARRAY of multiple instances. If the Variant variable is not an ARRAY, the result will also return '0'.

---

### DCAT

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Intermediate
**Tags:** control, dcat, instruction, parameter, timer, timer-delay, timing

#### Description

The function uses the 'Discrete Control Timer Alarm' instruction to start timing from the moment the command to open or close is issued based on parameter CMD, activating the corresponding alarm after the specified time. It can be applied in scenarios requiring timed monitoring and alarms for equipment.

#### Parameters

**Inputs:**

- **CMD** (`BOOL`): Command input.
- **O_FB** (`BOOL`): Feedback input when opened.
- **C_FB** (`BOOL`): Feedback input when closed.

**Outputs:**

- **Q** (`BOOL`): Displays the status of parameter CMD.
- **OA** (`BOOL`): Alarm output when opened.
- **CA** (`BOOL`): Alarm output when closed.

#### Example Code

```scl
Provided SCL example code showing how to use the SHL instruction for left shift operation.
```

#### Additional Information

If the signal status of the command input changes before the preset time is reached, timing is reset. This instruction does not provide error messages.

---

### DEMUX

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Intermediate
**Tags:** demux, input, output, parameter, timer-delay, value

#### Description

The function is multiplexing, transferring the value of the input parameter to the selected output parameter. It can be applied in scenarios that require distributing one input value to multiple outputs based on a specified index.

#### Parameters

**Inputs:**

- **K** (`integer`): Specifies the output to which the input value (IN) should be copied.
- **IN** (`binary, integer, etc.`): Input value.

**Outputs:**

- **OUT0** (`binary, integer, etc.`): First output.
- **OUT1** (`binary, integer, etc.`): Second output.
- **OUTn** (`binary, integer, etc.`): Optional output.
- **OUTELSE** (`binary, integer, etc.`): Output where input IN's value should be copied when K > n.

#### Example Code

```scl
Provides SCL example code demonstrating how to use the DEMUX instruction for multiplexing operations.
```

#### Additional Information

Ensure that the input parameter 'IN' and all output parameters have the same data type.

---

### DRUM

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Advanced
**Tags:** bit, control, drum, operation, output, timer-delay

#### Description

Function is to execute a sequencer program, applicable for step operations based on event and time conditions. Control stepping of the program by assigning output bits and output words, as well as based on enable masks and preset time.

#### Parameters

**Inputs:**

- **RESET** (`BOOL`): Signal state '1' indicates reset state.
- **JOG** (`BOOL`): When the signal state changes from '0' to '1', this instruction will proceed to the next step.
- **DRUM_EN** (`BOOL`): Signal state '1' allows the sequencer to execute ahead based on event and time conditions.
- **LST_STEP** (`BYTE`): Maximum number of steps.
- **EVENT(i)** (`BOOL`): Event bit.

**Outputs:**

- **OUT(j)** (`BOOL`): Output bit.
- **Q** (`BOOL`): Signal state '1' indicates that the time for the last step has expired.
- **OUT_WORD** (`WORD`): Target word address where the sequencer writes output values.
- **ERR_CODE** (`WORD`): Error information.

#### Example Code

```scl
Provides SCL example code demonstrating how to use the SHL instruction for left shift operations.
```

#### Additional Information

The time consumed for each step is determined by the product of a preset time base (DTBP) and the preset step value (S_PRESET). The current step and preset step of the sequencer can be controlled through static parameters (e.g., DSP, DSC).

---

### F_TRIG

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Beginner
**Tags:** edge, falling, input, output, signal, state, timer-delay, trig

#### Description

The function detects the state change of input CLK from '1' to '0' and generates a falling edge signal in output Q, which can be applied in scenarios where detecting the falling edge of a signal is necessary for appropriate processing.

#### Parameters

**Inputs:**

- **CLK** (`BOOL`): Arrival signal to query the edge of this signal.

**Outputs:**

- **Q** (`BOOL`): Result of edge detection.

#### Example Code

```scl
VAR
F_TRIG_DB:F_TRIG;
END_VAR 
BEGIN
F_TRIG_DB(CLK := TagIn, Q => TagOut);
F_TRIG type variable F_TRIG_DB must be defined in the VAR...END_VAR area. The previous state of the variable in input CLK is stored in the variable 'F_TRIG_DB'. If a signal state change from '1' to '0' is detected for 'TagIn', then the signal state of 'TagOut' will be '1' for one cycle.
```

#### Additional Information

After the CPU starts, if the value of input 'CLK' is FALSE, then 'F_TRIG' will set the output 'Q' to TRUE and hold it for one cycle.

#### Related Functions

- `R_TRIG`


---

### GetBlockName

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Beginner
**Tags:** block, get, name, output, read, timer-delay

#### Description

The function is to read the block name, applicable for retrieving the name of a specified block, with the ability to limit the length of the output name. If the block name exceeds the specified length, the end of the name will be indicated by '...'.

#### Parameters

**Inputs:**

- **SIZE** (`DINT`): Limit on the number of characters for the RET_VAL parameter output.

**Outputs:**

- **RET_VAL** (`WSTRING`): Reads the program block name.

#### Example Code

```scl
SCL example code is provided, demonstrating how to use the SHL instruction for left shift operations.
```

#### Additional Information

The GetBlockName instruction can limit the length of the block name; if the name is truncated, it will be marked with an '...'.

---

### IMC

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Intermediate
**Tags:** bit, compare, control, imc, input, output, signal, state, timer-delay

#### Description

The function compares input bits with mask bits, comparing the signal states of up to 16 configured input bits with the corresponding mask bits and outputs the match result. It can be applied in scenarios where logical control needs to be executed based on the comparison results of input bits and mask bits.

#### Parameters

**Inputs:**

- **IN_BIT0 to IN_BIT15** (`BOOL`): Compares the input bits with the mask bits.
- **CMP_STEP** (`BYTE`): Step number for comparison using the mask.

**Outputs:**

- **OUT** (`BOOL`): Signal state '1' indicates a match has been found.
- **ERR_CODE** (`WORD`): Error information.

#### Example Code

```scl
Provides SCL example code demonstrating how to use the SHL instruction for left shift operations.
```

#### Additional Information

If a match is found during the comparison, the signal state of parameter OUT is set to '1'. Otherwise, the parameter OUT is set to '0'. If the value of parameter CMP_STEP is greater than 15, the instruction is not executed, and an error message is output in parameter ERR_CODE.

---

### MAX_LEN

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Beginner
**Tags:** input, len, output, string, timer-delay, value

#### Description

The function determines the maximum length of the input string and outputs it as a numeric value. It can be applied in scenarios where the length of a string needs to be obtained for further processing.

#### Parameters

**Inputs:**

- **IN** (`STRING`): WSTRING, string.

#### Example Code

```scl
#maxLength := MAX_LEN(IN := #inputSTRING);
```

#### Additional Information

(W)STRING data type variable includes two lengths.

---

### PEEK

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Beginner
**Tags:** bit, data, input, memory, output, peek, read, timer-delay

#### Description

The function reads a memory address from the storage area without specifying a data type, applicable in scenarios where reading memory addresses in the input, output, or bit storage areas is required.

#### Example Code

```scl
Result1 := PEEK(AREA := Area, DBNUMBER := DBNumber, BYTEOFFSET := Byte);
```

#### Additional Information

To read memory addresses in the input, output, or bit storage areas, the value of the DBNUMBER parameter must be set to '0', otherwise the instruction will be invalid.

---

### PEEK_BOOL

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Beginner
**Tags:** bit, bool, data, input, memory, output, read, timer-delay

#### Description

The function reads a storage bit from the standard memory area and can be applied to situations that require reading storage bits from input, output, or bit memory areas without specifying data types.

#### Example Code

```scl
Result := PEEK_BOOL(AREA := Area, DBNUMBER := DBNumber, BYTEOFFSET := Byte, BITOFFSET := Bit);
```

#### Additional Information

To read a storage bit from the input, output, or bit memory areas, the value of the DBNUMBER parameter must be set to '0', otherwise the instruction will be invalid.

---

### PRESET_TIMER

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Beginner
**Tags:** input, instruction, operation, timer, timer-delay

#### Description

This function sets a time for the IEC timer. If the result of the input logical operation is '1', this instruction is executed every cycle. It can be applied in scenarios where there is a need to reset or preset the timer duration.

#### Parameters

**Inputs:**

- **<Duration>** (`TIME`): The duration for which the IEC timer will run.

**Outputs:**

- **<IEC Timer>** (`IEC_TIMER, TP_TIME, TON_TIME, TOF_TIME, TONR_TIME`): The IEC timer that is set with the specified duration.

#### Example Code

```scl
IF #started = false THEN TON_DB.TON(IN := Start, PT := PresetTime, Q => Status, ET => ElapsedTime); #started := true; #preset := true END_IF; IF TON_DB.ET < T#10s AND #preset = true THEN PRESET_TIMER(PT := T#25s, TIMER := TON_DB); #preset := false; END_IF; When the variable #started is '0', execute 'power on ...'
```

#### Additional Information

If the specified IEC timer is counting when the instruction is executed, the instruction will override the current value of the specified IEC timer.

---

### RESET_TIMER

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Beginner
**Tags:** timer, timer-delay, timing

#### Description

The function resets the specified IEC timer to '0', applicable in scenarios where the IEC timer needs to be reinitialized, for example, when the current time of the timer is less than a specific threshold, necessitating a reset to restart timing.

#### Parameters

**Outputs:**

- **<IEC Timer>** (`IEC_TIMER, TP_TIME, TON_TIME, TOF_TIME, TONR_TIME`): The IEC timer to be reset.

#### Example Code

```scl
IF #started = false THEN TON_DB.TON(IN := Start, PT := PresetTime, Q => Status, ET => ElapsedTime); #started := true; END_IF; IF TON_DB.ET < T#25s THEN RESET_TIMER(TIMER := TON_DB); #started := false; END_IF; When the variable #started is '0', the 'on-delay' instruction is executed. If the elapsed time of the IEC timer 'TON_DB' is less than 25s, the 'reset timer' instruction is executed, resetting the timer stored in the background data block 'TON_DB'.
```

#### Additional Information

Reinitializing the actual value of the IEC timer while it is running may compromise the function of the IEC timer, potentially leading to inconsistencies between the program and the actual process.

---

### R_TRIG

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Beginner
**Tags:** edge, input, output, rising, signal, timer-delay, trig

#### Description

The function detects the rising edge of the input signal; when the input CLK changes from "0" to "1", a rising edge signal is generated in the output Q. It can be applied in scenarios where detecting the rising edge changes of a signal is needed.

#### Parameters

**Inputs:**

- **CLK** (`BOOL`): Edge signal to detect the transition of this signal.

**Outputs:**

- **Q** (`BOOL`): Result of edge detection.

#### Example Code

```scl
VAR
R_TRIG_DB:R_TRIG;
END_VAR 
BEGIN
R_TRIG_DB(CLK := TagIn, Q => TagOut);
The R_TRIG type variable R_TRIG_DB needs to be defined in the VAR...END_VAR area. The previous state of the variable in input CLK is stored in the "R_TRIG_DB" variable. If the signal state of "TagIn" is detected to change from "0" to "1", then the signal state in "TagOut" will be "1" for one cycle.
```

#### Related Functions

- `F_TRIG`


---

### STP

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Beginner
**Tags:** stp, timer-delay

#### Description

The function is to exit the program and set the CPU to STOP mode, applicable in scenarios that require a safe stop of the program or device.

#### Parameters

**Inputs:**

- **MODE** (`UINT`): Specifies the mode for shutting down or restarting.
- **COMMENT** (`STRING`): Specifies the reason for the restart.

#### Example Code

```scl
Provided SCL example code demonstrating how to use the SHUT_DOWN instruction to shut down or restart the system.
```

#### Additional Information

This instruction will terminate program execution; whether to switch from RUN mode to STOP mode depends on the CPU configuration.

---

### S_COMP

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Beginner
**Tags:** comp, compare, output, string, timer-delay

#### Description

The function compares the contents of two WSTRING format variables and outputs the comparison result, applicable in scenarios where string comparison is needed.

#### Parameters

**Inputs:**

- **IN1** (`STRING`): WSTRING, input variable, format is STRING / WSTRING.
- **IN2** (`STRING`): WSTRING, input variable, format is STRING / WSTRING.

**Outputs:**

- **OUT** (`BOOL`): The result of the comparison.

#### Example Code

```scl
Provided SCL example code demonstrating how to use the SHL instruction for left shift operation.
```

#### Additional Information

Characters are compared starting from the left side based on their ASCII codes. The first different character determines the comparison result.

---

### S_CONV

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Beginner
**Tags:** conv, conversion, data, input, output, timer-delay, value

#### Description

The function converts the value in the IN input into the data format specified in the OUT output, and can be applied in scenarios that require conversion between different data types.

#### Parameters

**Inputs:**

- **IN** (`CHAR`): WCHAR, USINT, UINT, UDINT, ULINT, SINT, INT, DINT, LINT, REAL, LREAL, value to be converted.

**Outputs:**

- **OUT** (`CHAR`): WCHAR, USINT, UINT, UDINT, ULINT, SINT, INT, DINT, LINT, REAL, LREAL, STRING, WSTRING, conversion result.

#### Example Code

```scl
INT_TO_STRING(#inputValueNBR);
```

#### Additional Information

The length of the resulting string after conversion depends on the value in the IN input. In SCL, the string returned after computation will overwrite the contents of the variable at the return value location.

---

### S_ODT

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Intermediate
**Tags:** control, delay, edge, odt, parameter, rising, signal, timer, timer-delay

#### Description

The function starts the preset timer upon detecting a rising edge in the signal of parameter S, acting as a delay timer. It can be applied in scenarios requiring delayed control, such as delay control in automation devices.

#### Parameters

**Inputs:**

- **T_NO** (`TIMER, INT`): The timer that has been started. The number of timers depends on the CPU.
- **S** (`BOOL`): Start input.
- **TV** (`S5TIME, WORD`): Preset time value.
- **R** (`BOOL`): Reset input.

**Outputs:**

- **Q** (`BOOL`): Status of the timer.
- **BI** (`WORD`): Current binary encoded time value.

#### Example Code

```scl
Result := S_ODT(T_NO := Timer_1, S := 1, TV := Number, R := Reset, Q => Status, BI => Value); When the signal state of 'Timer_1' changes from '0' to '1', it starts. As long as the signal state of '1' remains '1', the timer will count for the duration 'Number'.
```

---

### S_ODTS

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Intermediate
**Tags:** delay, edge, odts, parameter, rising, signal, timer, timer-delay

#### Description

The function starts the timer upon detecting a rising edge of the parameter S signal and assigns parameters for a holding contact delay timer. It can be applied in scenarios where it is necessary to detect the rising edge of a signal and start a timer.

#### Parameters

**Inputs:**

- **T_NO** (`TIMER、INT`): The timer that has been started. The number of timers depends on the CPU.
- **S** (`BOOL`): Start input.
- **TV** (`S5TIME、WORD`): Preset time value.
- **R** (`BOOL`): Reset input.

**Outputs:**

- **Q** (`BOOL`): The state of the timer.
- **BI** (`WORD`): The current binary coded time value.

#### Example Code

```scl
Result := S_ODTS(T_NO := Timer_1, S := 1, TV := Number, R := Reset, Q => Status, BI => Value); When the signal state of 'Timer_1' changes from '0' to '1', the timer starts. The run time of the timer is 'Number'. If the timer reaches the preset time, 'Status' will return the signal state '1', regardless of the state of '1'.
```

---

### S_OFFDT

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Intermediate
**Tags:** control, delay, edge, falling, offdt, parameter, signal, timer, timer-delay

#### Description

The function detects the falling edge of the signal parameter S to start the preset timer, which can be applied in scenarios requiring delay control triggered by the falling edge of the signal.

#### Parameters

**Inputs:**

- **T_NO** (`TIMER, INT`): The timer that has been started. The number of timers depends on the CPU.
- **S** (`BOOL`): Start input.
- **TV** (`S5TIME, WORD`): Preset time value.
- **R** (`BOOL`): Reset input.

**Outputs:**

- **Q** (`BOOL`): The status of the timer.
- **BI** (`WORD`): The current binary encoded time value.

#### Example Code

```scl
Result := S_OFFDT(T_NO := Timer_1, S := 1, TV := Number, R := Reset, Q => Status, BI => Value); If the state of signal '1' changes from '1' to '0', the 'Timer_1' timer will be started. The running time of the timer is 'Number'. As long as the timer is timing or '1' returns the signal state '1', the signal state of 'Status' will be '1'.
```

---

### S_PEXT

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Intermediate
**Tags:** delay, edge, parameter, pext, rising, signal, timer, timer-delay

#### Description

The function detects the rising edge of parameter S's signal and starts the timer, which stops after running for the preset time TV. It can be applied in scenarios that require detection of the rising edge of a signal and delaying for a period of time.

#### Parameters

**Inputs:**

- **T_NO** (`TIMER, INT`): The initiated timer. The number of timers depends on the CPU.
- **S** (`BOOL`): Start signal.
- **TV** (`S5TIME, WORD`): Preset time value.
- **R** (`BOOL`): Reset input.

**Outputs:**

- **Q** (`BOOL`): Timer status.
- **BI** (`WORD`): Current binary-coded time value.

#### Example Code

```scl
Result := S_PEXT(T_NO := Timer_1, S := 1, TV := Number, R := Reset, Q => Status, BI => Value); When the signal status of 'Timer_1' changes from '0' to '1', '1' starts. When the timer is running, 'Status' returns signal status '1'. When the preset time is reached, 'Status' resets to '0'.
```

---

### S_PULSE

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Intermediate
**Tags:** control, edge, parameter, pulse, signal, timer, timer-delay, timing

#### Description

The function starts a specified timer and begins timing for a preset duration when it detects a logical change of the parameter S from '0' to '1'. It can be applied in scenarios that require edge detection of signals and timing control.

#### Parameters

**Inputs:**

- **T_NO** (`TIMER, INT`): The timer that has been started. The number of timers depends on the CPU.
- **S** (`BOOL`): Start input.
- **TV** (`S5TIME, WORD`): Preset time value.
- **R** (`BOOL`): Reset input.

**Outputs:**

- **Q** (`BOOL`): Status of the timer.
- **BI** (`WORD`): Current binary-coded time value.

#### Example Code

```scl
Result := S_PULSE(T_NO := Timer_1, S := 1, TV := Number, R := Reset, Q => Status, BI => Value); When the operand '1' has a rising edge, 'Timer_1' starts. It uses the 'Number' time value for decrementing until the state of '1' returns to '1'.
```

---

### TOF

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Intermediate
**Tags:** access, edge, input, output, rising, signal, timer, timer-delay, timing, tof, value

#### Description

The function starts the output on the rising edge of the input signal and begins timing when the input signal changes to '0'. After the preset time is reached, it resets the output while also allowing access to the current timer value. This can be used in scenarios where a response to an input signal is needed, followed by an automatic reset of the output after a certain time.

#### Parameters

**Inputs:**

- **IN** (`BOOL`): Start input.
- **PT** (`TIME`): Duration of the off-delay.

**Outputs:**

- **Q** (`BOOL`): Output that resets after the time PT.
- **ET** (`TIME`): Current value of the timer.

#### Example Code

```scl
VAR
TOF_DB:TOF_TIME;
END_VAR 
BEGIN
 TOF_DB(IN := Start, PT := PresetTime, Q => Status, ET => ElapsedTime); // TOF_TIME type variable TOF_DB must be defined in VAR...END_VAR area. The 'Status' is set when the 'Start' signal rises. When 'Start' becomes '0', the preset time PT starts counting. After the time ends, 'Status' resets. The current timer value is stored in 'ElapsedTime.'
```

#### Additional Information

Each call to the 'off-delay' instruction must be assigned to an IEC timer that stores instance data.

#### Related Functions

- `TON`
- `TP`


---

### TON

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Intermediate
**Tags:** delay, edge, input, output, parameter, rising, signal, timer, timer-delay, ton

#### Description

The function of 'on-delay' can be applied in scenarios where a timer is started on the rising edge of an input signal, and an output parameter is set after the specified delay time.

#### Parameters

**Inputs:**

- **IN** (`BOOL`): Start input.
- **PT** (`TIME`): Duration of the on-delay.

**Outputs:**

- **Q** (`BOOL`): The output that remains set when the timer PT time has expired.
- **ET** (`TIME`): The current value of the timer.

#### Example Code

```scl
VAR
TON_DB:TON_TIME;
END_VAR 
BEGIN
 TON_DB(IN := Start, PT := PresetTime, Q => Status, ET => ElapsedTime); 
You need to define a variable TON_DB of type TON_TIME in the VAR...END_VAR area. When the 'Start' signal rises, the PT preset time starts counting. After the time period expires, 'Status' is set to '1'. As long as 'Start' is '1', 'Status' remains set. The current time value is stored in 'ElapsedTime'.
```

#### Additional Information

Each time the 'on-delay' instruction is called, it must be assigned to an IEC timer that stores instance data.

#### Related Functions

- `TOF`
- `TP`
- `TONR`


---

### TONR

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Intermediate
**Tags:** accumulate, input, signal, state, timer-delay, tonr, value

#### Description

This function uses a time accumulator to accumulate time values over a specified period; as long as the state of the start input signal is '1', time accumulation will occur. It can be used in scenarios where recording of accumulated time values is needed.

#### Parameters

**Inputs:**

- **IN** (`BOOL`): Start input.
- **R** (`BOOL`): Reset parameters ET and Q.
- **PT** (`TIME`): Maximum duration for time recording.

**Outputs:**

- **Q** (`BOOL`): Operand that remains set when the time within the timer PT has expired.
- **ET** (`TIME`): Accumulated time.

#### Example Code

```scl
VAR
TONR_DB:TONR_TIME;
END_VAR 
BEGIN
TONR_DB(IN := Start, R := Reset, PT := PresetTime, Q => Status, ET => Time);  You need to define the variable TONR_DB of type TONR_TIME in the VAR...END_VAR area. When the 'Start' signal rises, the PT preset time begins to count. The accumulated time value will be stored in 'Time'. When the specified time value of PT is reached, 'Status' is set to '1'.
```

#### Additional Information

Each time the 'time accumulator' instruction is called, an IEC timer must be allocated to store instance data.

#### Related Functions

- `TON`
- `TP`


---

### TP

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Intermediate
**Tags:** control, edge, input, output, pulse, rising, signal, timer, timer-delay, value

#### Description

The function generates a pulse with a duration of PT based on the rising edge of the input signal IN, setting output Q to 1 until PT time elapses and automatically resets. It also monitors the current timer value ET. This can be applied in scenarios where control of specific time pulse signals is needed.

#### Parameters

**Inputs:**

- **IN** (`BOOL`): Start input.
- **PT** (`TIME`): Duration of the pulse.

**Outputs:**

- **Q** (`BOOL`): The output remains set for the duration of PT.
- **ET** (`TIME`): The current value of the timer.

#### Example Code

```scl
VAR
TP_DB:TP_TIME;
END_VAR 
BEGIN
 TP_DB(IN := Start, PT := PresetTime, Q => Status, ET => ElapsedTime); The variable TP_DB of type TP_TIME needs to be defined in the VAR...END_VAR area. When the 'Start' signal rises, the PT preset time starts timing, and 'Status' is set to '1'. The current time value is stored in 'ElapsedTime'.
```

#### Additional Information

Each time the 'Generate Pulse' instruction is called, an IEC timer is allocated to store instance data.

#### Related Functions

- `TON`
- `TOF`
- `TONR`


---

### T_COMP

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Beginner
**Tags:** comp, compare, data, timer, timer-delay

#### Description

This function compares the contents of two variables of data type 'timer' or 'date and time', applicable in scenarios requiring comparison of two time or date data to obtain comparison results.

#### Parameters

**Inputs:**

- **IN1** (`DATE`): TIME, LTIME, TOD, LTOD, DT, LDT, DTL, S5Time, the first value to be compared.
- **IN2** (`DATE`): TIME, LTIME, TOD, LTOD, DT, LDT, DTL, S5Time, the second value to be compared.

**Outputs:**

- **OUT** (`BOOL`): Return value.

#### Example Code

```scl
Provided SCL example code demonstrating how to use the SHL instruction for left shift operations.
```

#### Additional Information

To make a comparison, the length and format of the data types must be the same. The result of the comparison will be output in the OUT parameter as a return value.

---

### T_CONV

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Beginner
**Tags:** conv, data, input, output, parameter, timer-delay, value

#### Description

This function converts the data type of the IN input parameter to the data type on the OUT output, applicable in scenarios where it is necessary to convert data values between different data types.

#### Parameters

**Inputs:**

- **IN** (`Integer, TIME, Date and Time*`): The value to be converted.

#### Example Code

```scl
DT_TO_LTOD(inputTime);
```

#### Additional Information

If the input and output parameters have the same data type, this instruction will copy the corresponding value.

---

### VAL_STRG

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Intermediate
**Tags:** bit, control, output, strg, string, timer-delay, value

#### Description

This function converts numeric values to strings. It can be applied in scenarios that require converting SINT, UINT, INT, UDINT, DINT, REAL, LREAL types of numbers into strings, while controlling character bit count, decimal places, and output format.

#### Parameters

**Inputs:**

- **IN** (`USINT`): The value to be converted, which can be SINT, UINT, INT, UDINT, DINT, REAL, LREAL.
- **SIZE** (`USINT`): Number of character bits.
- **PREC** (`USINT`): Number of decimal places.
- **FORMAT** (`WORD`): Output format of the characters.

**Outputs:**

- **OUT** (`STRING`): WSTRING, the conversion result.

#### Example Code

```scl
VAL_STRG(IN := #inputVAL, SIZE := #sizeSTRG, PREC := #precVAL, FORMAT := #resultV2Sformat, P := #pointer2STRG, OUT => #outputSTRING);
```

#### Additional Information

Invalid characters will interrupt the conversion process.

---

### VariantPut

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Beginner
**Tags:** data, parameter, put, timer-delay, value, variant, write

#### Description

The function writes the value of the SRC parameter variable into the storage area of the DST parameter pointed to by the Variant. It can be used in scenarios where a variable of a known data type needs to be assigned to a Variant variable.

#### Parameters

**Inputs:**

- **SRC** (`Bit string, integer, floating point, timer, date time, string, ARRAY element, PLC data type`): The variable to be written
- **DST** (`Variant`): Destination at which to write data

#### Example Code

```scl

VAR_IN_OUT
VariantVal : Variant;
END_VAR

VAR_TEMP
tempVal : Int;
END_VAR
BEGIN
//other scl code here 
IF TypeOf(#tempVal) = TypeOf(#VariantVal) THEN 
VariantPut(SRC := #tempVal, DST := #VariantVal);
END_IF;
```

#### Additional Information

The data type of the SRC parameter variable must match the data type pointed to by the Variant.

---

### WAIT

**Type:** INSTRUCTION
**Category:** Timer & Delay
**Difficulty Level:** Beginner
**Tags:** delay, timer-delay, wait

#### Description

The function is used to configure the delay time, pausing program execution. It can be applied to scenarios where a temporary stop of program execution is needed to provide a waiting period for a specific process.

#### Parameters

**Inputs:**

- **WT** (`INT`): The delay time is measured in microseconds.

#### Example Code

```scl
Provides SCL example code that demonstrates how to use the INIT_RD instruction to reset all retained data.
```

#### Additional Information

The configurable delay can range from -32768 to 32767 microseconds, and the shortest delay time depends on the CPU and the execution time of the instruction.

---
