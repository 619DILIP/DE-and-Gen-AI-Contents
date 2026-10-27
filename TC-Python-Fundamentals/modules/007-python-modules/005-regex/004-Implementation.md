# Implementation 

## search
The "re" module can be used to search for patterns in your strings:
```python
import re

# potential password
password = "abC123sparrow"

# regular expressions to check password has at least one uppercase, lowercase, and number in it
has_upper = re.search('[A-Z]', password)
has_lower = re.search('[a-z]', password)
has_number = re.search('[0-9]', password)

if has_upper and has_lower and has_number:
    print("valid password")
else:
    print("invalid password")
# will output "valid password"
```
## findall
you can return all instances that match your regular expression in a list
```python
import re

# email response from vendor
correspondence = "I would love to set up a meeting! You can call me at 123-456-7890 or 098-765-4321."

# regular expression to check for patterns that match phone number formatting
# \d{x} means x digits in a row
phone_numbers = re.findall(r'\d{3}-\d{3}-\d{4}', correspondence)

print(phone_numbers)
# will output: ['123-456-7890', '098-765-4321']
```

## split
you can use the "re" module to split text into individual elements
```python
import re

# csv data
csv_data = "apple,fruit,$5,non-refundable"

# split the csv data into separate fields
parsed_data = re.split(r",", csv_data)

print(parsed_data)
# will output: ['apple', 'fruit', '$5', 'non-refundable']
```

## sub
you can replace substrings by using the sub function
```python
import re

# message with sensitive information
text = "Not sure why you need this, but my credit card number is 1234-5678-9012-3456."

# regular expression to replace credit card info with placeholder text
censored_text = re.sub(r'\d{4}-\d{4}-\d{4}-\d{4}', "[CENSORED]", text)

print(censored_text)
# will output "Not sure why you need this, but my credit card number is [CENSORED]."
```