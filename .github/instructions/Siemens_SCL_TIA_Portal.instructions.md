---
description: "Guidelines for writing Siemens SCL code for TIA Portal"
applyTo: "**/*.scl, **/*.udt"
---

# Siemens SCL TIA Portal Code Generation Guidelines

## Naming Conventions

1. **Variables (non temporary)**: Use PascalCase for variable names outside of functions, function blocks (e.g., `MotorSpeed`, `TemperatureThreshold`). If variables are declared inside a function, function block, use snake*case with prefix('*')(e.g., `_motor_speed`, `_temperature_threshold`).
2. **Constants**: Use UPPER*SNAKE_CASE for constants (e.g., `MAX_PRESSURE`, `DEFAULT_TIMEOUT`). If constants are declared inside a function, function block, use add prefix '*' (e.g., `_MAX_PRESSURE`, `_DEFAULT_TIMEOUT`).
3. **Functions**: Use PascalCase for function names (e.g., `CalculateArea`, `GetSensorData`).
4. **Function Blocks**: Use 'FB\_' prefix followed by PascalCase for function block
   names (e.g., `FB_MotorControl`, `FB_TemperatureMonitor`).
5. **In/Out/In_Out Variables**: Use 'i', 'o', 'io' prefixes respectively followed by PascalCase for input, output, and in_out variables in functions and function blocks (e.g., `iSensorValue`, `oActuatorState`, `ioConfigurationData`).
6. **Arrays**: Use plural nouns for array names (e.g., `SensorValues`, `ActuatorStates`).
7. **Booleans**: Use 'Is', 'Has', 'Can' prefixes for boolean variables (e.g., `IsActive`, `HasError`, `CanStart`). Use 'Is' (for indicate state) / 'Has' ( represent the existence of a relationship or a feature )/ 'Should' (for expected behavior )/ 'Can' ( indicate an ability or permission to perform an action) prefix for booleans (e.g., IsRunning, HasError, ShouldStart, CanProceed)
8. **Temporary Variables**: Use '_t_' prefix followed by snake_case for temporary variables (e.g., `_t_temp_result`, `_t_temp_index`).
9. **Global Variables**: Use 'Glb\_' prefix followed by PascalCase for global variables (e.g., `Glb_SystemStatus`, `Glb_ErrorCode`).
10. Use meaningful names avoiding abbreviations unless widely recognized (e.g., use `TemperatureThreshold` instead of `TempThresh`).
11. Limit name length to 30 characters for readability
12. Identifiers will not differ by: Only a mixture of case, The presence/absence of the underscore character, The interchange of the letter ‘O’, with the number ‘0’ or the letter ‘D’, The interchange of the letter ‘I’, with the number ‘1’ or the letter ‘l’, The interchange of the letter ‘S’ with the number ‘5’, The interchange of the letter ‘Z’ with the number 2, The interchange of the letter ‘n’ with the letter ‘h’. If this occurs if you use PascalCase with underscores between words for better readability.
13. For instance names of function blocks in function blocks, use prefix '\_'(e.g., `_MotorControl1`)
14. **Data Blocks**: Add prefix with `DB_` (e.g., `DB_MotorData`)
15. **User Defined Types**: Add prefix with `T_` (e.g., `T_MotorType`)
16. Use descriptive names reflecting purpose (e.g., `CalculateTorque`, `MotorStatus`)
17. Use verbs for functions (e.g., `StartMotor`, `StopProcess`)
18. Add prefix "Cfg\_" for configuration related variables (after other prefix) (e.g., `Cfg_MaxSpeed`, `iCfg_Timeout`)
19. For state machines, use STATE\_ prefix for states (e.g., `STATE_IDLE`, `STATE_RUNNING`)
20. For rising/falling edge detection variables, use 'RisingEdge'/'FallingEdge' prefix (after main prefix if exists) (e.g., `_t_RisingEdge_Start`, `_t_FallingEdge_Stop`, `_RisingEdge_Sensor`, `_FallingEdge_Alarm`)
21. For variables storing previous states, use "Prev" suffix (e.g., `MotorSpeedPrev`, `IsRunningPrev`)
22. **(Instances of Function Blocks)**: Use '\_' prefix followed by PascalCase for instances of function blocks (e.g., `_MotorControl`, `_TemperatureMonitor`).
23. Use one abbreviation per identifier only in the table below.

