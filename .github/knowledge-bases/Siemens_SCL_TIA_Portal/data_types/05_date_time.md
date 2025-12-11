# 05 Date Time

# DATE

| DATE |
|---|
Format

The DATE data type saves the date as an unsigned integer. The representation contains the year, the month, and the day.

The contents of an operand of DATE data type correspond in hexadecimal format to the number of days since 01-01-1990 (16#0000).

The following table shows the properties of data type DATE:

| Length (bytes) | Format | Value range | Examples of value input |
|---|---|---|---|
| 2 | IEC date (Year-Month-Day) | D#1990-01-01 to D#2169-06-06 | D#2009-12-31, DATE#2009-12-31 |
See also

Overview of the valid data types Basics of constants Data type conversion for S7-1200 (S7-1200)


# TIME_OF_DAY (TOD)

| TIME_OF_DAY (TOD) |
|---|
Format

Data
type TOD (TIME_OF_DAY) occupies a double word and stores the number of
milliseconds since the beginning of the day (0:00 h) as unsigned
integer.

The following table shows the properties of data type TOD:

| Length (bytes) | Format | Value range | Examples of value input |
|---|---|---|---|
| 4 | Time-of-day (hours:minutes:seconds.milliseconds) | TOD#00:00:00.000 to TOD#23:59:59.999 | TOD#10:20:30.400, TIME_OF_DAY#10:20:30.400 |
You always need to specify the hours, minutes and seconds. The specification of milliseconds is optional.

See also

Overview of the valid data types Basics of constants Data type conversion for S7-1200 (S7-1200)


# LTOD (LTIME_OF_DAY) (S7-1500, S7-1200 G2)

| LTOD (LTIME_OF_DAY) |
|---|
Format

Data
type LTOD (LTIME_OF_DAY) occupies two double words and stores the
number of nanoseconds since the beginning of the day (0:00 h) as
unsigned integer.

The following table shows the properties of data type LTOD:

| Length (bytes) | Format | Value range | Examples of value input |
|---|---|---|---|
| 8 | Time-of-day (hours:minutes:seconds.nanoseconds) | LTOD#00:00:00.000000000 to LTOD#23:59:59.999999999 | LTOD#10:20:30.400_365_215, LTIME_OF_DAY#10:20:30.400_365_215 |
You always need to specify the hours, minutes and seconds. The specification of nanoseconds is optional.

See also

Overview of the valid data types Overview of data type conversion (S7-1500, S7-1200 G2) Basics of constants Implicit conversions (S7-1500, S7-1200 G2) Explicit conversions (S7-1500, S7-1200 G2) Data type conversion for S7-1200 (S7-1200)


# DATE_AND_TIME (date and time of day) (S7-1500)

| DATE_AND_TIME (date and time of day) |
|---|
Format

The DT (DATE_AND_TIME) data type saves the information on date and time of day in BCD format.

The following table shows the properties of data type DT:

| Length (bytes) | Format | Value range | Example of value input |
|---|---|---|---|
| 8 | Date and time (year-month-day-hour:minute:second:millisecond 3)) | Min.: DT#1990-01-01-00:00:00.000 Max.: DT#2089-12-31-23:59:59.999 | DT#2008-10-25-08:12:34.567, DATE_AND_TIME#2008-10-25-08:12:34.567 |
The following table shows the structure of the DT data type:

| Byte | Contents | Value range |
|---|---|---|
| 0 | Year | 0 to 99 (Years 1990 to 2089) BCD#90 = 1990 ... BCD#0 = 2000 ... BCD#89 = 2089 |
| 1 | Month | BCD#1 to BCD#12 |
| 2 | Day | BCD#1 to BCD# 31 |
| 3 | Hour | BCD#0 to BCD#23 |
| 4 | Minute | BCD#0 to BCD#59 |
| 5 | Second | BCD#0 to BCD#59 |
| 6 | The two most significant digits of MSEC | BCD#0 to BCD#99 |
| 7 (4MSB) 1) | The least significant digit of MSEC | BCD#0 to BCD#9 |
| 7 (4LSB) 2) | Weekday | BCD#1 to BCD#7 BCD#1 = Sunday ... BCD#7 = Saturday |
| 1) MSB: Most significant bit 2) LSB: Least significant bit 3) Fixed point number | | |
See also

Overview of the valid data types Basics of constants Data type conversion for S7-1200 (S7-1200)


# LDT (DATE_AND_LTIME) (S7-1500, S7-1200 G2)

| LDT (DATE_AND_LTIME) |
|---|
Format

Data type LDT (DATE_AND_LTIME) stores the date and time-of-day information in nanoseconds since 01/01/1970 0:0.

The following table shows the properties of data type LDT:

| Length (bytes) | Format | Value range | Example of value input |
|---|---|---|---|
| 8 | Date and time (Year-Month-Day-Hour:Minute:Second.Nanoseconds) | Min.: LDT#1970-01-01-00:00:00.000000000 Max.: LDT#2262-04-11-23:47:16.854775807 | LDT#2008-10-25-08:12:34.567 |
See also

Overview of the valid data types Overview of data type conversion (S7-1500, S7-1200 G2) Basics of constants Implicit conversions (S7-1500, S7-1200 G2) Explicit conversions (S7-1500, S7-1200 G2) Data type conversion for S7-1200 (S7-1200)


# DTL (S7-1200, S7-1500, S7-1200 G2)

| DTL |
|---|
Description

An operand of data type DTL has a length of 12 bytes and stores date and time information in a predefined structure.

The following table shows the properties of data type DTL:

| Length (bytes) | Format | Value range | Example of value input |
|---|---|---|---|
| 12 | Date and time (Year-Month-Day-Hour:Minute:Second.Nanoseconds) | Min.: DTL#1970-01-01-00:00:00.0 Max.: DTL#2262-04-11-23:47:16.854775807 | DTL#2008-12-16-20:30:20.250 |
The
structure of data type DTL consists of several components each of which
can contain a different data type and range of values. The data type of
a specified value must match the data type of the corresponding
components.

| Note Invalid monitor value of DTL tags in hexadecimal format If the monitor value of the DTL tags is represented in hexadecimal format, this can be because one of the values (YEAR, MONTH, DAY, etc.) is invalid. For example, this is the case if a value > 24 was specified at the HOUR tag. |
|---|
The following table shows the structure components of data type DTL and their properties:

| Byte | Component | Data type | Value range |
|---|---|---|---|
| 0 | Year | UINT | 1970 to 2262 |
| 1 | | | |
| 2 | Month | USINT | 1 to 12 |
| 3 | Day | USINT | 1 to 31 |
| 4 | Weekday | USINT | 1(Sunday) to 7(Saturday) The weekday is not considered in the value entry. |
| 5 | Hour | USINT | 0 to 23 |
| 6 | Minute | USINT | 0 to 59 |
| 7 | Second | USINT | 0 to 59 |
| 8 | Nanosecond | UDINT | 0 to 999999999 |
| 9 | | | |
| 10 | | | |
| 11 | | | |
See also

Overview of the valid data types Basics of constants Data type conversion for S7-1200 (S7-1200)

Character strings
