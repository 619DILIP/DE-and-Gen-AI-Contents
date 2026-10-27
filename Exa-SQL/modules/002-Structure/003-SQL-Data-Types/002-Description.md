<br>

In a database, each `table` is defined with a set of `columns`. Each `column` must have a data type which restricts the type of data that can be assigned to it. Each vendor can support any number of the data types. Below is a list of the most common types broken into categories.

| Category  | Sub 1        | Sub 2           | Sub 3          |
| --------- | ------------ | --------------- | -------------- |
| Character | Fixed-length | Variable-length | --             |
| Numeric   | Decimal      | Integer         | Floating point |
| Temporal  | Date         | Time            | Timestamp      |


## Character

Character types can represent character data as either `fixed` or `variable`-length character types like 'a' or 'cat' or a social media post.

### Fixed-length character types

Fixed length character types store a fixed number of bytes in storage regardless of the string or number of characters being stored. The fix length types can be declared as `char(n)` or `character(n)` (depends on the database) and each character will take up 1 byte.

```SQL
middle_initial character(1);
```

or

```SQL
middle_initial character;
```

The above column `middle_initial` will be 1 byte in storage regardless if the column actually has a value or not. Remaining characters are padded with spaces.

```SQL
pet_type char(10);
```

The column `pet_type` will always take up 10 bytes regardless if the column is empty or contains 'dog', 'feline', 'lizard', 'fish', or whatever. For instance if the value of `pet_type` is 'dog' the actual value stored in the database is, 3 bytes for 'd', 'o', 'g' + 7 bytes for the remaining spaces.

### Variable-length character types

Variable-length character types store a variable number of bytes in storage, depending on the actual length of the data. A small overhead is used to store the length of the string. Variable length types can be declared as `character varying(n)` or `varchar(n)`

```SQL
first_name varchar(20);
```

Although the column first_name is declared with a maximum length of 20 characters, the actual storage depends on the length of the string stored, plus an overhead of 1 or 2 bytes to store the string's length:

- For varchar(n) where n ≤ 255, 1 byte is used for length storage.
- For varchar(n) where n > 255, 2 bytes are used for length storage.

**Remember the last 2 bytes are reserved for storing the length.** 

If the column first_name contains the value 'John', the actual size in storage would be 5 bytes: 4 bytes for the characters 'J', 'o', 'h', 'n', and 1 additional byte for the length.


## Numeric

Numeric types store type of numbers either whole or fractional. The minimum and maximum of the different numeric types will depend on the SQL implementation. The different type of numeric types are.

- bit(n)
- bit varying(n)
- integer
- smallint
- bigint
- real(s)
- float(p,s)
- double precision(p,s)
- decimal(p,s)

### Decimal

Decimal types are used to store exact fractional number values like money.

```SQL
annual_income decimal(10,2);
```

The `decimal` data types `decimal`, `float`, `double` have a syntax that includes `type(p,s)`. In the syntax 'p' is the precision that represents the number of significant digits, 's' is the scale that represents the number of digits after the decimal point. In the example of above `annual_income` will have a maximum of 10 digits with 8 before the decimal and 2 after it, with a max value of `99,999,999.99`

### Integer

Integer data types store signed and unsigned whole numbers.

```SQL
age int;
```

### Floating point

Floating point types store approximate fractional number values. The precision and scale of floating point numbers are variable length.

```SQL
avg_temp float(10);
```

## Temporal

Temporal types store data related to dates and times.

### Date

The date type represents a date value with 3 parts year, month, and day. The range for date types is typically `0001-01-01` to `9999-12-31`. Dates are also typically stored in the format `YYYY-MM-DD`.

```SQL
dob date;
```

### Time

The time type represents data related to time of day in hours, minutes, and seconds. The time type has the format `HH:MM:SS`.

```SQL
received_at time;
```

### Timestamp

The timestamp type represents data related to a date and time. Timestamps have the format `YYYY-MM-DD HH:MM:SS`. This format has a space between the date and time sections.

```SQL
created_at timestamp;
```

On top of these very common data types, a database vendor can add any number of other data types to the implementation. Some vendors add spatial types, boolean types, json types, large object types, and more.