| Abbrev. | Type            |
| ------- | --------------- |
| Min     | Minimum         |
| Max     | Maximum         |
| Lim     | Limit           |
| Current | Actual, Current |
| Next    | Next value      |
| Prev    | Previous value  |
| Avg     | Average         |
| Sum     | Total sum       |
| Diff    | Difference      |
| Cnt     | Count           |
| Len     | Length          |
| Pos     | Position        |

| Sim | Simulated |
| Dir | Direction |
| Err | Error |
| Msg | Message |
| Cfg | Configuration |
| Init | Initialization |
| Index | Index |
| Warn | Warning |
| Cmd | Command |
| Addr | Address |

## Coding Standards

- Use only SCL instructions available for Siemens S7-1500 PLCs in TIA Portal
- Use only valid SCL syntax
- Avoid unused variables
- Ensure code is compatible with Siemens S7-1500 and S7-1200 PLCs
- Write only code fulfilling the functional/behavioral requirements clearly and efficiently always checking with the user about the requirements before writing code
- Follow modular design principles; break complex logic into smaller, manageable functions and function blocks
- Prefer use Siemens LGF library functions for common tasks
- Prefer IEC standard timers and counters over S7 specific types for portability
- Optimize data block access by setting `S7_Optimized_Access := 'TRUE'
- Prefer use temporary variables (VAR_TEMP) DINT data type for loop counters
- Prefer use variable datatype DINT for state machines
- Limit STRING/WSTRING lengths to what is necessary using constants to save memory
- Avoid deep nesting of control structures; use early exits where possible
- Avoid deep nesting of if statements; use CASE statements for multiple branches
- Prefer use of functions for reusable logic
- Prefer use of function blocks for encapsulating complex behavior
- Prefer use of data blocks for structured data storage
- Prefer use of user-defined types for complex data structures
- Prefer use state machines for complex process control
- **Handle edge cases** - Check array bounds, validate inputs, handle errors
- Test thoroughly - Verify edge conditions nd error scenarios
- Always refer to Siemens official documentation for latest updates and best practices
- always remember to consider the scan cycle time and avoid long blocking operations; use state machines for complex sequences
- always keep in mind that PLC executes code cyclically in PLC scan cycles.
- limit the use of global variables; prefer passing parameters to functions and function blocks
- prefer use of constants for fixed values instead of magic numbers
- prefer use of Siemens Named value data types (NVT) (it is like enum) for discrete states instead of raw integers
- prefer use of arrays and structures for related data instead of multiple individual variables
- always initialize variables to avoid undefined states
- avoid premature optimization; focus on clarity first, then optimize bottlenecks
- WRITE code easily understandable by others, easily maintainable, easy to online debug and well documented
- prefer modular design; break complex logic into smaller, manageable functions and function blocks
- prefer use of standard libraries and tested code snippets where possible
- for rising/falling edge detection, prefer use compare with previous state stored in a VAR variable
- prefer use of structured programming techniques; avoid spaghetti code
- prefer use of meaningful error handling and reporting mechanisms
- for large UDT structures, prefer use io_out parameters with reference passing (VAR_IN_OUT) to avoid large memory copies for function blocks
- prefer use of symbolic names for hardware addresses instead of hardcoded values
- reduce Nesting With a Return Early strategy: Instead of nesting multiple IF statements, check for error conditions or special cases at the beginning of the function and return early. This flattens the code structure and improves readability(invert the conditions and use guard clauses to handle exceptional cases upfront. This reduces the overall nesting level and makes the main logic more prominent).
- avoid using GOTO statements as they can lead to spaghetti code and make the program flow hard to follow
- when using loops, ensure there is a clear exit condition to prevent infinite loops
- when using timers and counters, ensure they are properly initialized and reset as needed
- when using timers keep in mind their starting behavior - starts timing on rising edge of IN
- prefer use of descriptive names for states in state machines instead of generic names like STATE_1, STATE_2

## Documentation

- Use comments to explain complex logic
- Document function and function block interfaces with input/output descriptions
- Maintain a changelog for significant code changes
- Use version control for code management
- Comment why is done, not what is done; the code itself should be self-explanatory for the "what"
- in function blocks, function place REGION "DESCRIPTION" with brief description of the function block purpose and documentation (input/output parameters description, logical behavior, etc.)
- Use consistent indentation and formatting for readability
- UPDATE comments when code changes to keep documentation accurate

## Code Structure Template

```scl
FUNCTION_BLOCK "FB_Syntax"
TITLE = BLOCK_TITLE
{ S7_Optimized_Access := 'TRUE' }
AUTHOR : 'AUTHOR_NAME'
FAMILY : 'FAMILY_NAME'
NAME : USER_DEFINED_ID
VERSION : 0.1
//BLOCK_COMMENT
   VAR_INPUT
      i_Variable1 : Bool;   // Comment for input variable 1
      i_Variable2 : Bool;   // Comment for input variable 2
   END_VAR

   VAR_OUTPUT
      o_Variable : Bool; // Comment for output variable
   END_VAR

   VAR_IN_OUT
      io_Variable1 : Bool; // Comment for in-out variable 1
      io_Variable2 { ExternalWritable := 'False'} : Bool; // Comment for in-out variable 2 - not externally writable
      io_Variable3 { ExternalVisible := 'False'} : Bool; // Comment for in-out variable 3 - not externally visible
   END_VAR

   VAR
      _variable1 : Bool; // Comment for internal variable 1
      _variable2 : Bool; // Comment for internal variable 2
   END_VAR
   VAR RETAIN
      _variable3 : Word := 16#1; // Comment for internal retain variable 3 with initial value
   END_VAR
   VAR DB_SPECIFIC
      _variable4 : Word := 16#2; // Comment for internal DB specific ("Set In DB" options in TIA Portal for variable) variable 4 with initial value
   END_VAR
   VAR RETAIN
      _variable5 { S7_SetPoint := 'True'} : Word := 16#3; // Comment for internal retain variable 5 with "SetPoint" option in TIA Portal and initial value
   END_VAR


   VAR_TEMP
      _t_temp_variable1 : Byte; // Comment for temporary variable 1
   END_VAR

   VAR CONSTANT
      _CONSTANT_1 : Byte := 16#7; // Comment for constant variable 1 with initial value
      _CONSTANT_2 : Byte := 16#8; // Comment for constant variable 2
   END_VAR


