# 04 Timers

# TIME (IEC time)

| TIME (IEC time) |
|---|
Description

The
contents of an operand of the data type TIME is interpreted as
milliseconds. The representation contains information for days (d),
hours (h), minutes (m), seconds (s) and milliseconds (ms).

The following table shows the properties of data type TIME:

| Length (bits) | Format | Value range | Examples of value input |
|---|---|---|---|
| 32 | Signed duration | T#-24d_20h_31m_23s_648ms to T#+24d_20h_31m_23s_647ms | T#10d_20h_30m_20s_630ms, TIME#10d_20h_30m_20s_630ms |
It
is not necessary to specify all time units. T#5h10s is a valid entry,
for example. If only one unit is specified, the absolute value of days,
hours, and minutes must not exceed the high or low limits. When more
than one time unit is specified, the value must not exceed 24 days, 23
hours, 59 minutes, 59 seconds or 999 milliseconds.

See also

Overview of the valid data types Basics of constants Data type conversion for S7-1200 (S7-1200)


# LTIME (IEC time) (S7-1500, S7-1200 G2)

| LTIME (IEC time) |
|---|
Description

The
contents of an operand of data type LTIME is interpreted as
nanoseconds. The representation contains information for days (d), hours
(h), minutes (m), seconds (s) and milliseconds (ms), microseconds (us)
and nanoseconds (ns).

The following table shows the properties of data type LTIME:

| Length (bits) | Format | Value range | Examples of value input |
|---|---|---|---|
| 64 | Signed duration | LT#-106751d_23h_47m_16s_854ms_775us_808ns to LT#+106751d_23h_47m_16s_854ms_775us_807ns | LT#11350d_20h_25m_14s_830ms_652us_315ns, LTIME#11350d_20h_25m_14s_830ms_652us_315ns |
It
is not necessary to specify all time units. LT#5h10s is therefore a
valid entry, for example. If only one unit is specified, the absolute
value of days, hours, and minutes must not exceed the high or low
limits. When more than one time unit is specified, the value must not
exceed 106751 days, 23 hours, 59 minutes, 59 seconds, 999 milliseconds,
999 microseconds or 999 nanoseconds.

See also

Overview of the valid data types Overview of data type conversion (S7-1500, S7-1200 G2) Basics of constants Implicit conversions (S7-1500, S7-1200 G2) Explicit conversions (S7-1500, S7-1200 G2) Data type conversion for S7-1200 (S7-1200)

Date and time
