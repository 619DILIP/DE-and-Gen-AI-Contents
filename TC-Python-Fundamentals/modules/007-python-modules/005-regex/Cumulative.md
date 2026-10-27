# Cumulative for the regex

<details><summary>Learning Objectives</summary>

# Learning Objectives
After completing this module, associates should be able to:
- Explain what the regex module is
- Describe use cases for the regex module

</details>

<details><summary>Description</summary>

# Introduction
Regular Expressions (regex) are used to match and manipulate strings of text by creating patterns. This is useful for finding substrings, data validation, web scraping, and more. Python has a module called `re` that is used to work with regular expressions, and in Python 3, the third-party package `regex` has been added as well.

When working with regex, you will often need to perform complex pattern matching: there are "metacharacters" that help with this:
- `.` (Dot): Matches any single character except a newline
- `*` (Asterisk): Matches zero or more occurrences of the preceding character or group
- `+` (Plus): Matches one or more occurrences of the preceding character or group
- `?` (Question Mark): Matches zero or one occurrence of the preceding character or group
- `[]` (Character Class): Defines a set of characters to match
- `^` (Caret): Matches the start of a string
- `$` (Dollar Sign): Matches the end of a string
- `\` (Backslash): Escapes special characters to treat them as literal characters and can be used to represent character classes
- `|` (Pipe): Acts as an OR operator
- `()` (Parentheses): Groups characters together

</details>
<details><summary>Real World Application</summary>

# Real World Application for Regex
There are many use cases for regex in software development:
- **Pattern Matching**: Regex allows you to search for specific patterns within text, like finding all email addresses or phone numbers in a document.
- **String Replacement**: You can replace specific substrings with other text using regex, such as cleaning up data by replacing inconsistent date formats.
- **Form Input Validation**: Regex helps validate user input, such as ensuring valid email addresses, phone numbers, or passwords.
- **Data Cleaning**: Removing unwanted characters, whitespace, or formatting issues from text data.
- **Extracting Information**: Regex is useful for extracting data from HTML, XML, or JSON files.
- **Parsing Log Files**: Regex can parse log files to extract relevant information like timestamps, error messages, or IP addresses.
- **URL Routing**: In web development, regex patterns are used for URL routing and handling dynamic routes.
- **Tokenization**: Regex splits text into words or sentences, which is essential for natural language processing tasks.
- **Named Entity Recognition (NER)**: Identifying entities like names, dates, and locations in text.
- **Input Sanitization**: Preventing SQL injection or cross-site scripting (XSS) attacks by validating and sanitizing user input.
- **Content Filtering**: Regex can filter out sensitive information like credit card numbers or profanity.

</details>
<details><summary>Implementation</summary>

# Implementation

## search
The `re` module can be used to search for patterns in your strings:
```python
import re

# potential password
password = "abC123sparrow"

# regular expressions to check that the password has at least one uppercase letter, one lowercase letter, and one number
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
You can return all instances that match your regular expression in a list:
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
You can use the `re` module to split text into individual elements:
```python
import re

# csv data
csv_data = "apple,fruit,$5,non-refundable"

# split the CSV data into separate fields
parsed_data = re.split(r",", csv_data)

print(parsed_data)
# will output: ['apple', 'fruit', '$5', 'non-refundable']
```

## sub
You can replace substrings by using the sub function:
```python
import re

# message with sensitive information
text = "Not sure why you need this, but my credit card number is 1234-5678-9012-3456."

# regular expression to replace credit card info with placeholder text
censored_text = re.sub(r'\d{4}-\d{4}-\d{4}-\d{4}', "[CENSORED]", text)

print(censored_text)
# will output "Not sure why you need this, but my credit card number is [CENSORED]."
```

</details>
<details><summary>Summary</summary>

# Summary

- A regular expression (regex) is used for pattern matching.
- Regex supports using metacharacters to handle complex pattern matching.
- Python includes the `re` module with helper functions to work with regex.

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
