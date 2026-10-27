### Examples

Converting a string to uppercase:
```SQL
SELECT UCASE ("Hello World") AS UpperCase_String;  
```

| UpperCase_String   |
| -------------  |
| HELLO WORLD  |


Converting a string into lowercase:
```SQL
SELECT LCASE ("Hello World") AS LowerCase_String;  
```

| LowerCase_String   |
| -------------  |
| hello world  |

Selecting a substring of a string:
```SQL
SELECT MID ("Hello World", 4, 8) AS Substring;
```

| Substring   |
| -------------  |
| lo World |

Selecting the length of a string:
```SQL
SELECT LENGTH ("Hello World") AS String_Length;
```

| String_Length  |
| -------------  |
| 11 |

Rounding a numeric value to the number of decimals specified:
```SQL
SELECT ROUND (1560.44444, 2) AS Round_Value; 
```

| Round_Value  |
| -------------  |
| 1560.44 |


Selecting the current day and time:
```SQL
SELECT NOW () AS CurrentDateTime;  
```

| CurrentDateTime  |
| -------------  |
| 2022-07-17 08:44:36 |

Formatting a numeric value:
```SQL
SELECT FORMAT (1234.1234, 2) AS Format_Number;  
```

| Format_Number  |
| -------------  |
| 1234.12 |
