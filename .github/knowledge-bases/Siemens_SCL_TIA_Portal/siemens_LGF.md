# Siemens LGF Library Documentation

Documentation for Siemens Library of General Functions (LGF) blocks.

## Quick Navigation

**Categories:**
- [Array Processing](#array-processing) - Search, sort, and analyze arrays
- [Mathematical Functions](#mathematical) - Factorial, random number, regression
- [Data Type Conversion](#conversion) - String, time, and number conversions  
- [Bit/Byte Manipulation](#bit-byte) - Binary operations and bit handling
- [Time and Date Functions](#time-date) - Timers, clocks, and date handling
- [String Processing](#strings) - String comparison, search, and conversion
- [CRC Calculation](#crc) - Error detection algorithms (CRC8, CRC16, CRC32)
- [Matrix Operations](#matrix) - Matrix addition and multiplication
- [Statistical Analysis](#statistics) - Histograms and regression analysis
- [Advanced Functions](#advanced) - Ramps, buffers, and specialized operations


---

# LGF_SearchMinMax_UDInt - UDInt Array Min/Max Value and Index Searcher

**Type:** FUNCTION
**Category:** Array Processing
**Difficulty Level:** Beginner
**Tags:** array, search, min/max, udint, index, comparison

## Description

## Short description ##

This function searches, in an array of the data type UDInt, for the maximum and minimum value 
and the respective index in the array.

## Functional description ##

An array of any size is connected via the values input. The elements are then compared in turn. 
The smallest and largest values, as well as their corresponding index are output to the array.
Note If there are several identical min. or max. values, the index of the first min. or max. value is 
output.

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| minValue | UDInt | Minimum value found in the array |
| minValueIndex | DInt | Index of the minimum found value in the array |
| maxValue | UDInt | Maximum value found in the array |
| maxValueIndex | DInt | Index of the maximum found value in the array |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| values | Array[*] of UDInt | Array in whose fields the maximum and minimum are searched |


### Related Functions

- `LGF_SearchMinMax`
- `LGF_SearchMinMax_LReal`

---

# LGF_BinaryMaskCompare - Binary mask comparison

**Type:** FUNCTION
**Category:** Bit/Byte Manipulation
**Difficulty Level:** Intermediate
**Tags:** bitmask, comparison, bitwise, dword, binary, filtering

## Description

## Short description ##

This function compares two binary Values source and compare by a given mask.
Both given values are masked (input AND mask), and the results is than compared and returned.
Can be used for Word and Byte as well, by convert the passed parameter using for e.g. 
Byte_to_DWord(...).

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| source | DWord | Source value to compare |
| compare | DWord | Value to compare against |
| mask | DWord | Mask the data - bits will pass if TRUE or block if FALSE |

### Return Value

- **Type:** Bool
- **Description:** Return TRUE if masked values are equal


### Related Functions

- `LGF_BitSet`
- `LGF_BitReset`
- `LGF_IsParityEven`

---

# LGF_GetFactorial - Natural number factorial calculation

**Type:** FUNCTION
**Category:** Mathematical Functions
**Difficulty Level:** Beginner
**Tags:** factorial, mathematics, combinatorics, dint, calculation

## Description

## Short description ##

The function calculates the faculty of a natural number (ℕ!) and returns the result.
The permissible value range of the input parameter naturalNumber is between 0 and 12, as 12 
is the maximum factorial result fitting into a DInt type

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| naturalNumber | Int | Natural number (0..12) |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | FALSE: No error TRUE: An error occurred during the execution of the FB |
| status | Word | 16#0000-16#7FFF: Status of the FB 16#8000-16#FFFF: Error identification |

### Return Value

- **Type:** DInt
- **Description:** Calculated factorial

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8101 | ERR_WRONG_VALUE_RANGE |

---

# LGF_SetTime - System time, local time, and time zone setting

**Type:** FUNCTION_BLOCK
**Category:** Time and Date Functions
**Difficulty Level:** Advanced
**Tags:** time, date, system, timezone, dtl, datetime

## Description

## Short description ##

This block combines the functions of system time, local time, and set time zone.

## Functional description ##

Note The status of called commands is output in subFunctionStatus. In this case, the output value 
in status indicates which command caused the error. In this case, refer to the TIA Portal 
Online Help section for information on the respective commands.
Note The function uses internally the system function WR_LOC_T to write the local time of the CPU 
or WR_SYS_T to write the coordinated world time (UTC). Further it uses the system function 
SET_TIMEZONE to set the time zone of the PLC.
This block combines the functions of system time, local time, and set time zone.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| execute | Bool | Rising edge starts action once |
| systemTime | DTL | System time to be set in PLC |
| isLocalTime | Bool | TRUE: `systemTime` is local time, FALSE: `systemTime` is UTC time |
| timeZone | Int | Timezones HHMM [-1200.. -330.. 0.. 930.. 1200.. 1300] |
| isDaylightSavingTime | Bool | Daylight saving time changeover, TRUE: activated, FALSE: deactivated |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| done | Bool | TRUE: Commanded functionality has been completed successfully |
| busy | Bool | TRUE: FB is active and new output values can be expected |
| error | Bool | FALSE: No error / TRUE: An error occurred during the execution of the FB |
| lastSetTimeZone | String | Time zone that was set last by this block |
| status | Word | 16#0000-16#7FFF: Status of the FB / 16#8000-16#FFFF: Error identification |
| subFunctionStatus | Word | Status or return value of called FB's, FC's and system blocks |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_EXECUTION_FINISHED_NO_ERROR |
| 16#7000 | STATUS_NO_CALL |
| 16#7001 | STATUS_FIRST_CALL |
| 16#7002 | STATUS_SUBSEQUENT_CALL |
| 16#8201 | ERR_SET_TIME_LOCAL |
| 16#8202 | ERR_SET_TIME_UTC |
| 16#8203 | ERR_SET_TIMEZONE |
| 16#8600 | ERR_UNDEFINED_STATE |
| 16#8601 | ERR_WRONG_TIMEZONE |

---

# LGF_CalcCRC16 - CRC-16 Calculator

**Type:** FUNCTION
**Category:** CRC Calculation Functions
**Difficulty Level:** Advanced
**Tags:** crc, crc16, checksum, error-detection, polynomial, array

## Description

## Short description ##

The CRC calculation is used for error detection at data transmission. The result of a calculation 
returns a CRC value via the data sent. The receiver detects a faulty transmission due to the 
unequal CRC value. The function LGF_CalcCRC16 uses 16 bits as the generator polynomial 
(mask).

## Functional description ##

The function calculates the CRC value from a data stream of any size. The data stream is 
composed of the individual elements of the array at the input/output parameter array. The start 
value initValue and the generator polynomial mask can be freely selected.
The input noOfELements can be used to specify the desired number of elements for calculation, it 
applies:
𝑁𝑢𝑚𝑏𝑒𝑟𝑂𝑓𝐸𝑙𝑒𝑚𝑒𝑛𝑡𝑠 <=(𝐴𝑟𝑟𝑎𝑦𝑈𝑝𝑝𝑒𝑟𝐿𝑖𝑚𝑖𝑡 − 𝐴𝑟𝑟𝑎𝑦𝐿𝑜𝑤𝑒𝑟𝑈𝑛𝑑𝑒𝑟𝐿𝑖𝑚𝑖𝑡 + 1)
Note Various online tools are available for calculating the CRC values. The function of the block 
was tested with the following online tool, since it supports the input parameters mask
(Polynomial) and initValue (Initial Value):
http://www.sunshine2k.de/coding/javascript/crc/crc_js.html

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| initValue | Word | Start value for the calculation |
| mask | Word | Generator polynomial for the calculation |
| noOfElements | UInt | Number of elements to be used in CRC calculation |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | Error flag |
| status | Word | Status code |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| array | Array[*] of Byte | Data stream for which the CRC value will be calculated |

### Return Value

- **Type:** Word
- **Description:** Calculated CRC value

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8400 | ERR_NO_OF_ELEMENTS |


### Related Functions

- `LGF_CalcCRC8`
- `LGF_CalcCRC32Advanced`

---

# LGF_Random_UDInt - Random UDInt Number Generator

**Type:** FUNCTION
**Category:** Mathematical Functions
**Difficulty Level:** Beginner
**Tags:** random, random-number, udint, generator

## Description

## Short description ##

This function generates a random value with each call.
The random number has the data type UDInt.

## Functional description ##

Note The status of called commands is output in subFunctionStatus. In this case, the output value 
in status indicates which command caused the error. In this case, refer to the TIA Portal 
Online Help section for information on the respective commands.
The function generates random values in the range:
0 ≤ 𝑅𝑒𝑡𝑢𝑟𝑛𝑉𝑎𝑙 ≤ 4294967295.
The random value is formed from the nanoseconds of the current system time of the CPU. The 
byte order of this value is inverted and then converted to UDInt.

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | Error flag |
| status | Word | Status code |
| subfunctionStatus | Word | Status or return value of called blocks |

### Return Value

- **Type:** UDInt
- **Description:** Random number in the UDInt range

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_FINISHED_NO_ERROR |
| 16#8600 | ERR_RD_SYS_T |

---

# LGF_IecTimerOnOff - IEC_Timer implementation

**Type:** FUNCTION_BLOCK
**Category:** Time and Control Functions
**Difficulty Level:** Beginner
**Tags:** timer, ton, tof, time, iec, delay

## Description

## Short description ##

The Block implements an IEC_Timer TON and TOF

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| in | Bool | FALSE Boolean Input value |
| timeOnDelay | Time | T#0s Preset Time on Delay |
| timeOffDelay | Time | T#0s Preset Time off Delay |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| out | Bool | Delayed Input signal from input `in` |

---

# LGF_IsValueInToleranceByTime - Value Tolerance Checker by Time

**Type:** FUNCTION_BLOCK
**Category:** Monitoring Functions
**Difficulty Level:** Intermediate
**Tags:** tolerance, limit-checking, monitoring, time, range

## Description

## Short description ##

Checks if a given value is within a specified tolerance in percent of a given set point.
The block has a configurable timing for set point change hiding, lower limit and as well for upper 
limit violation hiding.

## Functional description ##

The setpoint, lowerMinimum and upperMaximum variables define a value range.
The function checks whether the value is below, in or above the value range. The outputs 
belowLowLimit, inLimits, or overHighLimit show where the value is located.
By the configuration it is possible to define whether the borders are given as absolute values or 
in percentage from set point.
The timing could be adjusted for set point changes and as well for hiding the violating of the 
lower or upper limit in case of peaks.
Figure: Principle of operation

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | Real | Value to check if in range of setpoint |
| setpoint | Real | Setpoint |
| lowerMinimum | Real | Lower limit/tolerance of the setpoint in percent or absolut |
| upperMaximum | Real | Upper limit/tolerance of the setpoint in percent or absolut |
| reset | Bool | Reset Block |
| configuration | LGF_typeIsValueInToleranceByTimeConfiguration | Module related configuration parameters |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| overHighLimit | Bool | TRUE: if value is above high limit |
| belowLowLimit | Bool | TRUE: if value is below low limit |
| inLimits | Bool | TRUE: if value is in between the limits |
| setpointChange | Bool | TRUE: when a setpoint change has been detected |
| error | Bool | Error occured |
| status | Word | Status of the function |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8401 | ERR_RANGE_LIMIT_VALUE_CALC |
| 16#8402 | ERR_SETPOINT_ABOVE_HIGH_LIMIT |
| 16#8403 | ERR_SETPOINT_BELOW_LOW_LIMIT |

## User Defined Types

### LGF_typeIsValueInToleranceByTimeConfiguration
Module related configuration parameters

### Members

| Name | Type | Description |
| :--- | :--- | :--- |
| disableLimits | Bool | TRUE: Disable the monitoring timer. Leaving the tolerance triggers immediately |
| limitsAsAbsoluteValues | Bool | TRUE: Limit given as absolut value / FALSE: Limits given as tolerance from setpoint |
| toleranceAsAbsoluteValues | Bool | TRUE: Toleranze given as absolut value / FALSE: Toleranze in percent from Setpoint |
| upperLimitMonitoringTime | Time | Monitoring time for the upper limit violation |
| lowerLimitMonitoringTime | Time | Monitoring time for the lower limit violation |
| setpointChangeMonitoringTime | Time | Monitoring time for setpoint changes |

---

# LGF_CalcCRC8 - CRC-8 Calculator

**Type:** FUNCTION
**Category:** CRC Calculation Functions
**Difficulty Level:** Advanced
**Tags:** crc, crc8, checksum, error-detection, byte, polynomial

## Description

## Short description ##

The CRC calculation is used for error detection at data transmission. The result of a calculation 
returns a CRC value via the data sent. The receiver detects a faulty transmission due to the 
unequal CRC value. The function LGF_CalcCRC8 uses 8 bits as the generator polynomial (mask).

## Functional description ##

The function calculates the CRC value from a data stream of any size. The data stream is 
composed of the individual elements of the array at the input/output parameter array. The start 
value initValue and the generator polynomial mask can be freely selected.
The input noOfELements can be used to specify the desired number of elements for calculation, it 
applies:
𝑁𝑢𝑚𝑏𝑒𝑟𝑂𝑓𝐸𝑙𝑒𝑚𝑒𝑛𝑡𝑠 <= (𝐴𝑟𝑟𝑎𝑦𝑈𝑝𝑝𝑒𝑟𝐿𝑖𝑚𝑖𝑡 − 𝐴𝑟𝑟𝑎𝑦𝐿𝑜𝑤𝑒𝑟𝑈𝑛𝑑𝑒𝑟𝐿𝑖𝑚𝑖𝑡 + 1)
Note Various online tools are available for calculating the CRC values. The function of the block 
was tested with the following online tool, since it supports the input parameters mask
(Polynomial) and initValue (Initial Value):
http://www.sunshine2k.de/coding/javascript/crc/crc_js.html

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| initValue | Byte | Start value for the calculation |
| mask | Byte | Generator polynomial for the calculation |
| noOfElements | UInt | Number of elements to be used in CRC calculation |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | Error flag |
| status | Word | Status code |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| array | Array[*] of Byte | Data stream for which the CRC value will be calculated |

### Return Value

- **Type:** Byte
- **Description:** Calculated CRC value

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8400 | ERR_NO_OF_ELEMENTS |


### Related Functions

- `LGF_CalcCRC16`
- `LGF_CalcCRC32Advanced`

---

# LGF_MatrixAddition - Matrix Addition

**Type:** FUNCTION
**Category:** Matrix Operations
**Difficulty Level:** Advanced
**Tags:** matrix, addition, lreal, array, mathematics, linear-algebra

## Description

## Short description ##

This block adds two matrices of equal size of the data type ARRAY[*,*] of LREAL.
The individual fields of the two incoming matrices are read, added and then output in the matrix 
matrixResult.
Note Note that all input and output matrices must have the same low and high limits and therefore 
the same number of columns and rows.

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | Error flag |
| status | Word | Status code |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| matrix1 | Array[*, *] of LReal | First summand (matrix) |
| matrix2 | Array[*, *] of LReal | Second summand (matrix) |
| matrixResult | Array[*, *] of LReal | Sum of the matrices |

### Return Value

- **Type:** Void
- **Description:** Void - Function has no return value

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8200 | ERR_MATR1_LOWBOUND_ROWS_MATR2_LOWBOUND_ROWS |
| 16#8201 | ERR_MATR1_LOWBOUND_ROWS_RESMATR_LOWBOUND_ROWS |
| 16#8202 | ERR_MATR1_LOWBOUND_COLUMNS_MATR2_LOWBOUND_COLUMNS |
| 16#8203 | ERR_MATR1_LOWBOUND_COLUMNS_RESMATR_LOWBOUND_COLUMNS |
| 16#8204 | ERR_MATR1_UPPBOUND_ROWS_MATR2_UPPBOUND_ROWS |
| 16#8205 | ERR_MATR1_UPPBOUND_ROWS_RESMATR_UPPBOUND_ROWS |
| 16#8206 | ERR_MATR1_UPPBOUND_COLUMNS_MATR2_UPPBOUND_COLUMNS |
| 16#8207 | ERR_MATR1_UPPBOUND_COLUMNS_RESMATR_UPPBOUND_COLUMNS |


### Related Functions

- `LGF_MatrixMultiplication`

---

# LGF_IsParityEven - Even Parity Checker for DWord

**Type:** FUNCTION
**Category:** Bit/Byte Manipulation
**Difficulty Level:** Intermediate
**Tags:** parity, bit-counting, dword, binary, even-check

## Description

## Short description ##

The function checks whether the parity of the input variable of type DWord is even. If the 
number of bits that are assigned TRUE in the sequence is even, the return value is set to TRUE.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| doubleWord | DWord | Variable for which the parity is to be determined. |

### Return Value

- **Type:** Bool
- **Description:** TRUE: When the number of bits that are assigned `TRUE` is even

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |


### Related Functions

- `LGF_BinaryMaskCompare`
- `LGF_BitSet`
- `LGF_BitReset`

---

# LGF_MatrixMultiplication - Matrix Multiplier

**Type:** FUNCTION
**Category:** Matrix Operations
**Difficulty Level:** Advanced
**Tags:** matrix, multiplication, lreal, array, mathematics, linear-algebra

## Description

## Short description ##

This function multiplies two matrices of the data type ARRAY[*,*] of LREAL.
The block multiplies two matrices of variable size. The individual elements of the two incoming 
matrices are read, multiplied, and then output in the matrixResult matrix.
Note Note that the number of columns in the first matrix must be equal to the number of rows in 
the second matrix.
The size of the initial matrix (m * n) results from the number of rows (m) of matrix1 and the 
number of columns (n) of matrix2.

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | Error flag |
| status | Word | Status code |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| matrix1 | Array[*, *] of LReal | First factor: Matrix to multiply |
| matrix2 | Array[*, *] of LReal | Second factor: Matrix to multiply |
| matrixResult | Array[*, *] of LReal | Product: The resulting matrix |

### Return Value

- **Type:** Void
- **Description:** Void - Function has no return value

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8200 | ERR_MATR1_LOWBOUND_COLUMNS_MATR2_LOWBOUND_ROWS |
| 16#8201 | ERR_MATR1_UPPBOUND_COLUMNS_MATR2_UPPBOUND_ROWS |
| 16#8202 | ERR_MATR1_LOWBOUND_ROWS_RESMATR_LOWBOUND_ROWS |
| 16#8203 | ERR_MATR2_LOWBOUND_COLUMNS_RESMATR_LOWBOUND_COLUMNS |
| 16#8204 | ERR_MATR1_UPPBOUND_ROWS_RESMATR_UPPBOUND_ROWS |
| 16#8205 | ERR_MATR2_UPPBOUND_COLUMNS_RESMATR_UPPBOUND_COLUMNS |


### Related Functions

- `LGF_MatrixAddition`

---

# LGF_DTLToString_DE - DTL to Traditional German Date String

**Type:** FUNCTION
**Category:** Data Type Conversion
**Difficulty Level:** Beginner
**Tags:** dtl, string, conversion, date, time, german

## Description

## Short description ##

This function converts a date of data type DTL into a character string of data type STRING in 
the traditional format (DD MM YYYYY…).

## Functional description ##

The block reads a date of data type DTL and converts the individual components of the date 
(year, month, day, hour…) into a character string and outputs it in traditional format (DE). The 
separator between the components of the date is variable.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| date | DTL | Date to convert as DTL tag |
| separator | Char | Separator between the components of the output date. |

### Return Value

- **Type:** String
- **Description:** Output string according to the traditional format.

---

# LGF_CompareString - String comparison operation

**Type:** FUNCTION
**Category:** String Processing
**Difficulty Level:** Beginner
**Tags:** string, comparison, sint, text

## Description

## Short description ##

Compares two strings and returns a number which indicates the result of the comparison.

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| left | String | Left / first string to compare |
| right | String | Right / second string to compare |

### Return Value

- **Type:** SInt
- **Description:** Return values: left < right := -1; left > right := 1; left == right := 0

## Status Codes

| Code | Description |
| :--- | :--- |
| 0 | RETURN_STRINGS_ARE_EQUAL Strings are equal |
| 1 | RETURN_STRING_LEFT_GREATER_THAN_RIGHT Left string is greater than right string |
| -1 | RETURN_STRING_LEFT_LESS_THAN_RIGHT Left string is less than right string |


### Related Functions

- `LGF_FindStringInCharArray`
- `LGF_ToUpper`

---

# LGF_CountArrayElements - Array element counting

**Type:** FUNCTION
**Category:** Array Processing
**Difficulty Level:** Beginner
**Tags:** array, count, variant, dint, size

## Description

## Short description ##

Count the number of array elements and returns the number of elements zero based (Array[0..x] 
of Type).

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| array | Variant | Input array to check for number of elements |

### Return Value

- **Type:** DInt
- **Description:** Number of elements in array (zero based); Returning `-1` if input variable is not type `array`; Returning `-2` if input variable is type `bool`

## Status Codes

| Code | Description |
| :--- | :--- |
| -1 | RETURN_NO_ARRAY No array is present at the input `array` |
| -2 | RETURN_NO_BOOL_ARRAYS_NOT_SUPPORTED Boolean arrays not supported |

---

# LGF_BitReset - Bit reset operation in DWORD

**Type:** FUNCTION
**Category:** Bit/Byte Manipulation
**Difficulty Level:** Beginner
**Tags:** bit, reset, dword, binary, manipulation

## Description

## Short description ##

This block resets a bit at a predefined position in a variable of the data type DWORD.
Alternatively, Word and Byte can be used instead of DWord by converting the passed
parameter with, for example, BYTE_TO_DWORD and the result with DWORD_TO_BYTE.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | DWord | Tag where the bit has to be reset |
| bitNo | USInt | Bit number to reset in "value" parameter |

### Return Value

- **Type:** DWord
- **Description:** Tag with reset bit


### Related Functions

- `LGF_BitSet`
- `LGF_BinaryMaskCompare`

---

# LGF_LIFO - LIFO Buffer Management

**Type:** FUNCTION_BLOCK
**Category:** Data Structure
**Difficulty Level:** Intermediate
**Tags:** lifo, stack, buffer, queue, variant, memory

## Description

## Short description ##

LIFO (Last-In First-Out / Stack buffer memory)
This function stores incoming data and outputs the latest/most recent not-yet-processed data.

## Functional description ##

Note The status of called commands is output in subFunctionStatus. In this case, the output value 
in status indicates which command caused the error. In this case, refer to the TIA Portal 
Online Help section for information on the respective commands.
Note I computer science the stack is also based on the LIFO principle.
With the push input, a new item is stored from the InOut parameter item in the next free position 
in the buffer. The output elementCount is incremented by one.
With the pop input, the latest / most recent item is output to the InOut parameter item, and this 
field in the buffer is replaced by the value at the parameter initialItem. The output 
elementCount is decremented by one.
The peek input allows the last entry in the buffer to be read out. The buffer is not changed.
With the reset input, the buffer is initialized and the index and counter are reset. The 
elementCount output is set to zero and the isEmpty output is set to TRUE.
With the clear input, the buffer is emptied and initialized with the initial value initialItem. Index 
and counter are reset. The elementCount output is set to zero and the isEmpty output is set to 
TRUE.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| push | Bool | Push item to the buffer |
| pop | Bool | Pop item from the buffer |
| peek | Bool | Peek item from the buffer (buffer not changed/modified) |
| reset | Bool | Initializing the buffer (reset the index and the counter) |
| clear | Bool | Clearing the buffer and initialize with the initial value initialItem (Reset index and counter). |
| initialItem | Variant | Value with which the ARRAY of the buffer is initialized (usually: 0 / default value) |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | An error occurred during the execution of the FB |
| status | Word | Status of the FB, Error identification |
| subFunctionStatus | Word | Status or return value of called FB's, FC's and system blocks |
| elementCount | DInt | Number of elements in the buffer |
| isEmpty | Bool | Buffer is empty |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| item | Variant | The entry that is either returned from the ring buffer or written into the buffer |
| buffer | Variant | The ARRAY that is used as the ring buffer. |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#7000 | STATUS_NO_CURRENT_JOBS |
| 16#8001 | ERR_BUFFER_EMPTY |
| 16#8002 | ERR_BUFFER_FULL |
| 16#8200 | ERR_NO_ARRAY |
| 16#8201 | ERR_WRONG_TYPE_ITEM |
| 16#8202 | ERR_WRONG_TYPE_INITIAL_ITEM |
| 16#8610 | ERR_CLEAR_BUFFER |
| 16#8611 | ERR_RETURN_LAST_ENTRY |
| 16#8612 | ERR_POP_REPLACE_ITEM_BY_INIT_VALUE |
| 16#8613 | ERR_WRITE_ENTRY |

---

# LGF_AstroClock - GPS-based Sunrise and Sunset Time Determination

**Type:** FUNCTION_BLOCK
**Category:** Time and Date Functions
**Difficulty Level:** Advanced
**Tags:** gps, sunrise, sunset, daylight, coordinate, time, dtl

## Description

## Short description ##

This function calculates the times of sunrise and sunset based on the local time for a specific  place on Earth. The exact position is transferred in the form of geographical GPS coordinates (longitude and latitude).

## Functional description ##

Note The status of called commands is output in subFunctionStatus. In this case, the output value 
in status indicates which command caused the error. In this case, refer to the TIA Portal 
Online Help section for information on the respective commands.
If processes must run automatically depending on the change between day and night, the 
function of an astronomical clock is required. Examples of this would be switching outdoor 
lighting on and off or opening and closing roller shutters.
If these processes are to be executed with a time delay i.e. a defined time before or after 
sunrise or sunset an offset is required in each case.
Note For precise execution of the function, it must be ensured that system time and local time of 
the SIMATIC controller are set correctly.
Based on the system time/local time of the SIMATIC controller and the set coordinates, the 
block calculates the times for sunrise and sunset. The offset times are added to the sunrise and 
sunset and output on the sunrise and sunset outputs. If the systems local time of the SIMATIC 
controller is between these values, the output isDaytime is set to the value TRUE.
Note Since the times for sunrise and sunset change daily, it is possible that the isDaytime output 
remains permanently on TRUE or FALSE over a longer period of time:
• with correspondingly large offset values
• for a place on the other side of the Arctic Circle
The input of the GPS coordinate values is checked for valid values. If there are invalid values, 
an appropriate error code is output to status.
If there is an invalid coordinate value for a formal parameter, the outputs sunrise and sunset
are set to the value DTL#1970-01-01-00:00:00.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| enable | Bool | TRUE: Activates the functionality of the FB |
| positionGps | LGF_typeGPS_DD | GPS position to calculate the time of sunrise and sunset |
| offsetSunrise | Time | Offset to sunrise (added to sunrise time, considered at `isDaytime`, negative time allowed) |
| positionGps | Time | Offset to sunset (added to sunset time, considered at `isDaytime`, negative time allowed) |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| valid | Bool | TRUE: Valid set of output values available at the FB |
| busy | Bool | TRUE: FB is active and new output values can be expected |
| error | Bool | FALSE: No error / TRUE: An error occurred during the execution of the FB |
| status | Word | 16#0000-16#7FFF: Status of the FB / 16#8000-16#FFFF: Error identification |
| subFunctionStatus | Word | Status or return value of called FB's, FC's and system blocks |
| actualLocalTime | DTL | Current time (local time) |
| sunriseTime | DTL | Sunrise time (localtime) |
| sunsetTime | DTL | Sunset time (localtime) |
| isDaytime | Bool | TRUE: If the local time of the controller is between “sunrise” and “sunset” |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_EXECUTION_FINISHED_NO_ERROR |
| 16#7000 | STATUS_NO_CALL |
| 16#7001 | STATUS_IN_OPERATION |
| 16#8204 | ERR_LATITUDE_VALUE |
| 16#8205 | ERR_LONGITUDE_VALUE |
| 16#8601 | ERR_RD_SYS_T |
| 16#8602 | ERR_RD_LOC_T |

## User Defined Types

### LGF_typeGPS_DD
Datatype for GPS Coordinates in decimal degrees. For a whole GPS Data set.

### Members

| Name | Type | Description |
| :--- | :--- | :--- |
| latitude | Real | Degrees latitude with decimal places (Unit: degree decimal), North = positive; South = negative) valid value range [-90.00000..90.00000]  |
| longitude | Real | Degrees longitude with decimal places (Unit: degree decimal), East = positive; West = negative) valid value range [-180.00000..180.00000]  |

---

# LGF_DecodeUtf8 - UTF-8 Byte Stream Decoder

**Type:** FUNCTION

## Description

## Short description ##

Decodes a UTF-8 encoded byte stream into a WString

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| byteStream | Array[*] of Byte | UTF-8 encoded byte stream |
| startPos | DInt | Position in byte stream to start decoding from |
| count | UInt | Number of character (not bytes) to decode; 0: byte stream is decoded until end |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| decodedString | WString | Decoded string |

### Return Value

- **Type:** Word
- **Description:** Status of the FC, Error identification

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#7FFD | WARN_UNSUPPORTED_CHAR |
| 16#7FFE | WARN_STREAM_EXCEEDS_MAX_LEN |
| 16#8201 | ERR_START_POS_OUTSIDE |
| 16#8202 | ERR_COUNT_EXCEEDS_BOUNDS |
| 16#8203 | ERR_COUNT_EXCEEDS_MAX_LEN |

---

# LGF_BitSet - Bit set operation in DWORD

**Type:** FUNCTION
**Category:** Bit/Byte Manipulation
**Difficulty Level:** Beginner
**Tags:** bit, set, dword, binary, manipulation

## Description

## Short description ##

This block sets a bit at a given position in a variable of the data type DWORD.
Alternatively, Word and Byte can be used instead of DWord by converting the passed
parameter with, for example, BYTE_TO_DWORD and the result with DWORD_TO_BYTE.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | DWord | Tag where the bit has to be set |
| bitNo | USInt | Bit number to set in "value" parameter |

### Return Value

- **Type:** DWord
- **Description:** Tag with the set bit


### Related Functions

- `LGF_BitReset`
- `LGF_BinaryMaskCompare`

---

# LGF_ToUpper - String Upper Case Converter

**Type:** FUNCTION
**Category:** String Processing
**Difficulty Level:** Beginner
**Tags:** string, uppercase, conversion, text

## Description

## Short description ##

This function converts the lowercase letters of a string into their capital equivalents

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| In | String | String input |

### Return Value

- **Type:** String
- **Description:** Resulting string, after the conversion


### Related Functions

- `LGF_CompareString`
- `LGF_FindStringInCharArray`

---

# LGF_RampCI - Ramp Function Generator

**Type:** FUNCTION_BLOCK
**Category:** Advanced Functions
**Difficulty Level:** Advanced
**Tags:** ramp, interpolation, curve, lreal, time, control

## Description

## Short description ##

The function generates a speed curve based on an interpolation point table. Linear interpolation 
occurs between the points within the prescribed time.

## Functional description ##

Note The status of called commands is output in subFunctionStatus. In this case, the output value 
in status indicates which command caused the error. In this case, refer to the TIA Portal 
Online Help section for information on the respective commands.
Global data
Together with the block, you automatically receive the PLC data type LGF_typeRampTimeTable, 
which is composed of the parameters outVal for the value of a base point and time for the time, 
until the next base point is reached. The declaration takes place in a one-dimensional array of 
the data type LGF_typeRampTimeTable beginning with the index 0. The array is created in a global 
data block and then passed to the module LGF_RampCI.
Principle of operation
With this block, speed curves can be executed based on parameterized interpolation points; in 
each call cycle values are output according to a schedule, and interpolation takes place 
between the interpolation points.
In each cycle the currently approached interpolation point number stepNumber, the actual 
remaining time remainTime until reaching the interpolation point, the total time totalTime, and 
the total remaining time until reaching the end of the speed curve remainTotalTime, are output. 
In addition, the output actTimeTable is set if the projected speed curve is currently being output.
The time interval of the calling cyclic interrupt OB is determined by interconnecting the calling 
cyclic interrupt OB at the input parameter callOB.
Figure: Interconnecting the cyclic interrupt OB
The following operating modes can be selected via control inputs:
• Restart
• Pre-assigning an output
• Output a speed curve
• Stop processing
• Specify processing step and processing time
• Switch-on cyclic operation+F1
• Update total time and remaining time
Restart
The output outValue is reset to 0.0 with a rising edge at the input reset. With 
enDefaultOutValue = TRUE, defaultOutValue is output at outputValue. The total time and total 
remaining time are updated and output.
Pre-assigning an output
If the speed curve should begin with a certain output value, then enDefaultOutValue must be 
TRUE. In this case the value defaultOutValue is present on the output of the timer. The internal 
processing of the speed curve continues during this time. If enDefaultOutValue changes to 
FALSE again, interpolation is performed to the currently active calibration point.
Output a speed curve
With a rising edge at the input start, the speed curve is output - as long as start is TRUE or until 
the speed curve is terminated by reaching the last interpolation point. Through a subsequent 
rising edge, the speed curve is output again. In addition, the total time is updated at each 
switch-on.
Switch-on cyclic operation
If, in addition to the input start, the input cyclicOP is also set to TRUE, the speed curve 
automatically returns to the start point after outputting the last interpolation point value and 
starts a new cycle.
There is no interpolation between the last interpolation point value and the starting point. The 
following must apply for a smooth transition: last interpolation point value = start point.
Stop speed curve
With hold = TRUE the value of the output variable (including time processing) is frozen. When 
resetting hold = FALSE, the program continues at the point of interruption or at a parameterized 
point (see “Defining the processing step and processing time”). The processing time of the 
speed curve is extended by the holding time T1*. (see Figure below).
Specify processing step and processing time
If the input parameter continue is set to TRUE for continuation while the speed curve is stopped 
(hold = TRUE), then after the input hold has been reset the interpolation point number 
contStepNbr (target interpolation point) will be approached within the time contStepTime
(interpolation). The total remaining time will be recalculated.
Updating total time and total remaining time
If values of the interpolation points are changed, the total time and the total remaining time of 
the speed curve can change. Since calculation of totalTime and remainTotalTime can 
significantly increase the processing time of the function block at many interpolation points, the 
calculation is only executed once with a rising edge on the updateTime input.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| defaultOutValue | LReal | Value for pre-assignment of the output variable |
| contStepNbr | Int | Number of the next interpolation point for continuing |
| contStepTime | Time | Remaining time to continue to the interpolation point |
| enDefaultOutValue | Bool | Assign default output value |
| start | Bool | Run down the interpolation point table |
| hold | Bool | Freeze/hold output at actual value |
| continue | Bool | Continuing |
| cyclicOP | Bool | Repeat interpolation point table cyclically |
| updateTime | Bool | Update time values |
| reset | Bool | Complete reset of function |
| callOB | OB_CYCLIC | Calling wake-alarm interrupt OB |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| outputValue | LReal | Output value |
| actTimeTable | Bool | Interpolation point table will be edited |
| stepNumber | Int | Current interpolation point number |
| remainTime | Time | Remaining time until reaching the next interpolation point |
| totalTime | Time | Total time for setpoint table |
| remainTotalTime | Time | Total remaining time |
| error | Bool | Error occurred during the execution of the FB |
| status | Word | Status of the FB |
| subfunctionStatus | Word | Status or return value of called FB's, FC's and system blocks |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| setpoints | Array[*] of LGF_typeRampTimeTable | Interpolation point table. |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_FINISHED_NO_ERROR |
| 16#7000 | STATUS_NO_CALL |
| 16#7001 | STATUS_FIRST_CALL |
| 16#7002 | STATUS_FURTHER_CALLS |
| 16#8200 | ERR_OB_UNAVAILABLE |
| 16#8201 | ERR_ARRAY_LOWER_BOUND |
| 16#8400 | ERR_QRY_CINT |

## User Defined Types

### LGF_typeRampTimeTable
Data type for setup a speed curve

### Members

| Name | Type | Description |
| :--- | :--- | :--- |
| outputValue | LReal | Setpoint Value to reach by the interpolation curve |
| time | Time | Time until the interpolation point is reached |

---

# LGF_CalcCRC32Advanced - Advanced CRC-32 Calculator

**Type:** FUNCTION
**Category:** CRC Calculation Functions
**Difficulty Level:** Advanced
**Tags:** crc, crc32, checksum, error-detection, polynomial, xor

## Description

## Short description ##

The CRC calculation is used for error detection at data transmission. The result of a calculation 
returns a CRC value via the data sent. The receiver detects a faulty transmission due to the 
unequal CRC value. The function LGF_CalcCRC32Advanced uses 32 bits as the generator 
polynomial (mask) and the parameters finalXorValue, reflectInput, and reflectResult.

## Functional description ##

The function calculates the CRC value from a data stream of any size. The data stream is 
composed of the individual elements of the array at the input/output parameter array. The start 
value initValue and the generator polynomial mask can be freely selected.
Via the Boolean input parameters reflectInput and reflectResult, you may optionally mirror 
the bits of the input data or the CRC value. An XOR operation is also performed with the CRC 
value at the end and the value finalXorValue.
The input noOfELements can be used to specify the desired number of elements for calculation, it 
applies:
𝑁𝑢𝑚𝑏𝑒𝑟𝑂𝑓𝐸𝑙𝑒𝑚𝑒𝑛𝑡𝑠 <= (𝐴𝑟𝑟𝑎𝑦𝑈𝑝𝑝𝑒𝑟𝐿𝑖𝑚𝑖𝑡 − 𝐴𝑟𝑟𝑎𝑦𝐿𝑜𝑤𝑒𝑟𝑈𝑛𝑑𝑒𝑟𝐿𝑖𝑚𝑖𝑡 + 1)
Note Various online tools are available for calculating the CRC values. The function of the block 
was tested with the following online tool, since it supports the input parameters mask
(Polynomial) and initValue (Initial Value):
http://www.sunshine2k.de/coding/javascript/crc/crc_js.html

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| initValue | DWord | Start value for the calculation |
| mask | DWord | Generator polynomial for the calculation |
| finalXorValue | DWord | Value for final XOR operation |
| reflectInput | Bool | Mirror the bits within the input byte |
| reflectResult | Bool | Mirror the order of the bits within the result |
| noOfElements | UInt | Number of elements to be used in CRC calculation |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | Error flag |
| status | Word | Status code |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| array | Array[*] of Byte | Data stream for which the CRC value will be calculated |

### Return Value

- **Type:** DWord
- **Description:** Calculated CRC value

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8400 | ERR_NO_OF_ELEMENTS |


### Related Functions

- `LGF_CalcCRC16`
- `LGF_CalcCRC8`

---

# LGF_StringToInt - String to DInt Converter

**Type:** FUNCTION
**Category:** Data Type Conversion
**Difficulty Level:** Beginner
**Tags:** string, dint, conversion, parsing

## Description

## Short description ##

This function converts a variable of data type String into a variable of data type DInt.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | String | String value to be converted to Double-Integer. Example: ‘+16927’ |

### Return Value

- **Type:** DInt
- **Description:** Converted Double-Integer value

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |


### Related Functions

- `LGF_IntToString`
- `LGF_TimeToString`

---

# LGF_IntToString - DInt to String Converter

**Type:** FUNCTION
**Category:** Data Type Conversion
**Difficulty Level:** Beginner
**Tags:** dint, string, conversion, formatting

## Description

## Short description ##

This function converts a variable of the data type DInt into a variable of the data type String.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | DInt | Double-Integer value to convert |

### Return Value

- **Type:** String
- **Description:** Converted value as string. Example: '+16927'


### Related Functions

- `LGF_StringToInt`
- `LGF_TimeToString`

---

# LGF_CountRisInDWord - DWORD rising edge counting

**Type:** FUNCTION_BLOCK
**Category:** Bit/Byte Manipulation
**Difficulty Level:** Intermediate
**Tags:** dword, rising-edge, transition, bit-counting, legacy

## Description

## Short description ##

The function analyzes a variable of the type DWORD and outputs how often a 0-1 sequence 
(rising edge) occurs in the variable.
Note LEGACY FUNCTION
Please update and use the FB with the same name LGF_CountRisInDWord in the future!
This function is no longer maintained!

## Functional description ##

In a variable of the data type DWORD, the block counts the rising edges (0-1 transitions) from 
left to right. The output countRisInDWord outputs the number of rising edges.
So that rising edges at the variable limit are also detected, the input value is copied to the static 
variable statDWordPrevCycle at the end of the evaluation and evaluated in the next cycle.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | DWord | Input Double word in which the rising edges are counted |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| numberOfEdges | Int | Number of rising edges in the DWord |

---

# LGF_SearchMinMax_LReal - LReal Array Min/Max Value and Index Searcher

**Type:** FUNCTION
**Category:** Array Processing
**Difficulty Level:** Beginner
**Tags:** array, search, min/max, lreal, floating-point, index

## Description

## Short description ##

This function searches, in an array of the data type LReal, for the maximum and minimum value 
and the respective index in the array.

## Functional description ##

An array of any size is connected via the values input. The elements are then compared in turn. 
The smallest and largest values, as well as their corresponding index are output to the array.
Note If there are several identical min. or max. values, the index of the first min. or max. value is 
output.

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| minValue | LReal | Minimum value found in the array |
| minValueIndex | DInt | Index of the minimum found value in the array |
| maxValue | LReal | Maximum value found in the array |
| maxValueIndex | DInt | Index of the maximum found value in the array |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| values | Array[*] of LReal | Array in whose fields the maximum and minimum are searched |


### Related Functions

- `LGF_SearchMinMax`
- `LGF_SearchMinMax_UDInt`

---

# LGF_TimeToString - Time to String Converter

**Type:** FUNCTION
**Category:** Data Type Conversion
**Difficulty Level:** Beginner
**Tags:** time, string, conversion, formatting, display

## Description

## Short description ##

This function converts a variable of the system data type Time into a variable of the data type 
String.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| timeValue | Time | Time value to convert Example: T#1D_3H_45M_6S |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| stringDay | String | Converted day as string |
| stringHour | String | Converted hour as string |
| stringMinute | String | Converted minute as string |
| stringSecond | String | Converted second as string |
| stringMilliSecond | String | Converted millisecond as string |

### Return Value

- **Type:** String
- **Description:** Converted time as string. Example: 1D3H45M6S0MS


### Related Functions

- `LGF_DTLToString_DE`
- `LGF_StringToInt`

---

# LGF_Histogram_DInt - Histogram Calculation Function Block for Integer Data

**Type:** FUNCTION_BLOCK
**Category:** Statistical Analysis
**Difficulty Level:** Advanced
**Tags:** histogram, dint, distribution, statistics, class, frequency

## Description

## Short description ##

The histogram shows the frequency distribution of a sample by class. A class describes a value 
interval in which the individual frequencies are added together. After specifying the number of 
classes, the class width and the respective class center are calculated. The number of classes 
is limited to 15.
The distribution is represented as a rectangle around the class mean with the class width and 
the cumulated frequency as height.
Figure: Distribution

## Functional description ##

The block sorts the transferred data and calculates the general class width using the transferred 
class count and data range. The block then counts the values that lie within a class. In order to 
draw a histogram, the block also calculates the necessary X and Y coordinates.
The elements of the passed array values are sorted in ascending order by the block. The 
LGF_Shellsort_UDInt block is used for sorting.
The number of classes can be specified using the following rule of thumb:

Formulas
The block uses the following formula to calculate the class width:

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| execute | Bool | Activation of the calculation with each positive edge. |
| numberOfClasses | UInt | Number of desired classes. |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | FALSE: No error, TRUE: An error occurred during the execution of the FB |
| status | Word | Status of the FB and error identification. |
| subFunctionStatus | Word | Status or return value of called FB's, FC's and system blocks |
| histValues | Array[0..1, 0..#CLASSES_COUNTER_UP_LIMIT] of LReal | Outputs the calculated values in a two-dimensional array. |
| axis | Array[0..3] of LReal | Specifies the axis values. |
| classWidth | LReal | Returns the calculated class width. |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| values | Array[*] of DInt | The array containing the data series that is to be used for the calculation. |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_EXECUTION_FINISHED: Execution finished without errors |
| 16#7000 | STATUS_NO_CALL: No call of FB. The block waits for activation. |
| 16#7001 | STATUS_FIRST_CALL: First call of FB after enabling |
| 16#8600 | ERR_SHELL_SORT: Error in command `LGF_ShellSort_DInt`. |
| 16#9101 | ERR_WRONG_NO_CLASSES: Incorrect number of classes. |


### Related Functions

- `LGF_Histogram_UDInt`
- `LGF_RegressionLine`

---

# LGF_MergeBitsToByte - 8-Bit to Byte Merger

**Type:** FUNCTION
**Category:** Bit/Byte Manipulation
**Difficulty Level:** Beginner
**Tags:** bit, byte, merge, boolean, binary

## Description

## Short description ##

This function merge 8 Bits / 8 Boolean variables into one Byte variable.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| bit7 | Bool | Input Bit 7 - MSB |
| bit6 | Bool | Input Bit 6 |
| bit5 | Bool | Input Bit 5 |
| bit4 | Bool | Input Bit 4 |
| bit3 | Bool | Input Bit 3 |
| bit2 | Bool | Input Bit 2 |
| bit1 | Bool | Input Bit 1 |
| bit0 | Bool | Input Bit 0 - LSB |

### Return Value

- **Type:** Byte
- **Description:** Composite Bit sequence stored as Byte variable


### Related Functions

- `LGF_BitSet`
- `LGF_BitReset`

---

# LGF_FindStringInCharArray - String Position Finder in Character Array

**Type:** FUNCTION
**Category:** String Processing
**Difficulty Level:** Intermediate
**Tags:** string, search, array, character, position, variant

## Description

## Short description ##

The function searches for a specified String within an array of characters.
Returning the position of the String in the Array, if the string is not found the return value is -1.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| searchFor | String | Text that is searched for |
| startPos | DInt | Position within the array to start search from (index zero based) |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| status | Word | Status of the FB |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| searchIn | Variant | Array of Character or Byte to search in |

### Return Value

- **Type:** DInt
- **Description:** Position (index) of the first character of the text that is searched for within the input array (index zero based). Return -1 if nothing found.

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8200 | ERR_NO_ARRAY |


### Related Functions

- `LGF_CompareString`
- `LGF_ToUpper`

---

# LGF_MergeWordsToDWord - 2-Word to DWord Merger

**Type:** FUNCTION
**Category:** Bit/Byte Manipulation
**Difficulty Level:** Beginner
**Tags:** word, dword, merge, binary, data-type

## Description

## Short description ##

This function merge 2 Word variables into one DWord variable.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| word1 | Word | Input Word 1 - MSB |
| word0 | Word | Input Word 0 - LSB |

### Return Value

- **Type:** DWord
- **Description:** Composite Word sequence stored as DWord variable

---

# LGF_IsValueInLimits - Value range limit check

**Type:** FUNCTION
**Category:** Monitoring Functions
**Difficulty Level:** Beginner
**Tags:** limit-checking, range, tolerance, lreal, validation

## Description

## Short description ##

The function checks whether a value is within a defined value range. The value range is defined 
with a lower and an upper limit.

## Functional description ##

The variables lowLimit and highLimit define a value range.
The function checks whether the value is below, in or above the value range. The outputs 
belowLowLimit, Ret_Val, or overHighLimit show where the value is located.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | LReal | Value to be checked to determine whether it is within the defined value range |
| lowLimit | LReal | Low limit where the value is checked against to be greater |
| highLimit | LReal | High limit where the value is checked against to to be less |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| overHighLimit | Bool | TRUE if the “value” is greater than the upper limit value |
| belowLowLimit | Bool | TRUE, if the “value” is less than the lower limit value |
| error | Bool | FALSE: No error TRUE: An error occurred during the execution of the FB |
| status | Word | 16#0000-16#7FFF: Status of the FB 16#8000-16#FFFF: Error identification |

### Return Value

- **Type:** Bool
- **Description:** Return: TRUE if the “value” is in the value range (range of the set point)

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8401 | ERR_RANGE_HIGH_BELOW_LOW_LIMIT |


### Related Functions

- `LGF_IsValueInToleranceByTime`

---

# LGF_ShellSort_UDInt - Shell Sort for UDInt Arrays

**Type:** FUNCTION
**Category:** Array Processing
**Difficulty Level:** Advanced
**Tags:** sort, shell-sort, udint, array, algorithm

## Description

## Short description ##

This block sorts an array of type UDInt with any number of elements (max. 1000) in ascending 
or descending order and returns the sorted version of the array in the same variable.

## Functional description ##

The block sorts according to the shell sort procedure. Note that the execution time of the block 
depends significantly on how many elements the array to be sorted has. The overview below 
shows several measured values of the block depending on the number of array elements.
Average steps needed for execution: 𝒪(𝑛 ⋅ log(𝑛)^2)
Table: Execution times of the block LGF_ShellSort…
Number of array elements S7-1212C DC/DC/DC S7-1516-3 PN/DP
100 approx. 11-16 ms approx. 1-2 ms
1000 approx. 185-205 ms approx. 10-12 ms
Note The block is executed synchronously and is not split over several PLC cycles. Thus the 
execution time has a direct effect on the PLC cycle time. Note this behavior for your project 
of the controller used and adjust the monitoring time of the controller if necessary.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| sortDirection | Bool | FALSE: Sort ascending; TRUE: Sort descending |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | An error occurred during the execution of the FB |
| status | Word | Status of the FB, Error identification |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| array | Array[*] of UDInt | Array to be sorted |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8200 | ERR_NO_ARRAY |
| 16#8201 | ERR_TOO_MANY_ELEMENTS |

---

# LGF_SearchMinMax - Array Min/Max Value and Index Searcher

**Type:** FUNCTION
**Category:** Array Processing
**Difficulty Level:** Intermediate
**Tags:** array, search, min/max, variant, generic, index

## Description

## Short description ##

This function searches, in an array of the data type DInt, for the maximum and minimum value 
and the respective index in the array.
The following data types of the array elements are supported:
Int, DInt, UInt, UDInt, USInt, SInt, and Real.

## Functional description ##

Note The status of called commands is output in subFunctionStatus. In this case, the output value 
in status indicates which command caused the error. In this case, refer to the TIA Portal 
Online Help section for information on the respective commands.
An array of any size is connected via the variableArray input. After a data type query in the 
block, the elements are copied one after the other into a variable of the appropriate type and 
compared. The smallest and largest values, as well as their corresponding index are output to 
the array.
Note The following data types of the array elements are supported:
Int, DInt, UInt, UDInt, USInt, SInt, and Real.
Note If there are several identical min. or max. values, the index of the first min. or max. value is 
output.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| variableArray | Variant | Array in whose fields the maximum and minimum are searched |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| minValue | Variant | Minimum value found in the array |
| minValueIndex | DInt | Index of the minimum found value in the array |
| maxValue | Variant | Maximum value found in the array |
| maxValueIndex | DInt | Index of the maximum found value in the array |
| error | Bool | Error flag |
| status | Word | Status code |
| subfunctionStatus | Word | Status or return value of called blocks |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8200 | ERR_NO_ARRAY |
| 16#8201 | ERR_WRONG_TYPE |
| 16#8202 | ERR_NOT_EQUAL_TYPES |
| 16#8203 | ERR_MOVE_BLK_VARIANT |


### Related Functions

- `LGF_SearchMinMax_UDInt`
- `LGF_SearchMinMax_LReal`

---

# LGF_Histogram_UDInt - Unsigned Integer Histogram Calculation Function Block

**Type:** FUNCTION_BLOCK
**Category:** Statistical Analysis
**Difficulty Level:** Advanced
**Tags:** histogram, udint, distribution, statistics, class, frequency

## Description

## Short description ##

The histogram shows the frequency distribution of a sample by class. A class describes a value 
interval in which the individual frequencies are added together. After specifying the number of 
classes, the class width and the respective class center are calculated. The number of classes 
is limited to 15.
The distribution is represented as a rectangle around the class mean with the class width and 
the cumulated frequency as height.
Figure: Distribution

## Functional description ##

The block sorts the transferred data and calculates the general class width using the transferred 
class count and data range. The block then counts the values that lie within a class. In order to 
draw a histogram, the block also calculates the necessary X and Y coordinates.
The elements of the passed array values are sorted in ascending order by the block. The 
LGF_Shellsort_UDInt block is used for sorting.
The number of classes can be specified using the following rule of thumb:

Formulas
The block uses the following formula to calculate the class width:

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| execute | Bool | Activation of the calculation with each positive edge. |
| numberOfClasses | UInt | Number of desired classes. |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | FALSE: No error, TRUE: An error occurred during the execution of the FB |
| status | Word | Status of the FB and error identification. |
| subfunctionStatus | Word | Status or return value of called FB's, FC's and system blocks |
| histValues | Array[0..1, 0..#CLASSES_COUNTER_UP_LIMIT] of LReal | Displays the relative frequency and class centers. |
| axis | Array[0..3] of LReal | Specifies the axis values. |
| classWidth | LReal | Returns the calculated class width. |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| values | Array[*] of UDInt | The array containing the data series for calculation. |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_EXECUTION_FINISHED: Execution finished without errors |
| 16#7000 | STATUS_NO_CALL: No call of FB. The block waits for activation. |
| 16#7001 | STATUS_FIRST_CALL: First call of FB after enabling |
| 16#8600 | ERR_SHELL_SORT: Error in command `LGF_ShellSort_UDInt`. |
| 16#9101 | ERR_WRONG_NO_CLASSES: Incorrect number of classes. |


### Related Functions

- `LGF_Histogram_DInt`
- `LGF_RegressionLine`

---

# LGF_RegressionLine - Linear Regression Calculator

**Type:** FUNCTION
**Category:** Statistical Analysis
**Difficulty Level:** Advanced
**Tags:** regression, linear, lreal, statistics, curve-fitting, slope

## Description

## Short description ##

The simplest case of a regression is the regression line. This means that the assumed 
relationship between the input and output signal is a linear straight line.
Figure: Regression line

## Functional description ##

The block calculates the regression line with the following line equation:
𝑓(𝑥) = 𝑚 ⋅ 𝑥 + 𝑡
𝑚: Gradient of straight line
𝑡: Intersection with y-axis
𝑁: number of array elements

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| slope | LReal | Gradient of straight line |
| intercept | LReal | The intersection with the Y axis |
| error | Bool | FALSE: No error TRUE: An error occurred during the execution of the FB |
| status | Word | Status of the FB |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| values | Array[*] of LGF_typeRegressionLine | The data points are transferred with their X- and Y-values. |

### Return Value

- **Type:** Void
- **Description:** Void - Function has no return value

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_EXECUTION_FINISHED |
| 16#8200 | ERR_NOT_ENOUGH_VALUES Error: Not enough Values. |

## User Defined Types

### LGF_typeRegressionLine
UDT for transferring datapoints to LGF_RegressionLine

### Members

| Name | Type | Description |
| :--- | :--- | :--- |
| x | Real | X-Axis value |
| y | Real | Y-Axis value |


### Related Functions

- `LGF_Histogram_DInt`
- `LGF_Histogram_UDInt`

---

# LGF_MatrixTranspose - Matrix Transposer

**Type:** FUNCTION

## Description

## Short description ##

This function transposes a matrix of the data type ARRAY[*,*] of LREAL.
Condition: Input matrix (m x n) = output matrix (n x m).
A matrix is transposed by making columns out of the rows.
Note Note that the number of rows of the input matrix must be equal to the number of columns of 
the output matrix. Also, the number of columns of the input matrix must be equal to the 
number of rows of the output matrix.

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | Error flag |
| status | Word | Status code |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| matrix | Array[*, *] of LReal | Matrix to be transposed |
| matrixTranspose | Array[*, *] of LReal | Transposed matrix |

### Return Value

- **Type:** Void
- **Description:** Void - Function has no return value

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8200 | ERR_MATR1_LOWBOUND_ROWS_RESMATR_LOWBOUND_COLUMNS |
| 16#8201 | ERR_MATR1_LOWBOUND_COLUMNS_RESMATR_LOWBOUND_ROWS |
| 16#8202 | ERR_MATR1_UPPBOUND_ROWS_RESMATR_UPPBOUND_COLUMNS |
| 16#8203 | ERR_MATR1_UPPBOUND_COLUMNS_RESMATR_UPPBOUND_ROWS |

---

# LGF_CalcDistance_3D - 3D distance calculation between points

**Type:** FUNCTION

## Description

## Short description ##

The function calculates the distance between two points in 3D space.

## Functional description ##

The block calculates the distance between two points in a Cartesian coordinate system. The 
distance is calculated with the following formula:
result = 2√((𝑥2 − 𝑥1)^2 + (𝑦2 − 𝑦1)^2 + (𝑧2 − 𝑧1)^2)

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| x1 | LReal | X coordinate point 1 |
| y1 | LReal | Y coordinate point 1 |
| z1 | LReal | Z coordinate point 1 |
| x2 | LReal | X coordinate point 2 |
| y2 | LReal | Y coordinate point 2 |
| z2 | LReal | Z coordinate point 2 |

### Return Value

- **Type:** LReal
- **Description:** Calculated distance between the Points

---

# LGF_GetBitStates - Double word edge detection

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

This function checks a DWord for falling as well as rising edges.
It returns the number of edges, a DWord with the edge bits, and a boolean value if edge(s) are 
present.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | DWord | Check input value for changes and edges |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| hasChanged | Bool | Input value has changed (compared to the previous cycle) |
| hasRisingEdges | Bool | Input value has rising edges |
| risingBits | DWord | Bitstream with the rising edges |
| noOfRisingBits | USInt | Number of rising edges in the input value |
| hasFallingEdges | Bool | Input value has falling edges |
| fallingBits | DWord | Bitstream with the falling edges |
| noOfFallingBits | USInt | Number of falling edges in the input value |

---

# LGF_MatrixSubtraction - Matrix Subtractor

**Type:** FUNCTION

## Description

## Short description ##

This function subtracts a matrix of the data type ARRAY[*,*] of LREAL from another one.
The individual fields of the two matrices are read, subtracted and then output in the matrix 
matrixResult.
Note Note that all input and output matrices must have the same number of columns and rows

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | Error flag |
| status | Word | Status code |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| matrix1 | Array[*, *] of LReal | First matrix - minuend |
| matrix2 | Array[*, *] of LReal | Second matrix - subtrahend |
| matrixResult | Array[*, *] of LReal | Sum of the matrices |

### Return Value

- **Type:** Void
- **Description:** Void - Function has no return value

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8200 | ERR_MATR1_LOWBOUND_ROWS_MATR2_LOWBOUND_ROWS |
| 16#8201 | ERR_MATR1_LOWBOUND_ROWS_RESMATR_LOWBOUND_ROWS |
| 16#8202 | ERR_MATR1_LOWBOUND_COLUMNS_MATR2_LOWBOUND_COLUMNS |
| 16#8203 | ERR_MATR1_LOWBOUND_COLUMNS_RESMATR_LOWBOUND_COLUMNS |
| 16#8204 | ERR_MATR1_UPPBOUND_ROWS_MATR2_UPPBOUND_ROWS |
| 16#8205 | ERR_MATR1_UPPBOUND_ROWS_RESMATR_UPPBOUND_ROWS |
| 16#8206 | ERR_MATR1_UPPBOUND_COLUMNS_MATR2_UPPBOUND_COLUMNS |
| 16#8207 | ERR_MATR1_UPPBOUND_COLUMNS_RESMATR_UPPBOUND_COLUMNS |

---

# LGF_FIFO - FIFO Buffer Management

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

FIFO (First-In First-Out / Queue / ring buffer memory)
This function stores incoming data and outputs the oldest unprocessed data.

## Functional description ##

Note The status of called commands is output in subFunctionStatus. In this case, the output value 
in status indicates which command caused the error. In this case, refer to the TIA Portal 
Online Help section for information on the respective commands.
Note In computer science, the queue is also based on the FIFO principle.
With the enqueue input, a new item is stored from the InOut parameter item in the next free 
position in the buffer. The output elementCount is incremented by one.
With the dequeue input, the next element to be processed is output to the InOut parameter item, 
and this field in the buffer is replaced by the value in the parameter initialItem. The output 
elementCount decremented by one.
With the reset input, the buffer is initialized and the index and counter are reset. The 
elementCount output is set to zero and the isEmpty output is set to TRUE.
With the clear input, the buffer is emptied and initialized with the initial value initialItem. Index 
and counter are reset. The elementCount output is set to zero and the isEmpty output is set to 
TRUE.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| enqueue | Bool | Enqueue item to the buffer |
| dequeue | Bool | Dequeue item from the buffer and return it on `item` |
| reset | Bool | Initializing the buffer (reset the index and the counter) |
| clear | Bool | Clearing the buffer and initialize with the initial value `initialItem` (Reset index and counter). |
| initialItem | Variant | Value with which the ARRAY of the buffer is initialized (usually: `0` / default value) |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | An error occurred during the execution of the FB |
| status | Word | Status of the FB, Error identification |
| subFunctionStatus | Word | Status or return value of called FB's, FC's and system blocks |
| elementCount | DInt | Number of elements in the buffer |
| isEmpty | Bool | Buffer is empty |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| item | Variant | The entry that is either returned from the ring buffer or written into the buffer |
| buffer | Variant | The ARRAY that is used as the ring buffer. |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#7000 | STATUS_NO_CURRENT_JOBS |
| 16#8001 | ERR_BUFFER_EMPTY |
| 16#8002 | ERR_BUFFER_FULL |
| 16#8200 | ERR_NO_ARRAY |
| 16#8201 | ERR_WRONG_TYPE_ITEM |
| 16#8202 | ERR_WRONG_TYPE_INITIAL_ITEM |
| 16#8601 | ERR_INDEX_IN_ARRAY_LIMITS_1 |
| 16#8602 | ERR_INDEX_IN_ARRAY_LIMITS_2 |
| 16#8610 | ERR_CLEAR_BUFFER |
| 16#8611 | ERR_RETURN_FIRST_ENTRY |
| 16#8612 | ERR_REPLACE_ITEM_BY_INIT_VALUE |
| 16#8613 | ERR_WRITE_ENTRY |

---

# LGF_Boxplot_DInt - Boxplot Calculation for Integer Data

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

If you want to get an overview of existing data, you can use a Boxplot diagram. A Boxplot shows 
you in which area the data is located and how it is distributed over this area. A Boxplot consists 
of the following parameters:
• Minimum (smallest occurring value of the sample)
• Lower or first quartile (below this value are 25% of the sample values)
• Median or second quartile (below this value are 50% of the sample values)
• Upper or third quartile (below this value are 75% of the sample values)
• Maximum (largest occurring value of the sample)
Figure: Boxplot

## Functional description ##

The block sorts the data series and then calculates the so-called “five-point summary”:
Table: Five-point summary
Characteristic value of the five-point summary Output parameter of the block
Minimum (smallest occurring value of the sample) min
Lower or first quartile (below this value are 25% of 
the sample values)
q25
Median or second quartile (below this value are 
50% of the sample values)
median
Upper or third quartile (below this value are 75% of 
the sample values)
q75
Maximum (largest occurring value of the sample) max
If outlier detection is activated, the block first calculates the limits. From these limit values, the 
values are recognized as outliers:

The block then calculates new values for the parameters max and min, which lie within the outlier 
limits. The outliers are counted and output as a percentage.
To make it easier to judge how the data is distributed, the block also calculates the skew. The 
skewness lies between the values -1 and 1 with the following meaning:
• -1: extremely left skewed distribution
• 0: symmetrical distribution
• 1: extreme right-skew distribution
The elements of the passed array are sorted in ascending order by the block. The 
LGF_Shellsort_DInt block is used for sorting.
The parameters are calculated as follows:
Table: Boxplot formulas Parameters Formula

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| execute | Bool | Activation of the calculation with each positive edge. |
| rangeOutlier | LReal | Outlier detection parameter. |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | An error occurred during the execution of the FB |
| status | Word | Status of the FB |
| subfunctionStatus | Word | Status or return value of called FB's, FC's and system blocks |
| outlierMax | LReal | Upper outliers in % |
| max | DInt | Maximum Value, not an outlier. |
| q75 | LReal | 3rd quartile or Q75 of the data series. |
| median | LReal | 2nd quartile or Median of the data series. |
| q25 | LReal | 1st quartile or Q25 of the data series. |
| min | DInt | Minimum Value, not an outlier. |
| outlierMin | LReal | Lower outliers in % |
| skewness | LReal | Skewness of the data series. |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| values | Array[*] of DInt | The array containing the data series for calculation |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_EXECUTION_FINISHED |
| 16#7000 | STATUS_NO_CALL |
| 16#7001 | STATUS_FIRST_CALL |
| 16#8200 | ERR_NEG_ARR_BOUND |
| 16#8600 | ERR_SHELL_SORT |
| 16#9101 | ERR_RANGE_NOT_OK |

---

# LGF_DTLToJulianDate - DTL to Julian Date Converter

**Type:** FUNCTION

## Description

## Short description ##

This function converts the date and time of data type DTL to the Julian date and as well the 
modified Julian Date to data type LReal (Double).
The timestamp is calculated based on UTC. This means that the time zone is not considered.
Only times after 01/01/1990 are permitted.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| timeDTL | DTL | Date and time as DTL to convert to Julian Date |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| julianDate | LReal | Converted Julian date |
| modifiedJulianDate | LReal | Converted modified Julian date |
| error | Bool | An error occurred during the execution of the FB |
| status | Word | Status of the FB, Error identification |

### Return Value

- **Type:** Void
- **Description:** ---

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_EXECUTION_FINISHED_NO_ERROR |
| 16#8000 | ERR_DTL_INPUT_VALUE_INVALID |
| 16#8001 | ERR_TIME_BEFORE_1990 |

---

# LGF_FileWrite - File Writing to UserFiles Folder

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

This function block offers writing data as binary / serialized data stream to a file which is then 
stored on the PLC's memory card in the folder UserFiles.

## Functional description ##

With the function LGF_FileWrite the data budget of a variable can be written to data in a file. For 
writing the data it is necessary to serialize it, which the function already takes from the user.
For serialization an external buffer in the form of a byte array must be connected which can take 
up the data quantity, if the buffer is too small an error is output.
The file name must always be specified in full together with the folder name and the file 
extension in the following format: UserFiles/test.dat.
Note The file extension (here e.g. dat) can be freely selected or omitted, it is useful for external 
processing to indicate the format of the file to the user.
A file extension in the file name has no influence on the content of the file as well as its 
formatting, to provide the data in an appropriate file format is up to the user.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| execute | Bool | Rising edge starts file write once |
| fileName | String | Name of file including path: UserFiles/test.dat |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| done | Bool | Commanded functionality has been completed successfully |
| busy | Bool | FB is not finished and new output values can be expected |
| error | Bool | An error occurred during the execution of the FB |
| status | Word | Status of the FB, Error identification |
| dataLength | DInt | Data length written to file (serialized length of data) |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| bufferByteArray | Array[*] of Byte | Byte array buffer for read / write from / to file |
| data | Variant | Data set to write into file |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_EXECUTION_FINISHED |
| 16#7000 | STATUS_NO_CALL |
| 16#7001 | STATUS_FIRST_CALL |
| 16#7002 | STATUS_SUBSEQUENT_CALL |
| 16#8201 | ERR_BUFFER_LOWERBOUND |
| 16#8202 | ERR_BUFFER_ARRAY_TO_SMALL_TO_COPY |
| 16#8401 | ERR_FILE_PATH |
| 16#8600 | ERR_UNDEFINED_STATE |
| 16#8601 | ERR_MOVE_BLK_VARIANT |
| 16#8603 | ERR_DATA_SERIALIZE |
| 16#8604 | ERR_FILE_WRITE_INIT |
| 16#8605 | ERR_FILE_WRITE |

## User Defined Types

### LGF_typeDiagnostics
Diagnostic structure to store and transfer diagnostic information from blocks trough the interface.

### Members

| Name | Type | Description |
| :--- | :--- | :--- |
| status | Word | Status of the Block or error identification when error occurred |
| subfunctionStatus | Word | Status or return value of called FB's, FC's and system blocks |
| stateNumber | DInt | State in the state machine of the block where the error occurred |

---

# LGF_ShiftRegister - Shift Register for Datatype Variant

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

The Function represents a shift register for any kind of Datatype (using variant).
It is possible to shift the elements in the array at bufferRegister to the left (index 
array[n]:=array[n+1]) or right (index array[n]:=array[n-1]).
It could be used for material tracking trough a machine or a process, e.g. for a rotary indexing 
table.
Note As this is a real shift operation, it may cause some runtime effects while using big array sizes 
to move at the input bufferRegister.
Please consider that a FIFO or LIFO storage, based on indexes, could be used as well for 
most applications.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| shiftLeft | Bool | Rising edge: Elements in the array bufferRegister shifted left. |
| shiftRight | Bool | Rising edge: Elements in the array bufferRegister shifted right. |
| shiftRange | UInt | Number of places to be shifted in the bufferRegister input array |
| clear | Bool | Clear buffer elements in bufferRegister with initalItem |
| fill | Bool | Overwrite buffer elements after shift operation. |
| initialItem | Variant | Value with which the array at input bufferRegister is initialized. |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | An error occurred during the execution of the FB |
| status | Word | Status of the FB, Error identification |
| subFunctionStatus | Word | Status or return value of called FB's, FC's and system blocks |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| bufferRegister | Variant | Buffer / Register memory as ARRAY, which keeps the data. |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#7000 | STATUS_NO_CURRENT_JOBS |
| 16#8200 | ERR_NO_ARRAY |
| 16#8201 | ERR_CLEARING_WITHOUT_INITIAL_ITEM |
| 16#8202 | ERR_FILL_WITHOUT_INITIAL_ITEM |
| 16#8203 | ERR_WRONG_TYPE_INITIAL_ITEM |
| 16#8401 | ERR_MORE_THAN_ONE_COMMAND |
| 16#8402 | ERR_IN_SHIFT_RANGE |
| 16#8610 | ERR_CLEAR_BUFFER |
| 16#8611 | ERR_SHIFT_BUFFER_LEFT |
| 16#8612 | ERR_SHIFT_BUFFER_LEFT_FILL |
| 16#8622 | ERR_SHIFT_BUFFER_RIGHT_FILL |

---

# LGF_Random_DInt - DInt range random number generation

**Type:** FUNCTION

## Description

## Short description ##

This function generates a random value with each call.
The random number has the data type DInt.

## Functional description ##

Note The status of called commands is output in subFunctionStatus. In this case, the output value 
in status indicates which command caused the error. In this case, refer to the TIA Portal 
Online Help section for information on the respective commands.
The function generates random values in the range:
−2147483648 ≤ 𝑅𝑒𝑡𝑢𝑟𝑛𝑉𝑎𝑙 ≤ 2147483647.
The random value is formed from the nanoseconds of the current system time of the CPU. The 
byte order of this value is inverted and then converted to DInt.

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | Error flag |
| status | Word | Status code |
| subfunctionStatus | Word | Status or return value of called blocks |

### Return Value

- **Type:** DInt
- **Description:** Random number in the DInt range

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_FINISHED_NO_ERROR |
| 16#8600 | ERR_RD_SYS_T |

---

# LGF_SplitDWordToWords - DWord to 2-Word Splitter

**Type:** FUNCTION

## Description

## Short description ##

This function splits a DWord variable into 2 Word variables.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| doubleWord | DWord | Bit sequence to be split |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| word1 | Word | Output Word 1 - MSW |
| word0 | Word | Output Word 0 - LSW |

---

# LGF_CalcCRC8Advanced - Advanced CRC-8 Calculator

**Type:** FUNCTION

## Description

## Short description ##

The CRC calculation is used for error detection at data transmission. The result of a calculation 
returns a CRC value via the data sent. The receiver detects a faulty transmission due to the 
unequal CRC value. The function LGF_CalcCRC8Advanced uses 8 bits as the generator 
polynomial (mask) and the parameters finalXorValue, reflectInput, and reflectResult.

## Functional description ##

The function calculates the CRC value from a data stream of any size. The data stream is 
composed of the individual elements of the array at the input/output parameter array. The start 
value initValue and the generator polynomial mask can be freely selected.
Via the Boolean input parameters reflectInput and reflectResult, you may optionally mirror 
the bits of the input data or the CRC value. An XOR operation is also performed with the CRC 
value at the end and the value finalXorValue.
The input noOfELements can be used to specify the desired number of elements for calculation, it 
applies:
𝑁𝑢𝑚𝑏𝑒𝑟𝑂𝑓𝐸𝑙𝑒𝑚𝑒𝑛𝑡𝑠 <= (𝐴𝑟𝑟𝑎𝑦𝑈𝑝𝑝𝑒𝑟𝐿𝑖𝑚𝑖𝑡 − 𝐴𝑟𝑟𝑎𝑦𝐿𝑜𝑤𝑒𝑟𝑈𝑛𝑑𝑒𝑟𝐿𝑖𝑚𝑖𝑡 + 1)
Note Various online tools are available for calculating the CRC values. The function of the block 
was tested with the following online tool, since it supports the input parameters mask
(Polynomial) and initValue (Initial Value):
http://www.sunshine2k.de/coding/javascript/crc/crc_js.html

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| initValue | Byte | Start value for the calculation |
| mask | Byte | Generator polynomial for the calculation |
| finalXorValue | Byte | Value for final XOR operation |
| reflectInput | Bool | Mirror the bits within the input byte |
| reflectResult | Bool | Mirror the order of the bits within the result |
| noOfElements | UInt | Number of elements to be used in CRC calculation |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | Error flag |
| status | Word | Status code |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| array | Array[*] of Byte | Data stream for which the CRC value will be calculated |

### Return Value

- **Type:** Byte
- **Description:** Calculated CRC value

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8400 | ERR_NO_OF_ELEMENTS |

---

# LGF_BinaryToGray - Binary to Gray Code Converter

**Type:** FUNCTION

## Description

## Short description ##

This function converts a binary coded value into a Gray-coded value.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| variableBinary | DWord | Binary coded value to convert to Gray code |

### Return Value

- **Type:** DWord
- **Description:** Gray-coded value

---

# LGF_MatrixInverse - Matrix Inverter

**Type:** FUNCTION

## Description

## Short description ##

This function inverts a square matrix of the data type ARRAY[*,*] of LREAL.
The square matrix of any size will be inverted according to the Shipley-Coleman method.
𝑚𝑎𝑡𝑟𝑖𝑥𝑅𝑒𝑠𝑢𝑙𝑡 = 𝑚𝑎𝑡𝑟𝑖𝑥^(−1)
Note Note that the input matrix must be square. This means that the number of rows must be 
equal to the number of columns. The output matrix must be the same size and have the 
same array boundaries as the input matrix.

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | Error flag |
| status | Word | Status code |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| matrix | Array[*, *] of LReal | Square input matrix that will be inversed |
| matrixResult | Array[*, *] of LReal | Inverted matrix |

### Return Value

- **Type:** Void
- **Description:** Void - Function has no return value

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8200 | ERR_NOT_SQUARE_MATRIX |
| 16#8201 | ERR_ALGORITHM_NOT_POSSIBLE |
| 16#8202 | ERR_MATR1_LOWBOUND_ROWS_RESMATR_LOWBOUND_ROWS |
| 16#8203 | ERR_MATR1_LOWBOUND_COLUMNS_RESMATR_LOWBOUND_COLUMNS |
| 16#8204 | ERR_MATR1_UPPBOUND_ROWS_RESMATR_UPPBOUND_ROWS |
| 16#8205 | ERR_MATR1_UPPBOUND_COLUMNS_RESMATR_UPPBOUND_COLUMNS |

---

# LGF_SplitWordToBytes - Word to 2-Byte Splitter

**Type:** FUNCTION

## Description

## Short description ##

This function splits a Word variable into 2 Byte variables.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| word | Word | Bit sequence to be split |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| byte1 | Byte | Output Byte 1 - MSB |
| byte0 | Byte | Output Byte 0 - LSB |

---

# LGF_CompareLRealByPrecision - LReal numbers comparison with variable precision

**Type:** FUNCTION

## Description

## Short description ##

This function checks floating point numbers for equality, by using an approximation formula and 
a fixed precision by constant 1.0E-12 (pico)

## Functional description ##

The comparison of the LREAL numbers is based on an given accuracy at the parameter 
precision. The difference between the two input values must be smaller than the precision
accuracy value multiplied by one of the two input values.
Equation:

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| valueA | LReal | First LREAL number to be compared. |
| valueB | LReal | Second LREAL number to be compared. |
| precision | LReal | Accuracy with which the two values are compared. |

### Return Value

- **Type:** Bool
- **Description:** FALSE: not equal, TRUE: approximately the same

---

# LGF_IsLittleEndian - Endianness Detection Function for Little Endian

**Type:** FUNCTION

## Description

## Short description ##

The function detects the endianness of the executing system.

### Return Value

- **Type:** Bool
- **Description:** TRUE if little endianness is detected

---

# LGF_SimpleSmoothingFC - Simple Smoothing Function

**Type:** FUNCTION

## Description

## Short description ##

The function calculates the linear mean value acyclically.
The simplest form of smoothing a sequence of measured values is to calculate the linear mean 
value by three points.
The function reads an array that is smoothed. 𝑁 − 2 smoothed measured values can be 
calculated from N measured values. Therefore, the output array in the index (0) and index (N) 
contains the value 0.

## Functional description ##

The function calculates the smoothed values using the following formula:

The calculated value is output or the calculated values are output at output smoothedValue.
Based on this formula, the function cannot calculate values for the elements 0 and N.

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | FALSE: No error TRUE: An error occurred during the execution of the FB |
| status | Word | Status of the FB |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| values | Array[*] of LReal | Values that are to be included in the smoothing. |
| smoothedValues | Array[*] of LReal | The smoothed values. |

### Return Value

- **Type:** Void
- **Description:** Void - Function has no return value

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_FINISHED_NO_ERROR |
| 16#8400 | ERR_NOT_ENOUGH_VALUES Error: Not enough values. |
| 16#8401 | ERR_ARRAY_DIFFERENT Error: The Arraysizes are not equal. |

---

# LGF_CalcDistance_2D - 2D distance calculation between points

**Type:** FUNCTION

## Description

## Short description ##

The function calculates the distance between two points in the plane.

## Functional description ##

The block calculates the distance between two points in a Cartesian coordinate system. The 
distance is calculated with the following formula:
result = 2√((x2 − x1)^2 + (y2 − y1)^2)

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| x1 | LReal | X coordinate point 1 |
| y1 | LReal | Y coordinate point 1 |
| x2 | LReal | X coordinate point 2 |
| y2 | LReal | Y coordinate point 2 |

### Return Value

- **Type:** LReal
- **Description:** Calculated distance between the Points

---

# LGF_KelvinToCelsius - Kelvin to Celsius Converter

**Type:** FUNCTION

## Description

## Short description ##

This function converts a temperature value - from °Kelvin to °Celsius.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | Real | Temperature to be converted in °Kelvin |

### Return Value

- **Type:** Real
- **Description:** Converted temperature in °Celsius

---

# LGF_MergeBitsToDWord - 32-Bit to DWord Merger

**Type:** FUNCTION

## Description

## Short description ##

This function merge 32 Bits / 32 Boolean variables into one DWord variable.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| bit31 | Bool | Input Bit 31 - MSB |
| bit30 | Bool | Input Bit 30 |
| bit29 | Bool | Input Bit 29 |
| bit28 | Bool | Input Bit 28 |
| bit27 | Bool | Input Bit 27 |
| bit26 | Bool | Input Bit 26 |
| bit25 | Bool | Input Bit 25 |
| bit24 | Bool | Input Bit 24 |
| bit23 | Bool | Input Bit 23 |
| bit22 | Bool | Input Bit 22 |
| bit21 | Bool | Input Bit 21 |
| bit20 | Bool | Input Bit 20 |
| bit19 | Bool | Input Bit 19 |
| bit18 | Bool | Input Bit 18 |
| bit17 | Bool | Input Bit 17 |
| bit16 | Bool | Input Bit 16 |
| bit15 | Bool | Input Bit 15 |
| bit14 | Bool | Input Bit 14 |
| bit13 | Bool | Input Bit 13 |
| bit12 | Bool | Input Bit 12 |
| bit11 | Bool | Input Bit 11 |
| bit10 | Bool | Input Bit 10 |
| bit9 | Bool | Input Bit 9 |
| bit8 | Bool | Input Bit 8 |
| bit7 | Bool | Input Bit 7 |
| bit6 | Bool | Input Bit 6 |
| bit5 | Bool | Input Bit 5 |
| bit4 | Bool | Input Bit 4 |
| bit3 | Bool | Input Bit 3 |
| bit2 | Bool | Input Bit 2 |
| bit1 | Bool | Input Bit 1 |
| bit0 | Bool | Input Bit 0 - LSB |

### Return Value

- **Type:** DWord
- **Description:** Composite Bit sequence stored as DWord variable

---

# LGF_SearchMinMax_DInt - DInt Array Min/Max Value and Index Searcher

**Type:** FUNCTION

## Description

## Short description ##

This function searches, in an array of the data type DInt, for the maximum and minimum value 
and the respective index in the array.

## Functional description ##

An array of any size is connected via the values input. The elements are then compared in turn. 
The smallest and largest values, as well as their corresponding index are output to the array.
Note If there are several identical min. or max. values, the index of the first min. or max. value is 
output.

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| minValue | DInt | Minimum value found in the array |
| minValueIndex | DInt | Index of the minimum found value in the array |
| maxValue | DInt | Maximum value found in the array |
| maxValueIndex | DInt | Index of the maximum found value in the array |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| values | Array[*] of DInt | Array in whose fields the maximum and minimum are searched |

---

# LGF_DTLToUnixTime - DTL to UNIX Time Converter

**Type:** FUNCTION

## Description

## Short description ##

This function converts the date and time of data type DTL to the UNIX time of data type DInt. The timestamp is calculated in UTC. This means that the time zone is not considered.
Only times after 01/01/1990 are permitted.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| timeDTL | DTL | Date and time as DTL to convert to UNIX time |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | An error occurred during the execution of the FB |
| status | Word | Status of the FB, Error identification |

### Return Value

- **Type:** DInt
- **Description:** Converted UNIX time

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_EXECUTION_FINISHED_NO_ERROR |
| 16#8000 | ERR_TIME_BEFORE_1990 |
| 16#8001 | ERR_DTL_INPUT_VALUE_INVALID |

---

# LGF_SwapBlockLWord - LWord Endianness Adjuster

**Type:** FUNCTION

## Description

## Short description ##

Adjusts/ switches the endianness of multibyte data typed values.
For this to achieve, a loop will iterate through the array elements and swap the bytes 
intrinsically.

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| data | Array[*] of LWord | Contains the data values, which will be endianness adjusted |

### Return Value

- **Type:** Void
- **Description:** Void - Function has no return value

---

# LGF_Boxplot_UDInt - Boxplot Calculation for Unsigned Integer Data

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

If you want to get an overview of existing data, you can use a Boxplot diagram. A Boxplot shows 
you in which area the data is located and how it is distributed over this area. A Boxplot consists 
of the following parameters:
• Minimum (smallest occurring value of the sample)
• Lower or first quartile (below this value are 25% of the sample values)
• Median or second quartile (below this value are 50% of the sample values)
• Upper or third quartile (below this value are 75% of the sample values)
• Maximum (largest occurring value of the sample)
Figure: Boxplot

## Functional description ##

The block sorts the data series and then calculates the so-called “five-point summary”:
Table: Five-point summary
Characteristic value of the five-point summary Output parameter of the block
Minimum (smallest occurring value of the sample) min
Lower or first quartile (below this value are 25% of 
the sample values)
q25
Median or second quartile (below this value are 
50% of the sample values)
median
Upper or third quartile (below this value are 75% of 
the sample values)
q75
Maximum (largest occurring value of the sample) max
If outlier detection is activated, the block first calculates the limits. From these limit values, the 
values are recognized as outliers:

The block then calculates new values for the parameters max and min, which lie within the outlier 
limits. The outliers are counted and output as a percentage.
To make it easier to judge how the data is distributed, the block also calculates the skew. The 
skewness lies between the values -1 and 1 with the following meaning:
• -1: extremely left skewed distribution
• 0: symmetrical distribution
• 1: extreme right-skew distribution
The elements of the passed array are sorted in ascending order by the block. The 
LGF_Shellsort_UDInt block is used for sorting.
The parameters are calculated as follows:
Table: Boxplot formulas Parameters Formula

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| execute | Bool | Activation of the calculation with each positive edge. |
| rangeOutlier | LReal | Outlier detection parameter. |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | An error occurred during the execution of the FB |
| status | Word | Status of the FB |
| subfunctionStatus | Word | Status or return value of called FB's, FC's and system blocks |
| outlierMax | LReal | Upper outliers in % |
| max | UDInt | Maximum Value, not an outlier. |
| q75 | LReal | 3rd quartile or Q75 of the data series. |
| median | LReal | 2nd quartile or Median of the data series. |
| q25 | LReal | 1st quartile or Q25 of the data series. |
| min | UDInt | Minimum Value, not an outlier. |
| outlierMin | LReal | Lower outliers in % |
| skewness | LReal | Skewness of the data series. |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| values | Array[*] of UDInt | The array containing the data series for calculation |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_EXECUTION_FINISHED |
| 16#7000 | STATUS_NO_CALL |
| 16#7001 | STATUS_FIRST_CALL |
| 16#8200 | ERR_NEG_ARR_BOUND |
| 16#8600 | ERR_SHELL_SORT |
| 16#9101 | ERR_RANGE_NOT_OK |

---

# LGF_MergeBytesToDWord - 4-Byte to DWord Merger

**Type:** FUNCTION

## Description

## Short description ##

This function merge 4 Byte variables into one DWord variable.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| byte3 | Byte | Input Byte 3 - MSB |
| byte2 | Byte | Input Byte 2 |
| byte1 | Byte | Input Byte 1 |
| byte0 | Byte | Input Byte 0 - LSB |

### Return Value

- **Type:** DWord
- **Description:** Composite Byte sequence stored as DWord variable

---

# LGF_Random_Real - Random Real Number Generator

**Type:** FUNCTION

## Description

## Short description ##

This function generates a random value with each call.
The random number has the data type Real in the range from 0.0 to 1.0.

## Functional description ##

Note The status of called commands is output in subFunctionStatus. In this case, the output value 
in status indicates which command caused the error. In this case, refer to the TIA Portal 
Online Help section for information on the respective commands.
The function generates random values in the range:
0.0 ≤ 𝑅𝑒𝑡𝑢𝑟𝑛𝑉𝑎𝑙 ≤ 1.0.
The random value is formed from the nanoseconds of the current system time of the CPU. The 
byte order of this value is inverted and then converted to a floating point.

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | Error flag |
| status | Word | Status code |
| subfunctionStatus | Word | Status or return value of called blocks |

### Return Value

- **Type:** Real
- **Description:** Random Real number between 0.0 and 1.0

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_FINISHED_NO_ERROR |
| 16#8600 | ERR_RD_SYS_T |

---

# LGF_CountFalInDWord - DWORD falling edge counting

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

The function analyzes a variable of the type DWORD and outputs how often a 1-0 sequence 
(falling edge) occurs in the variable.
Note LEGACY FUNCTION
Please update and use the FB with the same name LGF_CountFalInDWord in the future!
This function is no longer maintained!

## Functional description ##

In a variable of the data type DWORD, the block counts the falling edges (1-0 transitions) from 
left to right. The output countFalInDWord outputs the number of falling edges.
So that falling edges at the variable limit are also detected, the input value is copied to the static 
variable statDWordPrevCycle at the end of the evaluation and evaluated in the next cycle.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | DWord | Input Double word in which the falling edges are counted |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| numberOfEdges | Int | Number of falling edges in the DWord |

---

# LGF_ScaleLinear - Linear Scaler for Input Variable

**Type:** FUNCTION

## Description

## Short description ##

This function scales an input variable (LReal) via a linear straight-line equation.

## Functional description ##

The function linearly scales an input variable (e.g. an analog input value) to a specific output 
variable (e.g. level).
To determine the output variable, the following linear equation is used in the function:
𝑥 =
((𝑦2 − 𝑦1) / (𝑥2 − 𝑥1)) * (𝑥 − 𝑥1) + 𝑦1
The straight line is described by the two points, P1 and P2. You specify the points as a 
Cartesian coordinate system using x and y coordinates.
Note If the values of the parameters x1 and x2 are the same, the value of y1 is output on output y
By specifying yMin and yMax you can restrict the calculated value of y to a range limited at top 
and bottom. Thus, you avoid override and underride ranges.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| x | LReal | Input value `x` to be scaled |
| x1 | LReal | Point 1 (P1) -`x` coordinate of the linear function |
| y1 | LReal | Point 1 (P1) -`y` coordinate of the linear function |
| x2 | LReal | Point 2 (P2) -`x` coordinate of the linear function |
| y2 | LReal | Point 2 (P2) -`y` coordinate of the linear function |
| yMin | LReal | Lower limit value of the output |
| yMax | LReal | High limit value of the output |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | Error flag |
| status | Word | Status code |

### Return Value

- **Type:** LReal
- **Description:** Scaled output value `y`

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_FINISHED_NO_ERROR |
| 16#6001 | WARN_Y_LIMITED_TO_YMIN |
| 16#6002 | WARN_Y_LIMITED_TO_YMAX |
| 16#8200 | ERR_LOW_LIM_OVER_UP_LIM |

---

# LGF_ReadPnInterfaceParameter - Profinet Interface Parameter Reader

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

The function block provides Interface parameter like the IP Address settings, MAC Address and 
the PN Name.

## Functional description ##

The function reads the Interface settings / parameters using the system function RDREC (Read 
data record).
To read the MAC and IP address of the interface provided via it's hardware ID, it is mandatory 
to read the PD_INTERFACE_DATA_REAL data record of any PROFINET compliant interface.
Note Upon TIA Portal V17, it’s possible to use as well the system function CommConfig, which is in 
the Instructions / Communication / Open user communication (Version >= V8.1) located.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| execute | Bool | Rising edge starts action once |
| hardwareId | HW_ANY | Hardware ID of the Interface where the parameter should be read |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| done | Bool | Commanded functionality has been completed successfully |
| busy | Bool | FB is not finished, new output values can be expected |
| error | Bool | An error occurred during the execution of the FB |
| status | DWord | Status of the FB and error identification |
| address | IP_V4 | IP Address from interface |
| subnetMask | IP_V4 | Subnet mask from interface |
| standardGateway | IP_V4 | Standard gateway address from interface |
| macAddress | Array[0..5] of Byte | MAC Address from interface |
| pnName | String | Profinet name from interface |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_EXECUTION_FINISHED: Execution finished without errors |
| 16#7000 | STATUS_NO_CALL: No job being currently processed |
| 16#7001 | STATUS_FIRST_CALL: First call after incoming new job |
| 16#7002 | STATUS_SUBSEQUENT_CALL: Subsequent call during active processing |
| 16#9000 | ERR_UNDEFINED_STATE: Due to an undefined state in state machine |

---

# LGF_GpsDDToGps - GPS-DD to GPS Direction DMS Converter

**Type:** FUNCTION

## Description

## Short description ##

This function converts a given GPS-DD data type (decimal degrees) into a GPS data type 
(direction, degrees, minutes, and seconds).
GPS decimal degree to GPS “native”.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| gps | LGF_typeGPS_DD | GPS-Data to be converted (decimal degrees) |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | An error occurred during the execution of the FB |
| status | Word | Status of the FB, Error identification |

### Return Value

- **Type:** LGF_typeGPS
- **Description:** Converted GPS-Data (direction, degrees, minutes, and seconds)

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_EXECUTION_FINISHED_NO_ERROR |
| 16#8201 | ERR_LATITUDE_VALUE |
| 16#8203 | ERR_LONGITUDE_VALUE |

## User Defined Types

### LGF_typeGPS_DD
Datatype for GPS Coordinates in decimal degrees.

### Members

| Name | Type | Description |
| :--- | :--- | :--- |
| latitude | Real | Degrees latitude with decimal places |
| longitude | Real | Degrees longitude in degrees with decimal places |

### LGF_typeGPS
Datatype for GPS Coordinates with direction, degrees, minutes, seconds.

### Members

| Name | Type | Description |
| :--- | :--- | :--- |
| latitude | LGF_typeGPS_DMS | Datatype for GPS Coordinates in DMS and the Direction. |
| longitude | LGF_typeGPS_DMS | Datatype for GPS Coordinates in DMS and the Direction. |

---

# LGF_CompareVariant - Structured data comparison

**Type:** FUNCTION

## Description

## Short description ##

The function compares two structured actual parameters (array, PLC data type) and outputs 
whether they are of the same type and have the same values.
Compare arrays or plc datatypes and their values up to a max lengh of 200 Bytes of the 
connected variables. If at least one value of an element is not identical –> set function result = 
false
Restrictions:
The attached structure must not include Strings
The attached structure can not exceed 200 bytes, because of the internal buffer size

## Functional description ##

Note The status of called commands is output in subFunctionStatus. In this case, the output value 
in status indicates which command caused the error. In this case, refer to the TIA Portal 
Online Help section for information on the respective commands.
This block compares two (structured) actual parameters and shows whether they equate to the 
same value.
Note The following differences cannot be detected with the comparison method (byte level):
• Variables of the data type Struct cannot be compared.
• For strings, there may be differences in the range between the actual length and the maximum 
length.
• With REAL numbers in the structure, a disparity can also be displayed for “same” variables.
• Variables of the type ARRAY of BOOL cannot be checked for equality with the function, because 
the command used, CountOfElements, also counts the filling elements (e.g. 8 is returned with an 
ARRAY[0..1] of BOOL).

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | FALSE: No error / TRUE: An error occurred during the execution of the FB |
| status | Word | 16#0000-16#7FFF: Status of the FB / 16#8000-16#FFFF: Error identification |
| subFunctionStatus | Word | Status or return value of called FB's, FC's and system blocks |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| variableA | Variant | First comparison variable with any data type |
| variableB | Variant | Second comparison variable with any data type |

### Return Value

- **Type:** Bool
- **Description:** FALSE: Values of comparison variables or PLC data types are different. TRUE: Values of the comparison variables are equal and PLC data types are identical.

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8201 | ERR_INPUT_TYPES_MUST_MATCH |
| 16#8202 | ERR_INPUT_TYPES_LENGTH_NOT_EQUAL |
| 16#8601 | ERR_SERIALIZE_VARIABLE_A |
| 16#8602 | ERR_SERIALIZE_VARIABLE_B |

---

# LGF_GetCalendarWeek_ISO - ISO 8601 calendar week calculation

**Type:** FUNCTION

## Description

## Short description ##

This function uses the specified date to calculate the calendar week and the number of days that have passed since the beginning of the year for ISO 8601 European countries.

## Functional description ##

Counting method for European countries in accordance with ISO 8601
•     Calendar weeks have 7 days, start on a Monday, and they are counted continuously throughout the year
•     Calendar week 1 of a year is the week that contains the first Thursday.
•     Each year has either 52 or 53 calendar weeks.
•    A year has 53 calendar weeks if the following characteristics apply:
-    A common year begins on a Thursday and ends on a Thursday.
-    A leap year begins either on a Wednesday and ends on a Thursday or it begins on a Thursday and ends on a Friday.


•    The 29th, 30th and 31st December can belong to the calendar week 1 of the following year.
•    The 1st, 2nd, and 3rd January can still belong to the last calendar week of the previous year.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| date | DTL | Date used to calculate the calendar week and days since 1 January |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| calendarDay | DInt | Days past since January 1st on given date |
| error | Bool | FALSE: No error / TRUE: An error occurred during the execution of the FB |
| status | Word | 16#0000-16#7FFF: Status of the FB / 16#8000-16#FFFF: Error identification |

### Return Value

- **Type:** DInt
- **Description:** Number of the calendar week.

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8201 | ERR_LIM_DATE Date out of the range |

---

# LGF_RandomRange_UDInt - Random UDInt Range Number Generator

**Type:** FUNCTION

## Description

## Short description ##

This function generates a random value in defined limits with each call.
The random number has the data type UDInt in the specified range.

## Functional description ##

Note The status of called commands is output in subFunctionStatus. In this case, the output value 
in status indicates which command caused the error. In this case, refer to the TIA Portal 
Online Help section for information on the respective commands.
The block generates random values that are between the specified minValue and the maxValue. 
This random value is output via the Ret_Val.The random value is formed from the nanoseconds of the current system time of the CPU. The 
byte order of this value is inverted and then converted to a UDInt.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| minValue | UDInt | Minimum value of the range of the random number - lower border |
| maxValue | UDInt | Maximum value of the range of the random number - upper border |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | Error flag |
| status | Word | Status code |
| subfunctionStatus | Word | Status or return value of called blocks |

### Return Value

- **Type:** UDInt
- **Description:** Random UDInt number in the predefined range

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_FINISHED_NO_ERROR |
| 16#8200 | ERR_MAX_LESS_MIN |
| 16#8600 | ERR_RD_SYS_T |

---

# LGF_Integration - Function Curve Area Calculator

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

The function approximately calculates the area under a function curve. The function curve is 
transferred as an analog value (LReal) which varies over time. The integral value is output on 
integral.
The implementation is based on the trapezoidal rule and uses [ms] as time base.

## Functional description ##

Note The status of called commands is output in subFunctionStatus. In this case, the output value 
in status indicates which command caused the error. In this case, refer to the TIA Portal 
Online Help section for information on the respective commands.
The integral calculation includes the summation of those trapezoidal areas that span between 
the last two function values on the “value” input and the time. The elapsed time is calculated via 
the system time of the CPU. This trapezoidal area is identical to the product of the mean value 
of the two process values and the time interval.
Note The calculation takes [ms] as time base. So the analoge value hase to use the same time 
base, e.g. [volume flow/ms].
𝐴 = 1/2 * (𝐹𝑡1 + 𝐹𝑡0) * (𝑡1 − 𝑡0) + 1/2 * (𝐹𝑡2 + 𝐹𝑡1) *(𝑡2− 𝑡1) + ...
Start the integral calculation for the inputvalue at the parameter value:
• Set the parameter enable to the value TRUE
• Set the parameter reset to the value FALSE
If the parameter enable is set to the value FALSE, the integral calculation is stopped and the 
output integral outputs the last calculated value.
If the parameter reset is set to the value TRUE, the output integral is reset to 0.0

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| enable | Bool | Enables integral calculation |
| value | LReal | Analog value of the continuous function curve, based on [ms] |
| reset | Bool | Sets the output 'integral' to '0.0' |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| integral | LReal | Integral value |
| error | Bool | Error flag |
| status | Word | Status code |
| subfunctionStatus | Word | Status or return value of called blocks |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_EXECUTION_FINISHED_NO_ERROR |
| 16#8600 | ERR_READ_SYS_TIME |

---

# LGF_SwapBlockDWord - DWord Endianness Adjuster

**Type:** FUNCTION

## Description

## Short description ##

Adjusts/ switches the endianness of multibyte data typed values.
For this to achieve, a loop will iterate through the array elements and swap the bytes 
intrinsically.

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| data | Array[*] of DWord | Contains the data values, which will be endianness adjusted |

### Return Value

- **Type:** Void
- **Description:** Void - Function has no return value

---

# LGF_KelvinToRankine - Kelvin to Rankine Converter

**Type:** FUNCTION

## Description

## Short description ##

This function converts a temperature value - from °Kelvin to °Rankine.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | Real | Temperature to be converted in °Kelvin |

### Return Value

- **Type:** Real
- **Description:** Converted temperature in °Rankine

---

# LGF_StringToTime - String to Time Converter

**Type:** FUNCTION

## Description

## Short description ##

The function converts a variable of the data type String into a variable of the system data type 
Time.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| timeValue | String | Time to be converted as string Example: 1D3H45M6S0MS |

### Return Value

- **Type:** Time
- **Description:** Converted time value Example: T#1D_3H_45M_6S

---

# LGF_PulseRelay - Pulse relay and toggle flip-flop operation

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

This block corresponds to an impulse relay or a toggle flip-flop including set and reset input.   Pulse relay, Surge relay, Toggle-Flip-Flop, Frequency divider reset is leading / prior to set or trigger

## Functional description ##

Figure: LGF_PulseRelay Signal diagram
1.   Each rising edge of the input trigger changes the Boolean value of the output out.    
2.   Each rising edge of the input set sets the Bboolean value of the output out to TRUE.    
3.   Each rising edge of the input reset sets the Boolean value of the output out to FALSE. 
4.   If the inputs set and reset are set in the same cycle, the reset input has priority.
The block can also be used as a frequency divider. If the input trigger is supplied with a fixed frequency, the output out delivers half the frequency.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| trigger | Bool | FALSE Trigger to toggle output signal (rising edge) |
| set | Bool | FALSE Set output signal. rising edge |
| reset | Bool | FALSE Reset signal, rising edge (prior to set) |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| out | Bool | Ooutput signal |

---

# LGF_IsValueInTolerance - Value tolerance range check

**Type:** FUNCTION

## Description

## Short description ##

The function checks whether a value is within a defined value range.
The value range is defined with a set point, as well as a tolerance range, around the set point in 
percent (%). The function calculates the low limit and high limit of the value range.

## Functional description ##

The setpoint and tolerance percentage variables define a value range.
The function checks whether the value is below, in or above the value range. The outputs 
belowLowLimit, Ret_Val, or overHighLimit show where the value is located.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | LReal | Value to be checked |
| setpoint | LReal | Set point |
| tolerance | LReal | Tolerance range around the set point in percent |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| overHighLimit | Bool | TRUE if the value exceeds the upper limit |
| belowLowLimit | Bool | TRUE if the value is below the lower limit |
| error | Bool | Error flag |
| status | Word | Status code |

### Return Value

- **Type:** Bool
- **Description:** TRUE if the value is in the value range

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8401 | ERR_RANGE_LIMIT_VALUES |

---

# LGF_MatrixScalarMultiplication - Matrix Scalar Multiplier

**Type:** FUNCTION

## Description

## Short description ##

This function block multiplies a matrix of the data type ARRAY[*,*] of LREAL with a scalar.
A matrix is multiplied by a scalar, thereby multiplying each matrix element by the scalar. The 
result is output in the matrixResult matrix.
Note Note that the input and output matrix must have the same number of columns and rows.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| scalar | LReal | Scalar value where the matrix is multiplied |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | Error flag |
| status | Word | Status code |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| matrixInput | Array[*, *] of LReal | Matrix to multiply |
| matrixResult | Array[*, *] of LReal | The result matrix of the multiplication |

### Return Value

- **Type:** Void
- **Description:** Void - Function has no return value

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8201 | ERR_MATRICES_LOWER_BOUND_ROWS_DONT_MATCH |
| 16#8202 | ERR_MATRICES_UPPER_BOUND_ROWS_DONT_MATCH |
| 16#8203 | ERR_MATRICES_LOWER_BOUND_COLUMNS_DONT_MATCH |
| 16#8204 | ERR_MATRICES_UPPER_BOUND_COLUMNS_DONT_MATCH |

---

# LGF_CompareLReal - LReal numbers comparison with fixed precision

**Type:** FUNCTION

## Description

## Short description ##

This function checks floating point numbers for equality, by using an approximation formula and 
a fixed precision by constant 1.0E-12 (pico)

## Functional description ##

The comparison of the LREAL numbers is based on an fixed accuracy of 1.0E-12. The 
difference between the two input values must be smaller than the PRECISION accuracy multiplied 
by one of the two input values.
Equation:
Note If your application requires a different accuracy when comparing the numbers, adapt the 
“PRECISION” constant in the function to your requirements.
Or you may use the FC LGF_CompareLRealByPrecision.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| valueA | LReal | First LREAL number to be compared. |
| valueB | LReal | Second LREAL number to be compared. |

### Return Value

- **Type:** Bool
- **Description:** FALSE: not equal, TRUE: approximately the same

---

# LGF_ExtractStringFromCharArrayAdv - Advanced String Extractor from Character Array

**Type:** FUNCTION

## Description

## Short description ##

The function extracts a String specified by a text before and after from an array of characters 
with extended options.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| textBefore | String | Text in front of the characters which has to be extracted |
| textAfter | String | Text behind the characters which has to be extracted |
| includeBeforeAfter | Bool | TRUE: textBefore and textAfter are included in the extracted string |
| startPos | DInt | Position within the array to start search from (index zero based) |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| extractedString | String | Extracted string |
| position | DInt | Position (index) within the array where text begins (index zero based) |
| length | Int | Length of text that was extracted |
| status | Word | Status of the FB |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| searchIn | Variant | Array of Character or Byte to search in |

### Return Value

- **Type:** Word
- **Description:** Return value: Status of the FB

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8200 | ERR_NO_ARRAY |
| 16#9001 | WARNING_ONLY_START |
| 16#9002 | WARNING_NOTHING_FOUND |

---

# LGF_SplitWordToBits - Word to 16-Bit Splitter

**Type:** FUNCTION

## Description

## Short description ##

This function splits a Word variable into 16 Boolean / 16 Bit variables.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| word | Word | Bit sequence to be split |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| bit15 | Bool | Output Bit 15 - MSB |
| bit14 | Bool | Output Bit 14 |
| bit13 | Bool | Output Bit 13 |
| bit12 | Bool | Output Bit 12 |
| bit11 | Bool | Output Bit 11 |
| bit10 | Bool | Output Bit 10 |
| bit9 | Bool | Output Bit 9 |
| bit8 | Bool | Output Bit 8 |
| bit7 | Bool | Output Bit 7 |
| bit6 | Bool | Output Bit 6 |
| bit5 | Bool | Output Bit 5 |
| bit4 | Bool | Output Bit 4 |
| bit3 | Bool | Output Bit 3 |
| bit2 | Bool | Output Bit 2 |
| bit1 | Bool | Output Bit 1 |
| bit0 | Bool | Output Bit 0 - LSB |

---

# LGF_StringToDTL_ISO - International Date String to DTL Converter

**Type:** FUNCTION

## Description

## Short description ##

This function converts a character string in international format with date components into the 
data type DTL.

## Functional description ##

The block reads a date as a character string and converts it to the data type DTL. The individual 
date components in the character string are separated according to the international format. The 
separator between the components in the character string is irrelevant.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| date | String | Date as a character string according to the format. Example: 22-01-2019 14:07:57.696417000. |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | An error occurred during the execution of the FB |
| status | Word | Status of the FB, Error identification |

### Return Value

- **Type:** DTL
- **Description:** The converted date and time in the format DTL

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_FINISHED_NO_ERROR |
| 16#7000 | STATUS_NO_JOB |
| 16#8201 | ERR_FORMAT_YEAR |
| 16#8202 | ERR_FORMAT_MONTH |
| 16#8203 | ERR_FORMAT_DAY |
| 16#8204 | ERR_FORMAT_HOUR |
| 16#8205 | ERR_FORMAT_MINUTE |
| 16#8206 | ERR_FORMAT_SECOND |
| 16#8207 | ERR_FORMAT_NANOSECOND |

---

# LGF_IsBigEndian - Endianness Detection Function

**Type:** FUNCTION

## Description

## Short description ##

The function detects the endianness of the executing system.

### Return Value

- **Type:** Bool
- **Description:** TRUE if big endianness is detected

---

# LGF_NthRoot - N-th root extraction

**Type:** FUNCTION

## Description

## Short description ##

This function extracts the n-th root of a given value.
The root is defined as follows:
𝑟𝑒𝑠𝑢𝑙𝑡 = 𝑟𝑜𝑜𝑡√𝑣𝑎𝑙𝑢𝑒 = 𝑣𝑎𝑙𝑢𝑒^(1/𝑟𝑜𝑜𝑡)
STEP 7 (TIA Portal) results in the following formula:
𝑟𝑒𝑠𝑢𝑙𝑡 = 𝑣𝑎𝑙𝑢𝑒 ** (1/𝑟𝑜𝑜𝑡)

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | LReal | Value from which the root should be calculated |
| root | LReal | Exponent of root |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | Error flag |
| status | Word | Status code |

### Return Value

- **Type:** LReal
- **Description:** Returns the Nth root of a value

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8200 | ERR_NEG_VAR |

---

# LGF_SwapBlockWord - Word Endianness Adjuster

**Type:** FUNCTION

## Description

## Short description ##

Adjusts/ switches the endianness of multibyte data typed values.
For this to achieve, a loop will iterate through the array elements and swap the bytes 
intrinsically.

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| data | Array[*] of Word | Contains the data values, which will be endianness adjusted |

### Return Value

- **Type:** Void
- **Description:** Void - Function has no return value

---

# LGF_ShellSort_DInt - Shell Sort for DInt Arrays

**Type:** FUNCTION

## Description

## Short description ##

This block sorts an array of type DInt with any number of elements (max. 1000) in ascending or 
descending order and returns the sorted version of the array in the same variable.

## Functional description ##

The block sorts according to the shell sort procedure. Note that the execution time of the block 
depends significantly on how many elements the array to be sorted has. The overview below 
shows several measured values of the block depending on the number of array elements.
Average steps needed for execution: 𝒪(𝑛 ⋅ log(𝑛)^2)
Table: Execution times of the block LGF_ShellSort…
Number of array elements S7-1212C DC/DC/DC S7-1516-3 PN/DP
100 approx. 11-16 ms approx. 1-2 ms
Number of array elements S7-1212C DC/DC/DC S7-1516-3 PN/DP
1000 approx. 185-205 ms approx. 10-12 ms
Note The block is executed synchronously and is not split over several PLC cycles. Thus the 
execution time has a direct effect on the PLC cycle time. Note this behavior for your project 
of the controller used and adjust the monitoring time of the controller if necessary.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| sortDirection | Bool | FALSE: Sort ascending; TRUE: Sort descending |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | An error occurred during the execution of the FB |
| status | Word | Status of the FB, Error identification |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| array | Array[*] of DInt | Array to be sorted |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8200 | ERR_NO_ARRAY |
| 16#8201 | ERR_TOO_MANY_ELEMENTS |

---

# LGF_RankineToKelvin - Rankine to Kelvin Converter

**Type:** FUNCTION

## Description

## Short description ##

This function converts a temperature value - from °Rankine to °Kelvin.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | Real | Temperature to be converted in °Rankine |

### Return Value

- **Type:** Real
- **Description:** Converted temperature in °Kelvin

---

# LGF_Impulse - Pulse Generator

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

This function generates pulses at a given frequency. The pulse is always present for one 
(control) cycle.

## Functional description ##

The function generates pulses at the output impulse with the frequency frequency.
The block always begins with a pulse and sets the next pulse after the period that has elapsed.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| frequency | Real | 0.0 |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| impulse | Bool | Impulse signal output |
| countdown | Time | Time until next pulse |

---

# LGF_DifferenceQuotientFC - Numeric Differentiation Function

**Type:** FUNCTION

## Description

## Short description ##

This function numerically differentiates a signal sampled equidistantly in time. For example, the 
velocity can be calculated from a measured locus curve, or the acceleration can be calculated 
from the measured velocity. In order to minimize the effects of a scattering measurement signal, 
this algorithm uses a compensating polynomial.
The function calculates the differentiated values acyclically.
The function reads an array that is differentiated. 𝑁 − 4 smoothed measured values can be 
calculated from N measured values. The output array contains the value 0 in the index (0,1,N-
1,N). However, replacement values can be calculated.

## Functional description ##

To calculate the difference quotient of a scattering signal, a third-degree compensation 
polynomial is first placed through the measured values. This polynomial is then differentiated. 
With this method, even a distorted input signal can be sensibly differentiated.
The difference quotient is calculated with the following formula:
y'(n)= $ \frac {y(n-2)-8y(n-1)+8y(n+1)-y(n+2)}{12 \cdot deltaT} $ 
𝑑𝑒𝑙𝑡𝑎𝑇: equidistant distance between two measured values (e.g. 1s).
The function (FC) can calculate 𝑁 − 4 differentiated and smoothed measured values from N 
measured values. The output array would be assigned with 0 in the index (0,1,N-1,N). However, 
the following formalisms can be used to calculate substitute values:
y'(n-2)= $ \frac {-125y(n-2)+136y(n-1)+48y(n)-88y(n+1)+29y(n+2)}{84\cdot deltaT} $ 
y'(n-1)= $ \frac {-38y(n-2)-2y(n-1)+24y(n)+26y(n+1)-10y(n+2)}{84\cdot deltaT} $ 
y'(n+1)= $ \frac {10y(n-2)-26y(n-1)-24y(n)+2y(n+1)+38y(n+2)}{84\cdot deltaT} $ 
y'(n+2)= $ \frac {-29y(n-2)+88y(n-1)-48y(n)-136y(n+1)+125y(n+2)}{84\cdot deltaT} $

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| deltaT | LReal | Equidistant distance between two measured values. (e.g. 1s) |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | FALSE: No error TRUE: An error occurred during the execution of the FB |
| status | Word | Status of the FB |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| values | Array[*] of LReal | Values that will be included in the differentiation. |
| derivatedValues | Array[*] of LReal | The differentiated value range. |

### Return Value

- **Type:** Void
- **Description:** Void - Function has no return value

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_FINISHED_NO_ERROR |
| 16#8200 | ERR_DELTA_T Error: Delta time `deltaT` must not be zero. |
| 16#8400 | ERR_ARRAYS_DIFFERENT Error: The Array sizes are not equal. |
| 16#8401 | ERR_NOT_ENOUGH_VALUES Error: Not enough values. |

---

# LGF_ActDeactDevice - Device Activation and Deactivation State Machine

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

LGF_ActDeactDevice implements a compact state machine to activate and monitor or deactivate 
decentral devices.
The module monitors as well the device connection and error state after activation.
It works for PN (S7-1200 / S7-1500) and DP (S7-1500) devices.

## Functional description ##

The module provides the procedure for activating and deactivating remote IO-Devices in the 
Profinet (PN, S7-1500 & S7-1200) and Profibus (DP, S7-1500) network.
The activation of the device (defined at hwId) is initiated by a rising edge at activate, after 
complete activation this is indicated at the output isActivated and deviceStateOK. After that the 
connection status is displayed at the deviceStateOK output.
The connection is monitored and in case of a failure of this of more than the set monitoring time 
timeOutStateMonitoring at the output and reported as an error. After successful recovery of the 
connection by the system, the configured time is also waited until the error is reset to ensure 
stability.
Note The connection status of the decentralized device can also be displayed in the TIA Portal 
project navigation in the PLC, which is the controller, under the item ‘Distributed I/O’, if they 
are online with the engineering system.
Deactivation of the device (defined at hwId) is initiated by a rising edge at deactivate, after 
complete activation this is indicated at the output isDeactivated.
It is possible to define the states for switching on and off, as well as the monitoring times for 
activating and deactivating and the connection monitoring.All errors are automatically reset as soon as the faulty state is eliminated.
The exception to this are errors that can only be corrected by an intervention in the software, 
such as an incorrect or non-existent hardware ID of a non-existent decentralized IO device.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| enable | Bool | Enable functionality of FB |
| activate | Bool | Rising edge: Activate device given by `hwId` |
| deactivate | Bool | Rising edge: Deactivate device given by `hwId` |
| hwId | HW_DEVICE | Hardware ID of the device which should be activated / deactivated |
| parameter | LGF_typeActDeactDeviceParameter | Parameter dataset for the function `LGF_ActDeactDevice` |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| valid | Bool | TRUE: Valid set of output values available at the FB |
| busy | Bool | TRUE: FB is not finished and new output values can be expected |
| error | Bool | TRUE: An error occurred during the execution of the FB |
| status | Word | Status and error identification |
| activating | Bool | Activation of device active |
| isActivated | Bool | Device activated |
| deactivating | Bool | Deactivating of device active |
| isDeactivated | Bool | Device deactivated |
| deviceStateOK | Bool | Device is activated and connected to IO-System |
| diagnostics | LGF_typeDiagnostics | Diagnostic structure to store and transfer diagnostic information from blocks trough the interface. |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#7000 | STATUS_NO_CALL: No job being currently processed |
| 16#7001 | STATUS_FIRST_CALL: First call after incoming new job |
| 16#7002 | STATUS_SUBSEQUENT_CALL: Subsequent call during active processing |
| 16#8600 | ERR_UNDEFINED_STATE: Due to an undefined state in state machine |
| 16#8601 | ERR_LOG2GEO / ERR_GEO2LOG: Log2Geo or Geo2Log error, check diagnostics for more info |
| 16#8640 | ERR_DEVICE_DEACTIVATING: Error during device deactivation |
| 16#8641 | ERR_DEVICE_DEACTIVATING_TIME_OUT: Deactivation timeout error |
| 16#8660 | ERR_DEVICE_ACTIVATING: Error during device activation |
| 16#8661 | ERR_DEVICE_ACTIVATING_TIME_OUT: Activation timeout error |
| 16#8662 | ERR_READ_DEVICES_STATES_DURING_ACTIVATION: Error: Read Device states (DeviceStates) during device activation |
| 16#8670 | ERR_READ_DEVICES_STATES_WHILE_ACTIVE:Error: Read Device states (DeviceStates) while device active |
| 16#8671 | ERR_DEVICE_STATE_WHILE_ACTIVE: Device states present error and is unreachable, faulty Device or IO-System |
| 16#8672 | ERR_READ_ACTIVATION_STATE_WHILE_ACTIVE:Activation state (D_ACT_DP) of device is wrong |
| 16#8690 | ERR_DISABLING_DEACT_DEVICE: Deactivation (D_ACT_DP) of device throws an error while disabling |
| 16#8691 | ERR_DISABLING_WATCHDOG:Watchdog timer expired while disabling |

## User Defined Types

### LGF_typeActDeactDeviceParameter
UDT for configuring the behavior of the activation and deactivation process.

### Members

| Name | Type | Description |
| :--- | :--- | :--- |
| timeOutActDeact | Time | Time to monitor activation and deactivation commands |
| timeOutStateMonitoring | Time | Time to monitor device state |
| enableAndDeactivate | Bool | Disable device during startup |
| enableAndActivate | Bool | Enable device during startup |
| disableAndDeactivate | Bool | Disable device during module disabling |

### LGF_typeDiagnostics
UDT for diagnostic information from blocks.

### Members

| Name | Type | Description |
| :--- | :--- | :--- |
| status | Word | Status of the block or error identification |
| subfunctionStatus | Word | Status or return value of called blocks |
| stateNumber | DInt | State in the state machine where error occurred |

---

# LGF_KelvinToFahrenheit - Kelvin to Fahrenheit Converter

**Type:** FUNCTION

## Description

## Short description ##

This function converts a temperature value - from °Kelvin to °Fahrenheit

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | Real | Temperature to be converted in °Kelvin |

### Return Value

- **Type:** Real
- **Description:** Converted temperature in °Fahrenheit

---

# LGF_FahrenheitToCelsius - Fahrenheit to Celsius Converter

**Type:** FUNCTION

## Description

## Short description ##

This function converts a temperature value - from °Fahrenheit to °Celsius.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | Real | Temperature to be converted in °Fahrenheit |

### Return Value

- **Type:** Real
- **Description:** Converted temperature in °Celsius

---

# LGF_FahrenheitToKelvin - Fahrenheit to Kelvin Converter

**Type:** FUNCTION

## Description

## Short description ##

This function converts a temperature value - from °Fahrenheit to °Kelvin.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | Real | Temperature to be converted in °Fahrenheit |

### Return Value

- **Type:** Real
- **Description:** Converted temperature in °Kelvin

---

# LGF_JulianTimeToDTL - Julian Date to DTL Time Converter

**Type:** FUNCTION

## Description

## Short description ##

This function converts a given Julian Date (regular or modified) of data type LReal (Double) to a 
date and time of data type DTL.
The timestamp is calculated based on UTC. This means that the time zone is not considered.
Only times after 01/01/1990 are permitted.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| julianDate | LReal | Julian date to convert (standard or modified, depends on isModifiedDate) |
| isModifiedDate | Bool | TRUE: julianDate is the modified Julian date FALSE: julianDate is the regular Julian date |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | An error occurred during the execution of the FB |
| status | Word | Status of the FB, Error identification |

### Return Value

- **Type:** DTL
- **Description:** Converted time (Date and time). In case of Error DTL default value

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#6001 | WARN_CONVERSION_LIMIT |
| 16#8000 | ERR_TIME_BEFORE_1990 |

---

# LGF_BitToggle - Bit toggle operation in DWORD

**Type:** FUNCTION

## Description

## Short description ##

This block toggles (from TRUE to FALSE and viceversa) a bit at a predefined position in a variable of the data type DWORD.
Alternatively, Word and Byte can be used instead of DWord by converting the passed
parameter with, for example, BYTE_TO_DWORD and the result with DWORD_TO_BYTE

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | DWord | Tag where the bit has to be toggled |
| bitNo | USInt | Bit number to be toggled in the “value” parameter. |

### Return Value

- **Type:** DWord
- **Description:** Tag with toggled bit

---

# LGF_Frequency - Frequency Signal Generator

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

This function generates a signal that changes between the values FALSE and TRUE depending on 
a defined frequency and a pulse pause ratio.

## Functional description ##

The clock output is a Boolean value that toggles at the desired frequency. The pulsePauseRatio
input is used to set the pulse pause ratio.
The output countdown outputs the remaining time of the current state of clock.
If the desired frequency or pulse pause ratio is less than or equal to 0.0, the output clock = 
FALSE and countdown = 0s.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| frequency | Real | 0.0 |
| pulsePauseRatio | Real | 1.0 |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| clock | Bool | Output changes with defined frequency. |
| countdown | Time | Remaining time of the current clock state. |

---

# LGF_SplitDWordToBits - DWord to 32-Bit Splitter

**Type:** FUNCTION

## Description

## Short description ##

This function splits a DWord variable into 32 Boolean / 32 Bit variables.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| doubleWord | DWord | Bit sequence to be split |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| bit31 | Bool | Output Bit 31 - MSB |
| bit30 | Bool | Output Bit 30 |
| bit29 | Bool | Output Bit 29 |
| bit28 | Bool | Output Bit 28 |
| bit27 | Bool | Output Bit 27 |
| bit26 | Bool | Output Bit 26 |
| bit25 | Bool | Output Bit 25 |
| bit24 | Bool | Output Bit 24 |
| bit23 | Bool | Output Bit 23 |
| bit22 | Bool | Output Bit 22 |
| bit21 | Bool | Output Bit 21 |
| bit20 | Bool | Output Bit 20 |
| bit19 | Bool | Output Bit 19 |
| bit18 | Bool | Output Bit 18 |
| bit17 | Bool | Output Bit 17 |
| bit16 | Bool | Output Bit 16 |
| bit15 | Bool | Output Bit 15 |
| bit14 | Bool | Output Bit 14 |
| bit13 | Bool | Output Bit 13 |
| bit12 | Bool | Output Bit 12 |
| bit11 | Bool | Output Bit 11 |
| bit10 | Bool | Output Bit 10 |
| bit9 | Bool | Output Bit 9 |
| bit8 | Bool | Output Bit 8 |
| bit7 | Bool | Output Bit 7 |
| bit6 | Bool | Output Bit 6 |
| bit5 | Bool | Output Bit 5 |
| bit4 | Bool | Output Bit 4 |
| bit3 | Bool | Output Bit 3 |
| bit2 | Bool | Output Bit 2 |
| bit1 | Bool | Output Bit 1 |
| bit0 | Bool | Output Bit 0 - LSB |

---

# LGF_MergeBitsToWord - 16-Bit to Word Merger

**Type:** FUNCTION

## Description

## Short description ##

This function merge 16 Bits / 16 Boolean variables into one Word variable.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| bit15 | Bool | Input Bit 15 - MSB |
| bit14 | Bool | Input Bit 14 |
| bit13 | Bool | Input Bit 13 |
| bit12 | Bool | Input Bit 12 |
| bit11 | Bool | Input Bit 11 |
| bit10 | Bool | Input Bit 10 |
| bit9 | Bool | Input Bit 9 |
| bit8 | Bool | Input Bit 8 |
| bit7 | Bool | Input Bit 7 |
| bit6 | Bool | Input Bit 6 |
| bit5 | Bool | Input Bit 5 |
| bit4 | Bool | Input Bit 4 |
| bit3 | Bool | Input Bit 3 |
| bit2 | Bool | Input Bit 2 |
| bit1 | Bool | Input Bit 1 |
| bit0 | Bool | Input Bit 0 - LSB |

### Return Value

- **Type:** Word
- **Description:** Composite Bit sequence stored as Word variable

---

# LGF_MergeBytesToWord - 2-Byte to Word Merger

**Type:** FUNCTION

## Description

## Short description ##

This function merge 2 Byte variables into one Word variable

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| byte1 | Byte | Input Byte 1 - MSB |
| byte0 | Byte | Input Byte 0 - LSB |

### Return Value

- **Type:** Word
- **Description:** Composite Byte sequence stored as Word variable

---

# LGF_RectangleCI - Rectangle Signal Generator

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

This function generates a rectangular signal profile. For this it uses the time interval of the 
calling Cyclic Interrupt OB.

## Functional description ##

Note The status of called commands is output in subFunctionStatus. In this case, the output value 
in status indicates which command caused the error. In this case, refer to the TIA Portal 
Online Help section for information on the respective commands.
The block calculates the values for a rectangular signal profile, which is output to the output 
parameter value.
The amplitude, the offset in the Y-direction, the period, and the phase shift can be set at the 
input parameters.
The input parameter reset resets the signal profile. At the value output parameter, the value 0 is 
output as long as reset is set to TRUE.
The block must be called in a cyclic interrupt OB. The time interval of the calling cyclic interrupt 
OB is determined in the FB with the command QRY_CINT. For this, the constant name of the 
calling cyclic interrupt OB must be interconnected at the input parameter callOB.
The number of calculated values of the signal profile per period duration is calculated as follows:
𝑄𝑢𝑎𝑛𝑡𝑖𝑡𝑦𝑉𝑎𝑙𝑢𝑒𝑠 =
𝑃𝑒𝑟𝑖𝑜𝑑𝑑𝑢𝑟𝑎𝑡𝑖𝑜𝑛
/𝑇𝑖𝑚𝑒𝑖𝑛𝑡𝑒𝑟𝑣𝑎𝑘𝐶𝑦𝑐𝑙𝑖𝑐𝑖𝑛𝑡𝑒𝑟𝑟𝑢𝑝𝑡𝑂𝐵
Note To obtain a continuous signal profile of the curve, the time interval of the cyclic interrupt OB 
should not be selected too large depending on the period duration.
The Figure below shows the signal profile of the calculated values.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| amplitude | Real | 1.0 |
| offset | Real | 0.0 |
| periode | UDInt | 1000 |
| phaseShift | Real | 0.0 |
| callOB | OB_CYCLIC |  |
| reset | Bool | FALSE |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | Real | Current value of the rectangular signal. |
| error | Bool | FALSE: No error |
| status | Word | 16#0000-16#7FFF: Status of the FB 16#8000-16#FFFF: Error identification |
| subFunctionStatus | Word | Status or return value of called FB's, FC's and system blocks |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_FINISHED_NO_ERROR |
| 16#8600 | ERR_OB_UNAVAILABLE |
| 16#8601 | ERR_QRY_CINT |

---

# LGF_ShellSort_LReal - Shell Sort for LReal Arrays

**Type:** FUNCTION

## Description

## Short description ##

This block sorts an array of type LReal with any number of elements (max. 1000) in ascending 
or descending order and returns the sorted version of the array in the same variable.

## Functional description ##

The block sorts according to the shell sort procedure. Note that the execution time of the block 
depends significantly on how many elements the array to be sorted has. The overview below 
shows several measured values of the block depending on the number of array elements.
Average steps needed for execution: 𝒪(𝑛 ⋅ log(𝑛)^2)
Table: Execution times of the block LGF_ShellSort…
Number of array elements S7-1212C DC/DC/DC S7-1516-3 PN/DP
100 approx. 11-16 ms approx. 1-2 ms
1000 approx. 185-205 ms approx. 10-12 ms
Note The block is executed synchronously and is not split over several PLC cycles. Thus the 
execution time has a direct effect on the PLC cycle time. Note this behavior for your project 
of the controller used and adjust the monitoring time of the controller if necessary.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| sortDirection | Bool | FALSE: Sort ascending; TRUE: Sort descending |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | An error occurred during the execution of the FB |
| status | Word | Status of the FB, Error identification |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| array | Array[*] of LReal | Array to be sorted |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8200 | ERR_NO_ARRAY |
| 16#8201 | ERR_TOO_MANY_ELEMENTS |

---

# LGF_SinusCI - Sinusoidal Signal Generator

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

This function generates a sinusoidal signal profile. For this it uses the time interval of the calling 
Cyclic Interrupt OB.

## Functional description ##

Note The status of called commands is output in subFunctionStatus. In this case, the output value 
in status indicates which command caused the error. In this case, refer to the TIA Portal 
Online Help section for information on the respective commands.
The block calculates the values for a sinusoidal signal profile, which is output to the output 
parameter value.
The amplitude, the offset in the Y-direction, the period (in ms) and the phase shift (in ms) can 
be set at the input parameters.
The input parameter reset resets the signal profile. At the value output parameter, the value 0 is 
output as long as reset is set to TRUE.
The block must be called in a cyclic interrupt OB. The time interval of the calling cyclic interrupt 
OB is determined in the FB with the command QRY_CINT. For this, the constant name of the 
calling cyclic interrupt OB must be interconnected at the input parameter callOB.
The number of calculated values of the signal profile per period duration is calculated as follows:
𝑄𝑢𝑎𝑛𝑡𝑖𝑡𝑦𝑉𝑎𝑙𝑢𝑒𝑠 =
𝑃𝑒𝑟𝑖𝑜𝑑𝑑𝑢𝑟𝑎𝑡𝑖𝑜𝑛
/𝑇𝑖𝑚𝑒𝑖𝑛𝑡𝑒𝑟𝑣𝑎𝑘𝐶𝑦𝑐𝑙𝑖𝑐𝑖𝑛𝑡𝑒𝑟𝑟𝑢𝑝𝑡𝑂𝐵
Note To obtain a continuous signal profile of the curve, the time interval of the cyclic interrupt OB 
should not be selected too large depending on the period duration.The Figure below shows the signal profile of the calculated values.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| amplitude | Real | 1.0 |
| offset | Real | 0.0 |
| periode | UDInt | 1000 |
| phaseShift | Real | 0.0 |
| callOB | OB_CYCLIC |  |
| reset | Bool | FALSE |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | Real | Current value of the sinusoidal signal. |
| error | Bool | FALSE: No error |
| status | Word | 16#0000-16#7FFF: Status of the FB 16#8000-16#FFFF: Error identification |
| subFunctionStatus | Word | Status or return value of called FB's, FC's and system blocks |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_FINISHED_NO_ERROR |
| 16#8600 | ERR_OB_UNAVAILABLE |
| 16#8601 | ERR_QRY_CINT |

---

# LGF_IsGermanHoliday - German public holiday detection

**Type:** FUNCTION

## Description

## Short description ##

The function determines whether a given date is a public holiday.
All public holidays in Germany are taken into account.
Holidays that are NOT uniform nationwide can be switched on or off

## Functional description ##

The block calculates the public holiday calendar of the year for a given date and displays whether the given date is a public holiday.
Optionally, holidays that are not uniform nationwide, such as Epiphany (Three Kings), can be taken into account via the appropriate input parameters in the block.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| date | DTL | Date, which has to be evaluated |
| threeKings | Bool | Three Kings |
| roseMonday | Bool | Rose Monday |
| ascension | Bool | Ascension |
| corpusChristi | Bool | Corpus Christi |
| augsburgerFriedensfest | Bool | Augsburger Friedensfest |
| assumptionOfMary | Bool | Assumption Of Mary |
| reformationDay | Bool | Reformation Day |
| allSaintDay | Bool | All Saint Day |
| bussUndBettag | Bool | Day of Prayer and Repentance (Buss und Bettag) |

### Return Value

- **Type:** Bool
- **Description:** If the date at the input parameter is a public holiday - returning TRUE, otherwise returning FALSE

---

# LGF_GrayToBinary - Gray to Binary Code Converter

**Type:** FUNCTION

## Description

## Short description ##

This function converts a gray coded value into a binary coded value.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| variableGray | DWord | Gray coded value to convert to binary value |

### Return Value

- **Type:** DWord
- **Description:** Binary value

---

# LGF_RandomRange_Real - Random Real Range Number Generator

**Type:** FUNCTION

## Description

## Short description ##

This function generates a random value in defined limits with each call.
The random number has the data type Real in the specified range.

## Functional description ##

Note The status of called commands is output in subFunctionStatus. In this case, the output value 
in status indicates which command caused the error. In this case, refer to the TIA Portal 
Online Help section for information on the respective commands.
The block generates random values that are between the specified minValue and the maxValue. 
This random value is output via the Ret_Val.The random value is formed from the nanoseconds of the current system time of the CPU. The byte order of this value is inverted and then converted to a floating point.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| minValue | Real | Minimum value of the range of the random number - lower border |
| maxValue | Real | Maximum value of the range of the random number - upper border |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | Error flag |
| status | Word | Status code |
| subfunctionStatus | Word | Status or return value of called blocks |

### Return Value

- **Type:** Real
- **Description:** Random Real number in the predefined range

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_FINISHED_NO_ERROR |
| 16#8200 | ERR_MAX_LESS_MIN |
| 16#8600 | ERR_RD_SYS_T |

---

# LGF_Boxplot_LReal - Boxplot Calculation for Real Data

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

If you want to get an overview of existing data, you can use a Boxplot diagram. A Boxplot shows 
you in which area the data is located and how it is distributed over this area. A Boxplot consists 
of the following parameters:
• Minimum (smallest occurring value of the sample)
• Lower or first quartile (below this value are 25% of the sample values)
• Median or second quartile (below this value are 50% of the sample values)
• Upper or third quartile (below this value are 75% of the sample values)
• Maximum (largest occurring value of the sample)
Figure: Boxplot

## Functional description ##

The block sorts the data series and then calculates the so-called “five-point summary”:
Table: Five-point summary
Characteristic value of the five-point summary Output parameter of the block
Minimum (smallest occurring value of the sample) min
Lower or first quartile (below this value are 25% of 
the sample values)
q25
Median or second quartile (below this value are 
50% of the sample values)
median
Upper or third quartile (below this value are 75% of 
the sample values)
q75
Maximum (largest occurring value of the sample) max
If outlier detection is activated, the block first calculates the limits. From these limit values, the 
values are recognized as outliers:

The block then calculates new values for the parameters max and min, which lie within the outlier 
limits. The outliers are counted and output as a percentage.
To make it easier to judge how the data is distributed, the block also calculates the skew. The 
skewness lies between the values -1 and 1 with the following meaning:
• -1: extremely left skewed distribution
• 0: symmetrical distribution
• 1: extreme right-skew distribution
The elements of the passed array are sorted in ascending order by the block. The 
LGF_Shellsort_LReal block is used for sorting.
The parameters are calculated as follows:
Table: Boxplot formulas Parameters Formula

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| execute | Bool | Activation of the calculation with each positive edge. |
| rangeOutlier | LReal | Outlier detection parameter. |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | An error occurred during the execution of the FB |
| status | Word | Status of the FB |
| subfunctionStatus | Word | Status or return value of called FB's, FC's and system blocks |
| outlierMax | LReal | Upper outliers in % |
| max | LReal | Maximum Value, not an outlier. |
| q75 | LReal | 3rd quartile or Q75 of the data series. |
| median | LReal | 2nd quartile or Median of the data series. |
| q25 | LReal | 1st quartile or Q25 of the data series. |
| min | LReal | Minimum Value, not an outlier. |
| outlierMin | LReal | Lower outliers in % |
| skewness | LReal | Skewness of the data series. |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| values | Array[*] of LReal | The array containing the data series for calculation |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_EXECUTION_FINISHED |
| 16#7000 | STATUS_NO_CALL |
| 16#7001 | STATUS_FIRST_CALL |
| 16#8200 | ERR_NEG_ARR_BOUND |
| 16#8600 | ERR_SHELL_SORT |
| 16#9101 | ERR_RANGE_NOT_OK |

---

# LGF_ExtractStringFromCharArray - String Extractor from Character Array

**Type:** FUNCTION

## Description

## Short description ##

The function extracts a String specified by a text before and after from an array

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| textBefore | String | Text in front of the characters which has to be extracted |
| textAfter | String | Text behind the characters which has to be extracted |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| extractedString | String | Extracted string |
| status | Word | Status of the FB |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| searchIn | Variant | Array of Character or Byte to search in |

### Return Value

- **Type:** Word
- **Description:** Status of the FB

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_TEXT_FOUND |
| 16#8200 | ERR_NO_ARRAY |
| 16#9001 | WARNING_ONLY_START |
| 16#9002 | WARNING_NOTHING_FOUND |

---

# LGF_IsParityOdd - Odd Parity Checker for DWord

**Type:** FUNCTION

## Description

## Short description ##

The function checks whether the parity of the input variable of type DWord is odd. The return 
value is set to TRUE if the number of bits that are assigned TRUE in the sequence is odd.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| doubleWord | DWord | Variable for which the parity is to be determined. |

### Return Value

- **Type:** Bool
- **Description:** TRUE: When the number of bits that are assigned `TRUE` is odd

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |

---

# LGF_SplitByteToBits - Byte to 8-Bit Splitter

**Type:** FUNCTION

## Description

## Short description ##

This function splits a Byte variable into 8 Boolean / 8 Bit variables.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| byte | Byte | Bit sequence to be split |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| bit7 | Bool | Output Bit 7 - MSB |
| bit6 | Bool | Output Bit 6 |
| bit5 | Bool | Output Bit 5 |
| bit4 | Bool | Output Bit 4 |
| bit3 | Bool | Output Bit 3 |
| bit2 | Bool | Output Bit 2 |
| bit1 | Bool | Output Bit 1 |
| bit0 | Bool | Output Bit 0 - LSB |

---

# LGF_MatrixCompare - Matrix Comparator

**Type:** FUNCTION

## Description

## Short description ##

This function compares two matrices of the data type ARRAY[*,*] of LREAL of equal size.
If both matrices are identical, the return value of the function is set to TRUE.
Note Note that all input matrices must have the same lower and upper limit, and, therefore, the 
same number of columns and rows.

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | Error flag |
| status | Word | Status code |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| matrix1 | Array[*, *] of LReal | First Matrix |
| matrix2 | Array[*, *] of LReal | Second Matrix |

### Return Value

- **Type:** Bool
- **Description:** TRUE: Both matrices are identical.

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8200 | ERR_MATR1_LOWBOUND_ROWS_MATR2_LOWBOUND_ROWS |
| 16#8201 | ERR_MATR1_LOWBOUND_COLUMNS_MATR2_LOWBOUND_COLUMNS |
| 16#8202 | ERR_MATR1_UPPBOUND_ROWS_MATR2_UPPBOUND_ROWS |
| 16#8203 | ERR_MATR1_UPPBOUND_COLUMNS_MATR2_UPPBOUND_COLUMNS |

---

# LGF_LimRateOfChangeAdvancedCI - Advanced Rate of Change Limiter

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

The function LGF_LimRateOfChangeAdvanced limits the rate of change of an input variable. Jump 
functions become ramp functions. In addition, the block has various operating modes.

## Functional description ##

Note The status of called commands is output in subFunctionStatus. In this case, the output value 
in status indicates which command caused the error. In this case, refer to the TIA Portal 
Online Help section for information on the respective commands.
For the positive/negative value range, two rates of change in each case for the ramp (rising and 
falling values) can be parameterized. The following operating modes can be selected via control 
inputs:
• Restart
• Pre-assigning an output
• Normal operation (automatic)
• Switch through controlled variable (manual)
• Tracking
The output variable can be limited through two parametrize able limits. An active limitation of the 
rate of change of a ramp, as well as an active limitation of the output variable are reported via 
outputs.
The time interval of the calling cyclic interrupt OB is determined by interconnecting the calling 
cyclic interrupt OB at the input parameter callOB.
Restart
At restart reset = TRUE, the output outputValue is reset to 0.0.
If enDefaultOutValue = TRUE is set, defaultOutValue is output. All signal outputs are set to 
FALSE.
Pre-assigning an output
If enDefaultOutValue = TRUE is set, the value at defaultOutValue is output. When changing 
from TRUE to FALSE, outputValue is ramped from defaultOutValue to autoValue. When changing 
from FALSE to TRUE, the output outputValue immediately jumps to defaultOutValue.
Normal operation
The ramps are straight lines of limitation and are based on a rate of change per second; if, for 
example, the parameter setPosUpRateLim = 10.0 is assigned, then at a sampling time of 
1s/100ms/10ms, 10.0/1.0/0.1 will be added to outputValue at each block call, if autoValue > 
outputValue, until autoValue is reached.
The limitation of the rate of change can be parameterized in both positive and negative ranges 
for the increase and decrease.
Table: Marking of the ramps
Parameters Ramp
setPosUpRateLim outputValue > 0.0 and |outputValue| rising
setPosDownRateLim
outputValue > 0.0 and |outputValue| falling
setNegUpRateLim outputValue < 0.0 and |outputValue| rising
setNegDownRateLim
outputValue < 0.0 and |outputValue| falling
If the ramps are not parameterized (setPosUpRateLim, setPosDownRateLim, setNegUpRateLim, 
and setNegDownRateLim equal 0.0), the output remains at 0.0 and normal operation is disabled.
Tracking
If the input track = TRUE is set, the input variable autoValue is interconnected directly to the 
output variable outputValue. Thus, jumps of the input variable will also be output.
Switch through controlled variable
If manOp = TRUE is set, the controlled variable manualValue is interconnected directly to the 
output variable outputValue.
In this operating mode, the parameterization of the ramps or the high/low limitation of the output 
variable, and the pre-assignment of the output, are ineffective.
When changing from TRUE to FALSE, the output outputValue is ramped again after autoValue.
As soon as the value range between the low and high limits is reached, the high and low limits 
are reactivated.
Figure: Ramp function sequence, operating modes

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| autoValue | LReal | Signal to be processed and limited in its rate of change |
| manualValue | LReal | Manually controlled output value |
| posUpRateLim | LReal | Rate of change per second for the rising ramp in the positive value range |
| posDownRateLim | LReal | Rate of change per second for the falling ramp in the positive value range |
| negUpRateLim | LReal | Rate of change per second for the rising ramp in the negative value range |
| negDownRateLim | LReal | Rate of change per second for the falling ramp in the negative value range |
| highLim | LReal | High limit value |
| lowLim | LReal | Low limit value |
| defaultOutValue | LReal | Value for pre-assignment of the output variable |
| enDefaultOutValue | Bool | Assign default output value |
| track | Bool | Follow / tracking of Input variable |
| manOp | Bool | Manual mode on |
| reset | Bool | Complete restart of function |
| callOB | OB_CYCLIC | Calling wake-alarm interrupt OB |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| outputValue | LReal | Output variable |
| posUpRateLim | Bool | Rise limitation in positive range tripped |
| posDownRateLim | Bool | Down rate limit in positive range reached |
| negUpRateLim | Bool | Up rate limit in negative range reached |
| negDownRateLim | Bool | Down rate limit in negative range reached |
| highLim | Bool | High limit reached |
| lowLim | Bool | Low limit reached |
| error | Bool | Error occurred during the execution of the FB |
| status | Word | Status of the FB |
| subfunctionStatus | Word | Status or return value of called FB's, FC's and system blocks |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_FINISHED_NO_ERROR |
| 16#8200 | ERR_NEG_RATE_LIM |
| 16#8202 | ERR_NEG_RATE_OF_CHANGE |
| 16#8600 | ERR_QRY_CINT |
| 16#8601 | ERR_OB_UNAVAILABLE |

## User Defined Types

### LGF_typeNonLinSetpoints
Data type for setup a setpoint table for function

### Members

| Name | Type | Description |
| :--- | :--- | :--- |
| inputValue | LReal | Input value to be interpolated |
| outputValue | LReal | Corresponding interpolated value |

---

# LGF_EncodeUtf8 - WString to UTF-8 Byte Stream Encoder

**Type:** FUNCTION

## Description

## Short description ##

Encodes a WString into an UTF-8 encoded byte stream.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| sourceString | WString | Character that shall be converted to UTF-8 |
| startPos | DInt | Position in encoded byte stream to start insert encoded WChars (Array lower bound is added) |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| bytesUsed | UInt | Number of Bytes converted. Ranges from 1 to 3. |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| encodedByteStream | Array[*] of Byte | UTF-8 conformant byte sequence. |

### Return Value

- **Type:** Word
- **Description:** Status of the FC, Erroridentification

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8201 | ERR_START_POS_OUTSIDE |
| 16#8202 | ERR_COUNT_EXCEEDS_BOUNDS |

---

# LGF_TriangleCI - Triangular Signal Generator

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

This function generates a triangular signal profile. For this it uses the time interval of the calling 
Cyclic Interrupt OB.

## Functional description ##

Note The status of called commands is output in subFunctionStatus. In this case, the output value 
in status indicates which command caused the error. In this case, refer to the TIA Portal 
Online Help section for information on the respective commands.
The block calculates the values for a triangular signal profile, which is output to the output 
parameter value.
The amplitude, the offset in the Y-direction, the period, and the phase shift can be set at the 
input parameters.
The input parameter reset resets the signal profile. At the value output parameter, the value 0 is 
output as long as reset is set to TRUE.
The block must be called in a cyclic interrupt OB. The time interval of the calling cyclic interrupt 
OB is determined in the FB with the command QRY_CINT. For this, the constant name of the 
calling cyclic interrupt OB must be interconnected at the input parameter callOB.
The number of calculated values of the signal profile per period duration is calculated as follows:
𝑄𝑢𝑎𝑛𝑡𝑖𝑡𝑦𝑉𝑎𝑙𝑢𝑒𝑠 =
𝑃𝑒𝑟𝑖𝑜𝑑𝑑𝑢𝑟𝑎𝑡𝑖𝑜𝑛
/𝑇𝑖𝑚𝑒𝑖𝑛𝑡𝑒𝑟𝑣𝑎𝑘𝐶𝑦𝑐𝑙𝑖𝑐𝑖𝑛𝑡𝑒𝑟𝑟𝑢𝑝𝑡𝑂𝐵
Note To obtain a continuous signal profile of the curve, the time interval of the cyclic interrupt OB 
should not be selected too large depending on the period duration.The Figure below shows the signal profile of the calculated values.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| amplitude | Real | 1.0 |
| offset | Real | 0.0 |
| periode | UDInt | 1000 |
| phaseShift | Real | 0.0 |
| callOB | OB_CYCLIC |  |
| reset | Bool | FALSE |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | Real | Current value of the triangular signal. |
| error | Bool | FALSE: No error |
| status | Word | 16#0000-16#7FFF: Status of the FB 16#8000-16#FFFF: Error identification |
| subFunctionStatus | Word | Status or return value of called FB's, FC's and system blocks |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_FINISHED_NO_ERROR |
| 16#8600 | ERR_OB_UNAVAILABLE |
| 16#8601 | ERR_QRY_CINT |

---

# LGF_BitCount - DWORD bit count operation

**Type:** FUNCTION

## Description

## Short description ##

This block counts in a variable of type DWord how many bits are set (TRUE) and how many are 
not set (FALSE) and outputs the number at the outputs.
Instead of DWord, Word and Byte can also be used by converting the past parameter with e.g. 
BYTE_TO_DWORD and connecting the corresponding bit length of the data type at the 
parameter “numberOfBits”.
Byte=8, Word=16, DWord=32

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | DWord | Tag where the bit states has to be counted |
| numberOfBits | USInt | Number of bits in input tag "value" (bit size of Datatype), in case of Byte=8, Word=16, DWord=32 |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| countBitsFalse | USInt | Number of bits are FALSE in input tag "value" |
| countBitsTrue | USInt | Number of bits are TRUE in input tag "value" |

### Return Value

- **Type:** Void
- **Description:** Void - Function has no return value

---

# LGF_CalcCRC16Advanced - Advanced CRC-16 Calculator

**Type:** FUNCTION

## Description

## Short description ##

The CRC calculation is used for error detection at data transmission. The result of a calculation 
returns a CRC value via the data sent. The receiver detects a faulty transmission due to the 
unequal CRC value. The function LGF_CalcCRC16Advanced uses 16 bits as the generator 
polynomial (mask) and the parameters finalXorValue, reflectInput, and reflectResult.

## Functional description ##

The function calculates the CRC value from a data stream of any size. The data stream is 
composed of the individual elements of the array at the input/output parameter array. The start 
value initValue and the generator polynomial mask can be freely selected.
Via the Boolean input parameters reflectInput and reflectResult, you may optionally mirror 
the bits of the input data or the CRC value. An XOR operation is also performed with the CRC 
value at the end and the value finalXorValue.
The input noOfELements can be used to specify the desired number of elements for calculation, it 
applies:
𝑁𝑢𝑚𝑏𝑒𝑟𝑂𝑓𝐸𝑙𝑒𝑚𝑒𝑛𝑡𝑠 <= (𝐴𝑟𝑟𝑎𝑦𝑈𝑝𝑝𝑒𝑟𝐿𝑖𝑚𝑖𝑡 − 𝐴𝑟𝑟𝑎𝑦𝐿𝑜𝑤𝑒𝑟𝑈𝑛𝑑𝑒𝑟𝐿𝑖𝑚𝑖𝑡 + 1)
Note Various online tools are available for calculating the CRC values. The function of the block 
was tested with the following online tool, since it supports the input parameters mask
(Polynomial) and initValue (Initial Value):
http://www.sunshine2k.de/coding/javascript/crc/crc_js.html

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| initValue | Word | Start value for the calculation |
| mask | Word | Generator polynomial for the calculation |
| finalXorValue | Word | Value for final XOR operation |
| reflectInput | Bool | Mirror the bits within the input byte |
| reflectResult | Bool | Mirror the order of the bits within the result |
| noOfElements | UInt | Number of elements to be used in CRC calculation |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | Error flag |
| status | Word | Status code |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| array | Array[*] of Byte | Data stream for which the CRC value will be calculated |

### Return Value

- **Type:** Word
- **Description:** Calculated CRC value

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8400 | ERR_NO_OF_ELEMENTS |

---

# LGF_TaddrToString - TADDR_Param to String Converter

**Type:** FUNCTION

## Description

## Short description ##

The system data type TADDR_Param contains address information consisting of an IPV4 address 
and the port number.
The LGF_TaddrToString function converts a TADDR_Param system data type variable to a String
data type variable.

## Functional description ##

The function converts the IPV4 address with or without port number. The system data type 
TADDR_Param is a structured data type. This structure contains the variable REM_PORT_NR. If this 
variable is 0, no port is written to the parameter Ret_Val.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| ipAdressTaddr | TADDR_Param | IP-Address and Port number to convert into string |

### Return Value

- **Type:** String
- **Description:** IP-Address and Port number as string

---

# LGF_StringToDTL_DE - German Traditional Date String to DTL Converter

**Type:** FUNCTION

## Description

## Short description ##

This function converts a character string in the traditional format (DE) with date components into 
the data type DTL.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| date | String | Date as a character string according to the format. Example: 22-01-2019 14:07:57.696417000. |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | An error occurred during the execution of the FB |
| status | Word | Status of the FB, Error identification |

### Return Value

- **Type:** DTL
- **Description:** The converted date and time in the format DTL

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_FINISHED_NO_ERROR |
| 16#7000 | STATUS_NO_CURRENT_JOBS |
| 16#8201 | ERR_FORMAT_YEAR |
| 16#8202 | ERR_FORMAT_MONTH |
| 16#8203 | ERR_FORMAT_DAY |
| 16#8204 | ERR_FORMAT_HOUR |
| 16#8205 | ERR_FORMAT_MINUTE |
| 16#8206 | ERR_FORMAT_SECOND |
| 16#8207 | ERR_FORMAT_NANOSECOND |

---

# LGF_FloatingAverage - Moving Average Calculation Function Block

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

This function calculates a moving arithmetic mean value from REAL values. This method can be 
used to smooth data series. The values can be read in cyclically or triggered.

## Functional description ##

Note The block LGF_FloatingAverage does not query the data type for the input parameter value. 
For data types other than REAL, either an implicit conversion is performed automatically or 
an error is generated during compilation.
You can find further information in the Chapter “Overview of Data Type Conversion” in the 
Online Help section of the TIA Portal or under:
https://support.industry.siemens.com/cs/ww/en/view/109773506/100611494667
The block calculates the (moving) mean value based on the set window width. The window 
width indicates the maximum number of values read in last. After the maximum number of 
values has been read, the output windowSizeReached is set and each newly read value replaces 
the oldest value (FIFO principle).
Two options are available for reading the values. With the input cyclicExecution, the values are 
read and calculated cyclically. With the trigger input, the values are read in and calculated with 
each pulse.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| cyclicExecution | Bool | TRUE: cyclic operation, trigger not in use |
| trigger | Bool | Read in `value` with every pulse at input `trigger` |
| value | LReal | Value/s from which the moving average is to be determined. |
| windowSize | Int | Window length for sliding averaging in the range from 1..100. The standard value is 100. |
| reset | Bool | TRUE: The block is reset and the calculation starts again. |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| average | LReal | Moving / Floating average |
| windowSizeReached | Bool | FALSE: Maximum window width not yet reached, TRUE: Maximum window width reached |
| error | Bool | FALSE: No error, TRUE: An error occurred during the execution of the FB |
| status | Word | Status of the FB and error identification. |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_FINISHED_NO_ERROR: Execution finished without errors |
| 16#8200 | ERR_WRONG_WINDOW_SIZE: Incorrect window size/width set. |

---

# LGF_CalcCRC32 - CRC-32 Calculator

**Type:** FUNCTION

## Description

## Short description ##

The CRC calculation is used for error detection at data transmission. The result of a calculation 
returns a CRC value via the data sent. The receiver detects a faulty transmission due to the 
unequal CRC value. The function LGF_CalcCRC32 uses 32 bits as the generator polynomial 
(mask).

## Functional description ##

The function calculates the CRC value from a data stream of any size. The data stream is 
composed of the individual elements of the array at the input/output parameter array. The start 
value initValue and the generator polynomial mask can be freely selected.
The input noOfELements can be used to specify the desired number of elements for calculation, it 
applies:
𝑁𝑢𝑚𝑏𝑒𝑟𝑂𝑓𝐸𝑙𝑒𝑚𝑒𝑛𝑡𝑠 <= (𝐴𝑟𝑟𝑎𝑦𝑈𝑝𝑝𝑒𝑟𝐿𝑖𝑚𝑖𝑡 − 𝐴𝑟𝑟𝑎𝑦𝐿𝑜𝑤𝑒𝑟𝑈𝑛𝑑𝑒𝑟𝐿𝑖𝑚𝑖𝑡 + 1)
Note Various online tools are available for calculating the CRC values. The function of the block 
was tested with the following online tool, since it supports the input parameters mask
(Polynomial) and initValue (Initial Value):
http://www.sunshine2k.de/coding/javascript/crc/crc_js.html

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| initValue | DWord | Start value for the calculation |
| mask | DWord | Generator polynomial for the calculation |
| noOfElements | UInt | Number of elements to be used in CRC calculation |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | Error flag |
| status | Word | Status code |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| array | Array[*] of Byte | Data stream for which the CRC value will be calculated |

### Return Value

- **Type:** DWord
- **Description:** Calculated CRC value

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8400 | ERR_NO_OF_ELEMENTS |

---

# LGF_GetCalendarWeek_US - US calendar week calculation

**Type:** FUNCTION

## Description

## Short description ##

This function uses the specified date to calculate the calendar week and the number of days that have passed since the beginning of the year for the USA and many other countries.

## Functional description ##

Counting method for the USA and many other countries
•     Calendar weeks have 7 days, start on a Sunday and are counted continuously throughout the year
•     Calendar week 1 of a year is the week that contains January 1.
•     Each year has either 52 or 53 calendar weeks.
•    A year has 53 calendar weeks if the following characteristics apply:
-    A common year begins on a Saturday and ends on a Saturday.
-    A leap year begins either on a Saturday and ends on a Sunday or it begins on a Friday and ends on a Saturday.


•    The days after the last Saturday in December can belong to the first calendar week of the following year.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| date | DTL | Date used to calculate the calendar week and days since 1 January |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| calendarDay | DInt | Days past since January 1st on given date |
| error | Bool | FALSE: No error / TRUE: An error occurred during the execution of the FB |
| status | Word | 16#0000-16#7FFF: Status of the FB / 16#8000-16#FFFF: Error identification |

### Return Value

- **Type:** DInt
- **Description:** Number of the calendar week.

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8201 | ERR_LIM_DATE Date out of the range |

---

# LGF_SawToothCI - Sawtooth Signal Generator

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

This function generates a sawtooth-shaped signal profile. For this it uses the time interval of the 
calling Cyclic Interrupt OB.

## Functional description ##

Note The status of called commands is output in subFunctionStatus. In this case, the output value 
in status indicates which command caused the error. In this case, refer to the TIA Portal 
Online Help section for information on the respective commands.
The block calculates the values for a sawtooth-shaped signal profile, which is output to the 
output parameter value.
The amplitude, the offset in the Y-direction, the period, and the phase shift can be set at the 
input parameters.
The input parameter reset resets the signal profile. At the value output parameter, the value 0 is 
output as long as reset is set to TRUE.
The block must be called in a cyclic interrupt OB. The time interval of the calling cyclic interrupt 
OB is determined in the FB with the command QRY_CINT. For this, the constant name of the 
calling cyclic interrupt OB must be interconnected at the input parameter callOB.
The number of calculated values of the signal profile per period duration is calculated as follows:
𝑄𝑢𝑎𝑛𝑡𝑖𝑡𝑦𝑉𝑎𝑙𝑢𝑒𝑠 =
𝑃𝑒𝑟𝑖𝑜𝑑𝑑𝑢𝑟𝑎𝑡𝑖𝑜𝑛
/𝑇𝑖𝑚𝑒𝑖𝑛𝑡𝑒𝑟𝑣𝑎𝑘𝐶𝑦𝑐𝑙𝑖𝑐𝑖𝑛𝑡𝑒𝑟𝑟𝑢𝑝𝑡𝑂𝐵
Note To obtain a continuous signal profile of the curve, the time interval of the cyclic interrupt OB 
should not be selected too large depending on the period duration.The Figure below shows the signal profile of the calculated values.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| amplitude | Real | 1.0 |
| offset | Real | 0.0 |
| periode | UDInt | 1000 |
| phaseShift | Real | 0.0 |
| callOB | OB_CYCLIC |  |
| reset | Bool | FALSE |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | Real | Current value of the sawtooth signal. |
| error | Bool | FALSE: No error |
| status | Word | 16#0000-16#7FFF: Status of the FB 16#8000-16#FFFF: Error identification |
| subFunctionStatus | Word | Status or return value of called FB's, FC's and system blocks |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_FINISHED_NO_ERROR |
| 16#8600 | ERR_OB_UNAVAILABLE |
| 16#8601 | ERR_QRY_CINT |

---

# LGF_CelsiusToKelvin - Celsius to Kelvin Converter

**Type:** FUNCTION

## Description

## Short description ##

This function converts a temperature value - from °Celsius to °Kelvin.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | Real | Temperature to be converted in °Celsius |

### Return Value

- **Type:** Real
- **Description:** Converted temperature in °Kelvin

---

# LGF_SplitDWordToBytes - DWord to 4-Byte Splitter

**Type:** FUNCTION

## Description

## Short description ##

This function splits a DWord variable into 4 Byte variables.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| doubleWord | DWord | Bit sequence to be split |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| byte3 | Byte | Output Byte 3 - MSB |
| byte2 | Byte | Output Byte 2 |
| byte1 | Byte | Output Byte 1 |
| byte0 | Byte | Output Byte 0 - LSB |

---

# LGF_IsValueInRange - Value set point range check

**Type:** FUNCTION

## Description

## Short description ##

The function checks whether a value is within a defined value range.
The value range is defined with a set point and a range around this set point. The function 
calculates the low limit and high limit of the value range.

## Functional description ##

The setpoint and range variables define a range of values.
The function checks whether the value is below, in or above the value range. The outputs 
belowLowLimit, Ret_Val, or overHighLimit show where the value is located.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | LReal | Value to be checked to determine whether it is within the defined value range |
| setpoint | LReal | Set point |
| range | LReal | Area where the setpoint is in range |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| overHighLimit | Bool | TRUE if the “value” is greater than the upper limit value |
| belowLowLimit | Bool | TRUE, if the “value” is less than the lower limit value |
| error | Bool | FALSE: No error TRUE: An error occurred during the execution of the FB |
| status | Word | 16#0000-16#7FFF: Status of the FB 16#8000-16#FFFF: Error identification |

### Return Value

- **Type:** Bool
- **Description:** Return: TRUE if the “value” is in the value range (range of the set point)

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8401 | ERR_RANGE_LIMIT_VALUES |

---

# LGF_CountBooleanEdges - Boolean signal edge detection

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

This function evaluates a input signal for different states in a certain amount of time.
The states are:
• One edge and input present over the whole monitoring time
• Single edge
• Double edge
• N-Edges in between the monitoring time
The Output signal is present for at least on cycle after the monitoring time has expired, or as 
long as the input trigger remains TRUE.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| trigger | Bool | Trigger to evaluate signal |
| monitorTime | Time | Time to monitor and count edges on `trigger` input |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| single | Bool | Single edge until monitoring time expires |
| double | Bool | Two edges in between the monitoring time |
| long | Bool | Just a single edge in the monitoring time, the `trigger` input stays TRUE after the edge appears |
| severalEdges | Bool | Numerous Edges occur within the monitoring time |
| noOfEdges | USInt | Number of edges in between the monitoring time frame |

---

# LGF_SawTooth - Sawtooth Signal Profile Generator

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

This function generates a sawtooth-shaped signal profile. Each sawtooth consists of a defined 
number of steps (increments).
Note LEGACY FUNCTION
Please update and use the FB with the same name LGF_CountRisInDWord in the future!
This function is no longer maintained

## Functional description ##

Note Please note that changes at the input parameters only become effective with reset.
The block calculates the values for a sawtooth-shaped signal profile, which is output to the 
output parameter value. The signal begins with the start value startValue and is added with the 
value increment after each elapse of the time interval timeRange. The value can also be 
negative.
If the variable endlessSteps is set to FALSE, the number of add operations is counted. If this 
exceeds the value numberSteps, the output parameter value is set back to the start value. A new 
sawtooth begins.
If the variable endlessSteps is set to TRUE, the value increment is added without interruption, 
starting once at startValue. If the maximum positive INT value range (32767) of the output 
parameter value is exceeded, value changes to the maximum negative INT value range (-32768) and will continue to be added up.
Note The duration of a sawtooth at endlessSteps on FALSE is calculated as follows:
Duration = #timeRange * (#numberSteps + 1)

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| startValue | Int | 0 |
| timeRange | Time | T#0s |
| incrementRange | Int | 0 |
| numberSteps | Int | 0 |
| endlessSteps | Bool | FALSE |
| reset | Bool | FALSE |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | Int | Current value of the sawtooth signal. |

---

# LGF_Histogram_LReal - Histogram Calculation Function Block for Real Data

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

The histogram shows the frequency distribution of a sample by class. A class describes a value 
interval in which the individual frequencies are added together. After specifying the number of 
classes, the class width and the respective class center are calculated. The number of classes 
is limited to 15.
The distribution is represented as a rectangle around the class mean with the class width and 
the cumulated frequency as height.
Figure: Distribution

## Functional description ##

The block sorts the transferred data and calculates the general class width using the transferred 
class count and data range. The block then counts the values that lie within a class. In order to 
draw a histogram, the block also calculates the necessary X and Y coordinates.
The elements of the passed array values are sorted in ascending order by the block. The 
LGF_Shellsort_UDInt block is used for sorting.
The number of classes can be specified using the following rule of thumb:

Formulas

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| execute | Bool | Activation of the calculation with each positive edge. |
| numberOfClasses | UInt | Number of desired classes. |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | FALSE: No error, TRUE: An error occurred during the execution of the FB |
| status | Word | Status of the FB and error identification. |
| subfunctionStatus | Word | Status or return value of called FB's, FC's and system blocks |
| histValues | Array[0..1, 0..#CLASSES_COUNTER_UP_LIMIT] of LReal | Displays the relative frequency and class centers. |
| axis | Array[0..3] of LReal | Specifies the axis values. |
| classWidth | LReal | Returns the calculated class width. |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| values | Array[*] of LReal | The array containing the data series for calculation. |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_EXECUTION_FINISHED: Execution finished without errors |
| 16#7000 | STATUS_NO_CALL: No call of FB. The block waits for activation. |
| 16#7001 | STATUS_FIRST_CALL: First call of FB after enabling |
| 16#8600 | ERR_SHELL_SORT: Error in command `LGF_ShellSort_LReal`. |
| 16#9101 | ERR_WRONG_NO_CLASSES: Incorrect number of classes. |

---

# LGF_RandomRange_DInt - Random DInt Range Number Generator

**Type:** FUNCTION

## Description

## Short description ##

This function generates a random value in defined limits with each call.
The random number has the data type DInt in the specified range.

## Functional description ##

Note The status of called commands is output in subFunctionStatus. In this case, the output value 
in status indicates which command caused the error. In this case, refer to the TIA Portal 
Online Help section for information on the respective commands.
The block generates random values that are between the specified minValue and the maxValue. 
This random value is output via the Ret_Val.
The random value is formed from the nanoseconds of the current system time of the CPU. The 
byte order of this value is inverted and then converted to a DInt.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| minValue | DInt | Minimum value of the range of the random number - lower border |
| maxValue | DInt | Maximum value of the range of the random number - upper border |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | Error flag |
| status | Word | Status code |
| subfunctionStatus | Word | Status or return value of called blocks |

### Return Value

- **Type:** DInt
- **Description:** Random DInt number in the predefined range

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_FINISHED_NO_ERROR |
| 16#8200 | ERR_MAX_LESS_MIN |
| 16#8600 | ERR_RD_SYS_T |

---

# LGF_DifferenceQuotientFB - Numeric Differentiation Function Block

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

This function numerically differentiates a signal sampled equidistantly in time. For example, the 
velocity can be calculated from a measured locus curve, or the acceleration can be calculated 
from the measured velocity. In order to minimize the effects of a scattering measurement signal, 
this algorithm uses a compensating polynomial.
The function block calculates the differentiated values cyclically.
The function block reads-in a value with each positive edge on the insert been read in, the 
block calculates a differentiated value and outputs it.

## Functional description ##

To calculate the difference quotient of a scattering signal, a third-degree compensation 
polynomial is first placed through the measured values. This polynomial is then differentiated. 
With this method, even a distorted input signal can be sensibly differentiated.
The difference quotient is calculated with the following formula:

The function (FC) can calculate 𝑁 − 4 differentiated and smoothed measured values from N 
measured values. The output array would be assigned with 0 in the index (0,1,N-1,N). However, 
the following formalisms can be used to calculate substitute values:

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| enable | Bool | Activates the block. |
| insert | Bool | Accepts the value at the input `value` at positive edge and outputs a `derivatedValue` if five values have been read in. |
| value | LReal | Value that must be included in the differentiation. |
| deltaT | LReal | Equidistant distance between two measured values. (e.g. 1s) |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| derivatedValue | LReal | The differentiated value. |
| error | Bool | FALSE: No error, TRUE: An error occurred during the execution of the FB |
| status | Word | Status and error identification of the FB |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#7000 | STATUS_NO_CALL: The block waits for activation through the parameter `enable`. |
| 16#7001 | STATUS_FIRST_CALL: First call of FB after enabling |
| 16#7002 | STATUS_SUBSEQUENT_CALL: Processing is active. Subsequent call of FB. |
| 16#7010 | STATUS_NOT_ENOUGH_VALUES: The block requires five (5) values to calculate a differentiated value. |
| 16#8200 | ERR_DELTA_T: Delta time `deltaT` must not be zero. |

---

# LGF_CosinusCI - Cosine Signal Generator

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

This function generates a cosinusoidal signal profile. For this it uses the time interval of the 
calling Cyclic Interrupt OB.

## Functional description ##

Note The status of called commands is output in subFunctionStatus. In this case, the output value 
in status indicates which command caused the error. In this case, refer to the TIA Portal 
Online Help section for information on the respective commands.
The block calculates the values for a cosinusoidal signal profile, which is output to the output 
parameter value.
The amplitude, the offset in the Y-direction, the period (in ms) and the phase shift (in ms) can 
be set at the input parameters.
The input parameter reset resets the signal profile. At the value output parameter, the value 0 is 
output as long as reset is set to TRUE.
The block must be called in a cyclic interrupt OB. The time interval of the calling cyclic interrupt 
OB is determined in the FB with the command QRY_CINT. For this, the constant name of the 
calling cyclic interrupt OB must be interconnected at the input parameter callOB.
The number of calculated values of the signal profile per period duration is calculated as follows:
𝑄𝑢𝑎𝑛𝑡𝑖𝑡𝑦𝑉𝑎𝑙𝑢𝑒𝑠 =𝑃𝑒𝑟𝑖𝑜𝑑𝑑𝑢𝑟𝑎𝑡𝑖𝑜𝑛/𝑇𝑖𝑚𝑒𝑖𝑛𝑡𝑒𝑟𝑣𝑎𝑘𝐶𝑦𝑐𝑙𝑖𝑐𝑖𝑛𝑡𝑒𝑟𝑟𝑢𝑝𝑡𝑂𝐵
Note To obtain a continuous signal profile of the curve, the time interval of the cyclic interrupt OB 
should not be selected too large depending on the period duration.
The Figure below shows the signal profile of the calculated values.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| amplitude | Real | 1.0 |
| offset | Real | 0.0 |
| periode | UDInt | 1000 |
| phaseShift | Real | 0.0 |
| callOB | OB_CYCLIC |  |
| reset | Bool | FALSE |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | Real | Current value of the cosinusoidal signal. |
| error | Bool | FALSE: No error |
| status | Word | 16#0000-16#7FFF: Status of the FB 16#8000-16#FFFF: Error identification |
| subFunctionStatus | Word | Status or return value of called FB's, FC's and system blocks |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_FINISHED_NO_ERROR |
| 16#8600 | ERR_OB_UNAVAILABLE |
| 16#8601 | ERR_QRY_CINT |

---

# LGF_GetCalendarDay - Calendar day calculation

**Type:** FUNCTION

## Description

## Short description ##

This function uses the specified date to calculate the number of days that have passed since the beginning of the year (1st January).
The function is used in the functions “LGF_GetCalendarWeek_ISO” and
“LGF_GetCalendarWeek_US” .

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| date | DTL | Date for the calculation of the calendar days since 1 January. |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | FALSE: No error / TRUE: An error occurred during the execution of the FB |
| status | Word | 16#0000-16#7FFF: Status of the FB / 16#8000-16#FFFF: Error identification |

### Return Value

- **Type:** DInt
- **Description:** Days past since January 1st.

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8201 | ERR_LIM_DATE Date out of the range |

---

# LGF_FileRead - File Reading from UserFiles Folder

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

This function block offers reading data as binary / serialized data stream from files stored on the 
PLC's memory card in the folder UserFiles.

## Functional description ##

With the function LGF_FileRead a file can be read into the data budget of a variable at data. To 
read the data it is necessary to deserialize it, which the function already takes from the user.
For deserialization an external buffer in the form of a byte array must be connected which can 
take up the amount of data, if the buffer is too small an error is output.
The file name must always be specified in full together with the folder name and the file 
extension in the following format: UserFiles/test.dat.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| execute | Bool | Rising edge starts file read once |
| dataLengthMustMatch | Bool | The length of the file data set and the dataset in the PLC have to match. |
| fileName | String | Name of file including path: `UserFiles/test.dat` |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| done | Bool | Commanded functionality has been completed successfully |
| busy | Bool | FB is not finished and new output values can be expected |
| error | Bool | An error occurred during the execution of the FB |
| status | Word | Status of the FB, Error identification |
| dataLength | DInt | Data length read from file (serialized length of `data`) |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| bufferByteArray | Array[*] of Byte | Byte array buffer for read / write from / to file |
| data | Variant | Data set read from file |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_EXECUTION_FINISHED |
| 16#7000 | STATUS_NO_CALL |
| 16#7001 | STATUS_FIRST_CALL |
| 16#7002 | STATUS_SUBSEQUENT_CALL |
| 16#8201 | ERR_BUFFER_LOWERBOUND |
| 16#8202 | ERR_BUFFER_ARRAY_TO_SMALL_TO_COPY |
| 16#8401 | ERR_FILE_PATH |
| 16#8411 | ERR_FILE_SIZE_GRATER_THEN_DATA_SIZE |
| 16#8412 | ERR_FILE_SIZE_LESS_THEN_DATA_SIZE |
| 16#8600 | ERR_UNDEFINED_STATE |
| 16#8601 | ERR_MOVE_BLK_VARIANT |
| 16#8602 | ERR_DATA_SERIALIZE |
| 16#8603 | ERR_DATA_DESERIALIZE |
| 16#8604 | ERR_FILE_READ_INIT |
| 16#8605 | ERR_FILE_READ |

## User Defined Types

### LGF_typeDiagnostics
Diagnostic structure to store and transfer diagnostic information from blocks trough the interface.

### Members

| Name | Type | Description |
| :--- | :--- | :--- |
| status | Word | Status of the Block or error identification when error occurred |
| subfunctionStatus | Word | Status or return value of called FB's, FC's and system blocks |
| stateNumber | DInt | State in the state machine of the block where the error occurred |

---

# LGF_SmoothByPolynomFC - Polynomial Smoothing Function

**Type:** FUNCTION

## Description

## Short description ##

This function calculates the smoothed values by polynomial acyclically.
For smoothing, a 3rd degree polynomial is placed through five value points. The error squares 
of the distances between polynomial and real value are minimized. The smoothed values can 
be determined from the polynomial parameters obtained in this way.
The function reads an array that is smoothed. 𝑁 − 4 smoothed measured values can be 
calculated from N measured values. The output array contains the value 0 in the index (0,1,N-
1,N). However, replacement values can be calculated.

## Functional description ##

The 3rd degree compensation polynomial is calculated as follows:

𝑁 − 4 smoothed measured values can thus be calculated from the N measured values. The 
output array contains the value 0 in the index (0.1, N-1, N).
These “missing” values are calculated with the following formalisms:

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | FALSE: No error TRUE: An error occurred during the execution of the FB |
| status | Word | Status of the FB |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| values | Array[*] of LReal | Values that are to be included in the smoothing. |
| smoothedValues | Array[*] of LReal | The smoothed values. |

### Return Value

- **Type:** Void
- **Description:** Void - Function has no return value

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_FINISHED_NO_ERROR |
| 16#8400 | ERR_ARRAYS_DIFFERENT Error: The Array sizes are not equal. |
| 16#8401 | ERR_NOT_ENOUGH_VALUES Error: Not enough values. |

---

# LGF_SimpleSmoothingFB - Simple Smoothing Function Block

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

The function calculates the linear mean value cyclically.
The simplest form of smoothing a sequence of measured values is to calculate the linear mean 
value by three points.
The function reads-in a value with each positive edge on the insert input. As soon as three 
values have been read in, the block calculates a smoothed value and outputs it.

## Functional description ##

The function calculates the smoothed values using the following formula:
𝑦(𝑛) = (𝑦(𝑛 − 1) + 𝑦(𝑛) + 𝑦(𝑛 + 1)) / 3
The calculated value is output or the calculated values are output at output smoothedValue.
Based on this formula, the function cannot calculate values for the elements 0 and N.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| enable | Bool | Activates the block. |
| insert | Bool | Accepts the value at the input `value` at positive edge and outputs a `smoothedValue` if three values have been read in. |
| value | LReal | Value that is to be included in the smoothing. |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| smoothedValue | LReal | The smoothed value. |
| error | Bool | FALSE: No error, TRUE: An error occurred during the execution of the FB |
| status | Word | Status of the FB and error identification. |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#7000 | STATUS_NO_CALL: The block waits for activation through the parameter `enable`. |
| 16#7001 | STATUS_FIRST_CALL: First call of FB after enabling |
| 16#7002 | STATUS_SUBSEQUENT_CALL: Processing is active. Subsequent call of FB. |
| 16#7010 | STATUS_NOT_ENOUGH_VALUES: The block requires three (3) values to calculate a smoothed value. |

---

# LGF_StringToTaddr - String to TADDR_Param Converter

**Type:** FUNCTION

## Description

## Short description ##

The system data type TADDR_Param contains address information consisting of an IPV4 address 
and the port number.
The LGF_StringToTaddr function converts a variable od data type String to a TADDR_Param
system data type variable.

## Functional description ##

The function converts the IPV4 address with or without port number from data type String to 
TADDR_Param.
The string must be in the following form:
• without port number: [0..255].[0..255].[0..255].[0..255]
• with port number: [0..255].[0..255].[0..255].[0..255]:[0..65535]

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| ipAddressString | String | IPV4 address string in the format of 192.168.1.200:55047 [Port number including colon : is optional] |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | An error occurred during the execution of the FB |
| status | Word | Status of the FB, Error identification |

### Return Value

- **Type:** TADDR_Param
- **Description:** IP-Address and Port number as TADDR_Param data type

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_FINISHED_NO_ERROR |
| 16#8110 | ERR_OCTET_WRONG_NUMBER_OF_CHAR |
| 16#8120 | ERR_OCTET_STRING_IS_EMPTY |
| 16#8130 | ERR_OCTET_EXCEEDS_MAX_IP_ADDRESS |
| 16#8150 | ERR_PORT_WRONG_NUMBER_OF_CHAR |
| 16#8151 | ERR_PORT_STRING_IS_EMPTY |
| 16#8152 | ERR_PORT_EXCEEDS_MAX_PORT |

---

# LGF_BitTest - Bit status check operation

**Type:** FUNCTION

## Description

## Short description ##

This block checks whether a bit is TRUE or FALSE at a given position in a variable of the data type DWORD.
Alternatively, Word and Byte can be used instead of DWord by converting the passed
parameter with, for example, BYTE_TO_DWORD and the result with DWORD_TO_BYTE.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | DWord | Tag where the bit has to be tested |
| bitNo | USInt | bit number to test in "value" parameter |

### Return Value

- **Type:** Bool
- **Description:** Value of the checked bit.

---

# LGF_AverageAndDeviation - Arithmetic Mean and Standard Deviation Calculator

**Type:** FUNCTION

## Description

## Short description ##

This function calculates the arithmetic mean and the standard deviation from a series of 
numbers.

## Functional description ##

An array of any size is connected via the variableArray input. After reading-out the array 
boundaries, the arithmetic mean value and the standard deviation will be calculated from the 
values and both will be output.
Note An array with too many elements can cause the cycle monitoring time to be exceeded.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| variableArray | Array[*] of LReal | Sequence of numbers to calculate with |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| arithmeticAverage | LReal | Calculated arithmetic average value |
| standardDeviation | LReal | Calculated standard deviation |

### Return Value

- **Type:** Void
- **Description:** Void - Function has no return value

---

# LGF_BitSetTo - Bit assignment operation in DWORD

**Type:** FUNCTION

## Description

## Short description ##

This block sets a bit to TRUE or FALSE at a predefined position in a variable of the data type DWORD.
Alternatively, Word and Byte can be used instead of DWord by converting the passed
parameter with, for example, BYTE_TO_DWORD and the result with DWORD_TO_BYTE.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | DWord | Tag where the bit has to be set / reset |
| bitNo | USInt | Bit number to set in "value" parameter |
| setTo | Bool | Set bit to FALSE / TRUE |

### Return Value

- **Type:** DWord
- **Description:** Tag with set bit

---

# LGF_ToLower - String Lower Case Converter

**Type:** FUNCTION

## Description

## Short description ##

This function converts the capital letters of a string into their lower case equivalents.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| In | String | String input |

### Return Value

- **Type:** String
- **Description:** Resulting string, after the conversion

---

# LGF_CalcCRC8For1Byte - Single Byte CRC-8 Calculator

**Type:** FUNCTION

## Description

## Short description ##

The CRC calculation is used for error detection at data transmission. The result of a calculation 
returns a CRC value via the data sent (Byte). The receiver detects a faulty transmission due to 
the unequal CRC value. The function LGF_CalcCRC8For1Byte uses 8 bits as the generator 
polynomial (mask).

## Functional description ##

The function calculates the CRC value from a data byte value. The start value initValue and 
the generator polynomial mask can be freely selected.
Note Various online tools are available for calculating the CRC values. The function of the block 
was tested with the following online tool, since it supports the input parameters mask
(Polynomial) and initValue (Initial Value):
http://www.sunshine2k.de/coding/javascript/crc/crc_js.html

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| initValue | Byte | Start value for the calculation |
| mask | Byte | Generator polynomial for the calculation |
| value | Byte | Data byte for which the CRC value will be calculated |

### Return Value

- **Type:** Byte
- **Description:** Calculated CRC value

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |

---

# LGF_SmoothByPolynomFB - Polynomial Smoothing Function Block

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

This function calculates the smoothed values by polynomial cyclically.
For smoothing, a 3rd degree polynomial is placed through five value points. The error squares 
of the distances between polynomial and real value are minimized. The smoothed values can 
be determined from the polynomial parameters obtained in this way.
The function reads-in a value with each positive edge on the insert input. As soon as five 
values have been read in, the block calculates a smoothed value and outputs it.

## Functional description ##

The 3rd degree compensation polynomial is calculated as follows:

𝑁 − 4 smoothed measured values can thus be calculated from the N measured values. The 
output array contains the value 0 in the index (0.1, N-1, N).
These “missing” values are calculated with the following formalisms:

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| enable | Bool | Activates the block. |
| insert | Bool | Accepts the value at the input `value` at positive edge and outputs a `smoothedValue` if five values have been read in. |
| value | LReal | Value that is to be included in the smoothing. |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| smoothedValue | LReal | The smoothed value. |
| error | Bool | FALSE: No error, TRUE: An error occurred during the execution of the FB |
| status | Word | Status of the FB and error identification. |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#7000 | STATUS_NO_CALL: The block waits for activation through the parameter `enable`. |
| 16#7001 | STATUS_FIRST_CALL: First call of FB after enabling |
| 16#7002 | STATUS_SUBSEQUENT_CALL: Processing is active. Subsequent call of FB. |
| 16#7010 | STATUS_NOT_ENOUGH_VALUES: The block requires five (5) values to calculate a smoothed value. |

---

# LGF_ConvertTemperature - Temperature Unit Converter

**Type:** FUNCTION

## Description

## Short description ##

This function converts a temperature value from one into another unit by using an appropriate 
given mode parameter.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| mode | Int | Conversion mode |
| value | Real | Temperature value to be converted |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | An error occurred during the execution of the FB |
| status | Word | Status of the FB |

### Return Value

- **Type:** Real
- **Description:** Converted temperature result

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#8200 | ERR_WRONG_MODE |

---

# LGF_TimerSwitch - Timer with various time switch points

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

This block is a timer. It is possible to define daily, weekly, monthly, yearly time switch points and 
time switch points for working days or weekend days.
Mode: Permanently off: 0, Daily: 1, Weekly: 2, Monthly: 3, Yearly: 4, Workday: 5, Weekend: 6, 
Permanently on: 10
The time value is always compared with the local time of the PLC, therefore the time value 
specified at the On and Off parameters must be specified as local time.

## Functional description ##

Note The status of called commands is output in subFunctionStatus. In this case, the output value 
in status indicates which command caused the error. In this case, refer to the TIA Portal 
Online Help section for information on the respective commands.
Note The function uses internally the system function RD_LOC_T to read the local time of the CPU, 
for the correct function it is therefore necessary that the local time of the CPU is set correctly.
The block offers various timer types, which are determined in the mode parameter:
• Permanently off (mode = 0)
• Daily timer (mode = 1)
• Weekly timer (mode = 2)
• Monthly timer (mode = 3)
• Yearly timer (mode = 4)
• Weekdays, Monday to Friday (mode = 5)
• Weekend, Saturday and Sunday (mode = 6)
• Permanently on (mode = 10)
The time value is always compared with the local time of the PLC, therefore the time value 
specified at the On and Off parameters must be specified as local time.
Depending on the mode, the following formal parameters must be interconnected:
Mode. Mode Required - formal parameters
0 . Permanently OFF – none
1 . Daily timer – onHour / offHour
– onMinute / offMinute
2 . Weekly timer – onWeekday / offWeekday
– onHour / offHour
– onMinute / offMinute
3 . Monthly timer – onDay / offDay
– onHour / offHour
– onMinute / offMinute
4 . Yearly timer – onMonth / offMonth
– onDay / offDay
– onHour / offHour
– onMinute / offMinute
5 . Weekdays – onHour / offHour
– onMinute / offMinute
6 . Weekend – onHour / offHour
– onMinute / offMinute
10 . Permanently ON – none
If the set start time equals the current local time of the controller, the output signal is set to 
TRUE. If the set switch-off time equals the current local time of the controller, the signal output is 
reset again.
Note Please note that the block can be used in the “Monthly timer” modes (mode = 3) or “yearly 
timer” (mode = 4) the block only switches if the days that you specify at the input parameters, 
“onDay” and “offDay”, actually occur in this month.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| onMonth | USInt | Month, in which the signal shall be set. |
| onDay | USInt | Day, at which the signal shall be set. |
| onWeekday | USInt | Day of the week on which the signal will be set; Sunday: 1, Monday: 2, Tuesday: 3, ... |
| onHour | USInt | Hour, at which the signal shall be set. |
| onMinute | USInt | Minute, at which the signal shall be set. |
| offMonth | USInt | Month, in which the signal shall be reset. |
| offDay | USInt | Day, at which the signal shall be reset. |
| offWeekday | USInt | Day of the week on which the signal will be reset; Sunday: 1, Monday: 2, Tuesday: 3, ... |
| offHour | USInt | Hour, at which the signal shall be reset. |
| offMinute | USInt | Minute, at which the signal shall be reset. |
| mode | USInt | Specifies the mode (see Principle of operation) |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| signal | Bool | Output signal |
| actLocalTime | DTL | Current local time |
| error | Bool | FALSE: No error / TRUE: An error occurred during the execution of the FB |
| status | Word | 16#0000-16#7FFF: Status of the FB / 16#8000-16#FFFF: Error identification |
| subFunctionStatus | Word | Sub function status code |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#8200 | ERR_NO_MODE_SELECTED |
| 16#8600 | ERR_RD_LOC_T |

---

# LGF_LimRateOfChangeCI - Rate of Change Limiter

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

This function limits the rate of change of an input variable. A jump function becomes a ramp 
function.

## Functional description ##

Note The status of called commands is output in subFunctionStatus. In this case, the output value 
in status indicates which command caused the error. In this case, refer to the TIA Portal 
Online Help section for information on the respective commands.
The ramp is a limit line and refers to a rate of change per second; if, for example, setChangeRate 
= 10.0 is parameterized at a sampling time of 1s/100ms/10ms for every block call, then if value 
> delayedValue, 10.0/1.0/0.1 is added to delayedValue until value is reached.
The limitation of the rate of change applies to both positive and negative values for the rise and 
fall.
The output delayedValue can be preset or initialized.
The time interval of the calling cyclic interrupt OB is determined by interconnecting the calling 
cyclic interrupt OB at the input parameter callOB.
Pre-assigning an output
If enDefaultOutValue = TRUE is set, the value at defaultOutValue is output. When changing 
from TRUE to FALSE, the output delayedValue is ramped from defaultOutValue to value. When 
changing from FALSE to TRUE, the output delayedValue immediately jumps to defaultOutValue.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | LReal | Signal to be processed and limited in its rate of change |
| setChangeRate | LReal | Rate of change of ramp function |
| defaultOutValue | LReal | Value for pre-assignment of the output variable |
| enDefaultOutValue | Bool | Assign default output value |
| callOB | OB_CYCLIC | Calling wake-alarm interrupt OB |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| delayedValue | LReal | Output variable |
| error | Bool | Error occurred during the execution of the FB |
| status | Word | Status of the FB |
| subfunctionStatus | Word | Status or return value of called FB's, FC's and system blocks |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_FINISHED_NO_ERROR |
| 16#8200 | ERR_NEG_RATE_LIM |
| 16#8600 | ERR_QRY_CINT |
| 16#8601 | ERR_OB_UNAVAILABLE |

---

# LGF_DataLogC - Standalone Data Logger with Advanced Configuration

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

LGF_DataLogC (C -> Compact) function integrates all the datalog system functions and can be 
used as standalone data logger.

## Functional description ##

The function LGF_DataLogC combines the system functions for creating and writing data logs in 
one block.
The procedure provides that an existing Datalog is opened on the basis of the name (name), if it 
was not created before, this is recognized and the function creates the Datalog.
Afterwards, depending on the parameterization, the data is written from data in an adjustable 
interval or only on request to triggerLogEntry.
ReadMe The functionality of Datalogs can be found in the user manual:
• DataLogCreate
• DataLogOpen
• DataLogClose
• DataLogWrite
• DataLogClear
• DataLogDelete
NOTICE The following parameters are only effective when creating a data log:
• parameter.header
• parameter.maxNumberOfEntries
• parameter.timestampFormat (S7-1200 and the S7-1500 support different formats, see the 
manual DataLogCreate)
NOTICE When logging data by interval (isLoggingByInterval) time variances occur, which are 
caused by a fluctuating cycle time.
Therefore it is recommended to call the function in a time interrupt OB besides the call in the 
cyclic program and to set the trigger for writing in this interrupt OB.
NOTICE A data log which is deleted by the function without deleting the file cannot be created again 
as long as the file exists, it must first be deleted manually in the system.
Please also note the parameter parameter.deleteFile which also deletes the file next to the 
data in case of a delete command deleteLog.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| enable | Bool | TRUE: Enable functionality of FB |
| name | String | Name of datalog, also used as file name |
| triggerLogEntry | Bool | Rising edge trigger one entry in data log (only if `parameter.isLoggingByInterval` := FALSE) |
| clearLog | Bool | Rising edge triggering clearing of datalog file |
| deleteLog | Bool | Rising edge triggering deletion of datalog file if exist |
| parameter | LGF_typeDataLogParameter | This UDT belongs to the Module `LGF_DataLogC` and lists all possible parameter to configure its behaviour. |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| valid | Bool | TRUE: Valid set of output values available at the FB |
| busy | Bool | TRUE: FB is not finished and new output values can be expected |
| error | Bool | TRUE: An error occurred during the execution of the FB |
| status | Word | Status of the FB, Error identification |
| writeEntryDone | Bool | TRUE: DataLog write done successfully |
| clearLogDone | Bool | TRUE: DataLog clear done successfully |
| deleteLogDone | Bool | TRUE: DataLog delete done successfully |
| lastEntryReached | Bool | TRUE: Last entry of datalog reached, if `enableRingBuffer` is set, start from beginning, otherwise block ends here |
| noOfEntries | UDInt | Number of entries in datalog |
| diagnostics | LGF_typeDiagnostics | Diagnostic structure to store and transfer diagnostic information from blocks trough the interface. |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| data | Variant | Data structure to log in datalog file |

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_FINISHED_NO_ERROR |
| 16#7000 | STATUS_NO_CALL |
| 16#7001 | STATUS_FIRST_CALL |
| 16#7002 | STATUS_SUBSEQUENT_CALL |
| 16#7010 | STATUS_MAX_ENTRIES_REACHED |
| 16#8401 | ERR_WRONG_COMMAND_CALL_ORDER |
| 16#8600 | ERR_UNDEFINED_STATE |
| 16#8601 | ERR_DATALOG_OPEN |
| 16#8602 | ERR_DATALOG_CREATE |
| 16#8603 | ERR_DATALOG_CLOSE |
| 16#8604 | ERR_DATALOG_WRITE |
| 16#8605 | ERR_DATALOG_DELETE |

## User Defined Types

### LGF_typeDataLogParameter
This UDT belongs to the Module LGF_DataLogC and lists all possible parameter to configure its behaviour.

### Members

| Name | Type | Description |
| :--- | :--- | :--- |
| header | String | Headline of datalog, string of all data fields, separated by a comma: "field1,field2,field3,..." |
| maxNumberOfEntries | UDInt | Maximum number of entries in datalog |
| timestampFormat | USInt | Timestamp format |
| clearOnOpen | Bool | Clear datalog during opening datalog while enabling block |
| deleteFile | Bool | Delete as well datalog file during datalog delete |
| enableRingBuffer | Bool | TRUE: Overwrite old values and start from the beginning if datalog reaches its maximum entries FALSE: Stop logging if `maxNumberOfEntries` entries reached |
| loggingByInterval | Bool | TRUE: Log on interval time parameter FALSE: log on "triggerEntry" |
| loggingInterval | Time | Time for automatic logging interval |

### LGF_typeDiagnostics
Diagnostic structure to store and transfer diagnostic information from blocks trough the interface.

### Members

| Name | Type | Description |
| :--- | :--- | :--- |
| status | Word | Status of the Block or error identification when error occurred |
| subfunctionStatus | Word | Status or return value of called FB's, FC's and system blocks |
| stateNumber | DInt | State in the state machine of the block where the error occurred |

---

# LGF_CelsiusToFahrenheit - Celsius to Fahrenheit Converter

**Type:** FUNCTION

## Description

## Short description ##

This function converts a temperature value - from °Celsius to °Fahrenheit.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | Real | Temperature to be converted in °Celsius |

### Return Value

- **Type:** Real
- **Description:** Converted temperature in °Fahrenheit

---

# LGF_NonLinearInterpolation - Non-Linear Interpolation Function

**Type:** FUNCTION_BLOCK

## Description

## Short description ##

This function implements a characteristic curve. The characteristic curve is defined via an 
interpolation point table with linear interpolation between the interpolation points. A prescribed 
input value generates an output value in each cycle based on the characteristic curve from the 
interpolation point table.

## Functional description ##

The value of the output outputValue based on the following priority:
1. As long as the input enDefaultOutValue is set, the value defined via the parameter 
defaultOutValue will be output as output value.
2. As long as the input reset is set, the block is reset and the output value is 0.0.
3. If the input track is set, the output value will be output directly as input value, without 
consideration of the characteristic curve.
4. Based on the input value, a characteristic curve value is calculated via the linearly 
interpolated, interpolation point table and output as an output value.
– If the input value is between two interpolation points within the interpolation point table, 
the output value is calculated as the intersection with the connecting line between the 
preceding and following interpolation points (see Figure below).
– If the input value is before the first interpolation point (lowest value defined in the 
interpolation point table), the output value will be calculated as the intersection of the 
line formed by the first two interpolation points of the interpolation point table.
– If the input value is after the last interpolation point (highest value defined in the 
interpolation point table), the output value will be calculated as the intersection of the 
line formed by the last two interpolation points of the interpolation point table.
Interpolation point table
The interpolation point table is implemented through a variable of the data type Array. The type 
of the array corresponds to the PLC data type LGF_typeNonLinSetpoints.
You can create the interpolation point table in any global data block. The size of the array 
depends on the number of interpolation points.
NOTICE To keep the computing time of the block as short as possible, there is no check of the 
parameterization or the data of the interpolation point table.
When entering the interpolation points in the interpolation point table, the following 
particularities must be considered. If these particularities are not taken into account, it can 
lead to a malfunction of the block.
• At least two interpolation points must be entered in the interpolation point table.
• The interpolation points in the interpolation point table must be entered in the Table in ascending 
order of the input values.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| value | LReal | Input value for calculating the output value |
| defaultOutValue | LReal | Value for pre-assignment of the output variable |
| enDefaultOutValue | Bool | Assign default output value |
| track | Bool | Follow the value of the input without using the characteristic curve |
| reset | Bool | Reset the interpolation if the point table is changed in running operation |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| outputValue | LReal | The calculated output value from the input value |

### In/Out Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| setpoints | Array[*] of LGF_typeNonLinSetpoints | Setpoint table for defining the characteristic curve |

## User Defined Types

### LGF_typeNonLinSetpoints
Data type for setup a setpoint table

### Members

| Name | Type | Description |
| :--- | :--- | :--- |
| inputValue | LReal | Input value to be interpolated |
| outputValue | LReal | Corresponding interpolated value |

---

# LGF_UnixTimeToDTL - Unix Time to DTL Time Converter

**Type:** FUNCTION

## Description

## Short description ##

This function converts the Unix time of data type DInt to a date and time of data type DTL. The 
timestamp is calculated in UTC. This means that the time zone is not considered.
Only times after 01/01/1990 are permitted.

### Input Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| timeUnix | DInt | UNIX time to convert |

### Output Parameters

| Name | Type | Description |
| :--- | :--- | :--- |
| error | Bool | An error occurred during the execution of the FB |
| status | Word | Status of the FB, Error identification |

### Return Value

- **Type:** DTL
- **Description:** Converted time (Date and time). In case of Error: 0 (error = true)

## Status Codes

| Code | Description |
| :--- | :--- |
| 16#0000 | STATUS_NO_ERROR |
| 16#6001 | WARN_CONVERSION_LIMIT |
| 16#8000 | ERR_TIME_BEFORE_1990 |