BEGIN



	REGION Initialize
	    // Statement section REGION

	END_REGION

END_FUNCTION_BLOCK
```

Below template for Function without returned value ("Void") in file \*.scl

```scl
FUNCTION "Function_Syntax" : Void
TITLE = BLOCK_TITLE
{ S7_Optimized_Access := 'TRUE' }
AUTHOR : 'AUTHOR_NAME'
FAMILY : 'FAMILY_NAME'
NAME : USER_DEFINED_ID
VERSION : 0.1
//BLOCK_COMMENT
   VAR_INPUT
      i_Variable1 : Bool;   // Comment for input variable 1
      i_Variable2 : Bool;   // Comment for input variable 2
   END_VAR

   VAR_OUTPUT
      o_Variable2 : Bool; // Comment for output variable 2
   END_VAR

   VAR_IN_OUT
      io_Variable : Bool; // Comment for in-out variable
   END_VAR

   VAR_TEMP
      _t_temp_variable3 : Bool := False; // Comment for temporary variable 3 with initial value
   END_VAR

   VAR CONSTANT
      _CONSTANT_1 : INT := 10; // Comment for constant variable 1 with initial value
   END_VAR


BEGIN
    // Statement section
END_FUNCTION
```

Below template for Function with returned byte value ("Byte") in file \*.scl
Replace data type "Byte" with other data type if needed.

```scl
FUNCTION "Function_Syntax_ReturnedVal" : Byte
TITLE = BLOCK_TITLE
{ S7_Optimized_Access := 'TRUE' }
AUTHOR : 'AUTHOR_NAME'
FAMILY : 'FAMILY_NAME'
NAME : USER_DEFINED_ID
VERSION : 0.1
//BLOCK_COMMENT
   VAR_INPUT
      i_Variable1 : Bool;   // Comment for input variable 1
      i_Variable2 : Bool;   // Comment for input variable 2
   END_VAR

   VAR_OUTPUT
      o_Variable2 : Bool; // Comment for output variable 2
   END_VAR

   VAR_IN_OUT
      io_Variable : Bool; // Comment for in-out variable
   END_VAR

   VAR_TEMP
      _t_temp_variable3 : Bool := False; // Comment for temporary variable 3 with initial value
   END_VAR

   VAR CONSTANT
      _CONSTANT_1 : INT := 10; // Comment for constant variable 1 with initial value
   END_VAR

