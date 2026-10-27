# Write Mode
the "write" mode is used in the open function when you need to add content to a file, and can also be used to create the file. If the file referenced in the open function does not exist it will be created, but if it does exist the content of the file will be truncated (removed). 

# Write & Read Mode
"Write & read" is similar to "write" in that a file can be created or truncated depending on whether it exists initially, but unlike "write" mode the content of the file can also be read.

# Append Mode
"Append" mode is similar to "write" mode in that a new file can be created if the referenced file does not already exist, but where it differs from "write" mode is that you can reference a file that already exists and not truncate the content of that file. Instead, the cursor is moved to the end of the file by default, which allows for adding new content to the file without erasing the previous content.

# Append & Write
Similar to "write & read", "append & read" functions the same as "append" with the ability to also read data from the file.
