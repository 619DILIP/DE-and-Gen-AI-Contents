# Introduction 
Regular Expressions (regex) are used to match and manipulate strings of text by creating patterns. This is useful for finding substrings, data validation, web scraping, and more. Python has a module called "re" that is used to work with regular expression, and in Python 3 the third party package "regex" has been added as well.

When working with regex you will often need to perform complex pattern matching: there are "metacharacters" that help with this:
- ```.``` (Dot): Matches any single character except a newline
- ```*``` (Asterisk): Matches zero or more occurrences of the preceding character or group
- ```+``` (Plus): Matches one or more occurrences of the preceding character or group
- ```?``` (Question Mark): Matches zero or one occurrence of the preceding character or group
- ```[]``` (Character Class): Defines a set of characters to match
- ```^``` (Caret): Matches the start of a string
- ```$``` (Dollar Sign): Matches the end of a string
- ```\``` (Backslash): Escapes special characters to treat them as literal characters, and can be used to represent character classes
- ```|``` (Pipe): Acts as an OR operator
- ```()``` (Parentheses): Groups characters together