BEGIN
	REGION RETURN value
	    #Function_Syntax_ReturnedVal := 1;
	END_REGION

END_FUNCTION
```

Below template for Data Block in file \*.scl for not retained data block with optimized access

```scl
DATA_BLOCK "DB_Syntax"
TITLE = BLOCK_TITLE
{ S7_Optimized_Access := 'TRUE' }
AUTHOR : 'AUTHOR_NAME'
FAMILY : 'FAMILY_NAME'
NAME : USER_DEFINED_ID
VERSION : 0.1
NON_RETAIN
//BLOCK_COMMENT
   VAR
      b1 : Bool; // Comment for variable 1
      w1 : Byte; // Comment for variable 2
      w2 : Byte; // Comment for variable 3
      w3 { ExternalAccessible := 'False'; ExternalVisible := 'False'; ExternalWritable := 'False'} : Byte; // Comment for variable 4 - not externally accessible, visible or writable
      w4 { ExternalVisible := 'False'} : Byte; // Comment for variable 5 - not externally visible
      w5 { ExternalWritable := 'False'} : Byte; // Comment for variable 6 - not externally writable
      w6 { ExternalVisible := 'False'} : Byte; // Comment for variable 7 - not externally visible
      w7 { ExternalWritable := 'False'} : Byte; //
      w8 { S7_SetPoint := 'True'} : Byte; // Comment for variable 8 - with "SetPoint" option
   END_VAR
   VAR RETAIN
      w9 : Byte; // Comment for retained variable 9
   END_VAR


BEGIN
   w1 := 16#1; // Initialize variable 1
   w2 := 16#2; // Initialize variable 2
   w3 := 16#3; // Initialize variable 3
   w4 := 16#4;
   w5 := 16#5;
   w6 := 16#6;
   w7 := 16#7;
   w8 := 16#8;
   w9 := 16#09;

END_DATA_BLOCK
```

Below template for User Defined Type in file \*.udt

```udt
TYPE "T_DataType"
TITLE = DATATYPE_NAME
VERSION : 0.1
//DATATYPE_COMMENT
   STRUCT
      variable1 : Bool; // Comment for variable 1
      variable2 { S7_SetPoint := 'True'} : Byte := 16#1; // Comment for variable 2 - with "SetPoint" option and initial value
      variable3 { ExternalAccessible := 'False'; ExternalVisible := 'False'; ExternalWritable := 'False'} : Byte := 16#2; // Comment for variable 3 - not externally accessible, visible or writable with initial value
      variable4 { ExternalWritable := 'False'} : Byte := 16#3; // Comment for variable 4 - not externally writable with initial value
      variable5 { ExternalVisible := 'False'} : Byte := 16#4; // Comment for variable 5 - not externally visible with initial value
   END_STRUCT;

END_TYPE

