<details><summary>Learning Objectives</summary>
<br>

After completing this module, associates should be able to:
- Understand the purpose of scalar functions in SQL.
- Explore different types of scalar functions and their uses.

</details>
<details><summary>Description</summary>
<br>

Scalar functions are pre-defined functions in SQL. They operate on a single value and return a single value. Seven common scalar functions are given as follows: 

| Scalar Function  | Description |
| ------------- | ------------- |
| UCASE()  |  Converts the value of a field to uppercase.   |
| LCASE()  |  Converts the value of a field to lowercase.   |
| MID()  | Returns the substring from the text field.  |
| LEN()  | Returns the length of the value in a text field.  |
| ROUND()  | Used to round a numeric field to the number of decimals specified.  |
| NOW()  | Returns the current system date and time.  |
| FORMAT()  | Used to format how a field is displayed.  |

</details>
<details><summary>Real World Application</summary>
<br>

Scalar functions can be used to maintain records that are case-sensitive and format-sensitive.

Real-world applications include:

- Bank management system: 
    Maintaining proper bank balances in the correct format.
- Employee management system: 
    Maintaining proper ID verification, which can be case-sensitive.
- Captcha manager: 
    Providing verification to enter websites that require case-sensitive inputs.

</details>
<details><summary>Implementation</summary> 

### Examples

Converting a string to uppercase:
```SQL
SELECT UCASE("Hello World") AS UpperCase_String;  
```

| UpperCase_String   |
| -------------  |
| HELLO WORLD  |


Converting a string to lowercase:
```SQL
SELECT LCASE("Hello World") AS LowerCase_String;  
```

| LowerCase_String   |
| -------------  |
| hello world  |

Selecting a substring of a string:
```SQL
SELECT MID("Hello World", 4, 8) AS Substring;
```

| Substring   |
| -------------  |
| lo World |

Selecting the length of a string:
```SQL
SELECT LENGTH("Hello World") AS String_Length;
```

| String_Length  |
| -------------  |
| 11 |

Rounding a numeric value to the specified number of decimals:
```SQL
SELECT ROUND(1560.44444, 2) AS Round_Value; 
```

| Round_Value  |
| -------------  |
| 1560.44 |


Selecting the current date and time:
```SQL
SELECT NOW() AS CurrentDateTime;  
```

| CurrentDateTime  |
| -------------  |
| 2022-07-17 08:44:36 |

Formatting a numeric value:
```SQL
SELECT FORMAT(1234.1234, 2) AS Format_Number;  
```

| Format_Number  |
| -------------  |
| 1234.12 |

</details>
<details><summary>Summary</summary> 
<br>

- Scalar functions operate on a single value and return a single value.

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