```

In the above template, replace the placeholders
where BLOCK_TITLE, AUTHOR_NAME, FAMILY_NAME, USER_DEFINED_ID, BLOCK_COMMENT, DATATYPE_NAME, DATATYPE_COMMENT are to be replaced with actual values.
BLOCK_TITLE - brief title of the function block - 125 characters max
AUTHOR_NAME - name of the author of the function block - 125 characters max
FAMILY_NAME - family name of the function block - 125 characters max
USER_DEFINED_ID - user defined unique identifier of the function block appeared in block header - 125 characters max
BLOCK_COMMENT - brief description of the function block purpose and functionality
VERSION - version of the function block in format major.minor - max 99.99  
DATATYPE_NAME - name of the user defined data type - 125 characters max
DATATYPE_COMMENT - brief description of the user defined data type purpose and functionality

## Available builtin instructions for S7-1500 PLC by Category

### Edge Detection

R_TRIG, F_TRIG

### Timers

**IEC Timers:** TP, TON, TOF, TONR, RESET_TIMER, PRESET_TIMER
**S7 Timers:** S_PULSE, S_PEXT, S_ODT, S_ODTS, S_OFFDT, WAIT

### Counters

**IEC Counters:** CTU, CTD, CTUD
**S7 Counters:** S_CU, S_CD, S_CUD

### Type Checking & Variants

TypeOf, TypeOfElements, TypeOfDB, IS_ARRAY, VariantGet, VariantPut, Variant_TO_DB_ANY, DB_ANY_TO_Variant, CountOfElements, REF

### Mathematical

ABS, MIN, MAX, LIMIT, SQR, SQRT, LN, EXP, FRAC

### Trigonometric

SIN, COS, TAN, ASIN, ACOS, ATAN

### Data Conversion

CONVERT, ROUND, CEIL, FLOOR, TRUNC, SCALE_X, NORM_X, SCALE, UNSCALE, SWAP

### Move & Copy

MOVE_BLK, MOVE_BLK_Variant, UMOVE_BLK, FILL_BLK, UFILL_BLK, BLKMOV, UBLKMOV, FILL

### Bit Operations

BITSUM, GATHER, GATHER_BLK, SCATTER, SCATTER_BLK, SEG, BCDCPL, DECO, ENCO

### Shift & Rotate

SHL, SHR, ROL, ROR

### Memory Access

PEEK, PEEK_BOOL, POKE, POKE_BOOL, POKE_BLK, READ_LITTLE, WRITE_LITTLE, READ_BIG, WRITE_BIG

### Array Operations

ReadFromArrayDB, WriteToArrayDB, ReadFromArrayDBL, WriteToArrayDBL, LOWER_BOUND, UPPER_BOUND

### Serialization

Serialize, Deserialize

### Symbol Resolution

ResolveSymbols, MoveResolvedSymbolsToBuffer, MoveResolvedSymbolsFromBuffer, MoveToResolvedSymbol, MoveFromResolvedSymbol, GetSymbolName, GetSymbolPath, GetSymbolForReference, GetInstanceName, GetInstancePath, GetBlockName

### Selection & Multiplexing

SEL, MUX, DEMUX

### Control Flow

IF, CASE, FOR, WHILE, REPEAT, CONTINUE, EXIT, GOTO, RETURN

### String Operations

S_MOVE, S_COMP, S_CONV, LEN, MAX_LEN, CONCAT, LEFT, RIGHT, MID, DELETE, INSERT, REPLACE, FIND, STRG_VAL, VAL_STRG, Strg_TO_Chars, Chars_TO_Strg, ATH, HTA, JOIN, SPLIT

### Date & Time

T_COMP, T_CONV, T_ADD, T_SUB, T_DIFF, T_COMBINE, WR_SYS_T, RD_SYS_T, RD_LOC_T, WR_LOC_T, SET_TIMEZONE, SNC_RTCB, TIME_TCK, RTM

### Process Control

DRUM, DCAT, MCAT, IMC, SMC, LEAD_LAG

### Error Handling

GET_ERROR, GET_ERR_ID

### System Functions

INIT_RD, RUNTIME, RE_TRIGR, STP, SHUT_DOWN, ENDIS_PW

### Assignment

AssignmentAttempt

## Knowledge Base Files

Files are located in the `.github/knowledge-bases/Siemens_SCL_TIA_Portal/` directory.

### `scl_instruction_detail_all.json`

**Primary reference** - JSON object containing 159 SCL instructions. Each instruction entry includes:

- `instruction_name` - Official instruction name
- `parameters` - Input/Output/InOut parameters with data types
- `example_code` - Working SCL code examples with explanations
- `additional_info` - Important notes, limitations, firmware requirements
- `brief_description` - Concise functional summary

### `scl_keywords.jsonl`

**Extended reference** - JSONL format with additional details:

- `description` - Detailed operation explanation
- `how_to_use` - Step-by-step usage instructions
- `generated_keywords` - Search terms for finding instructions

### `siemens_LGF.jsonl`

**Extended reference** - JSONL format with Siemens LGF library functions:

- `function_name` - Official LGF function name
- `description` - Detailed operation explanation
- `how_to_use` - Step-by-step usage instructions
- `parameters` - Input/Output/InOut parameters with data types
- `example_code` - Working SCL code examples with explanations
- `generated_keywords` - Search terms for finding functions
