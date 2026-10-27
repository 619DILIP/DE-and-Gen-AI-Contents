<details><summary>Learning Objectives</summary>

After completing this module, associates should be able to:
- Add content to files in write mode


</details>

<details><summary>Description</summary>

# Write Mode
The "write" mode is used in the open function when you need to add content to a file, and it can also be used to create the file. If the file referenced in the open function does not exist, it will be created; if it does exist, the content of the file will be truncated (removed).

# Write & Read Mode
"Write & read" is similar to "write" in that a file can be created or truncated depending on whether it initially exists, but unlike "write" mode, the content of the file can also be read.

# Append Mode
"Append" mode is similar to "write" mode in that a new file can be created if the referenced file does not already exist, but where it differs from "write" mode is that you can reference a file that already exists without truncating the content of that file. Instead, the cursor is moved to the end of the file by default, allowing for the addition of new content to the file without erasing the previous content.

# Append & Write
Similar to "write & read," "append & read" functions the same as "append" with the ability to also read data from the file.

</details>
<details><summary>Real World Application</summary>

It is common practice to save important information inside files outside of the application that needs the file's data. This could include your logs, a test report, quarterly earnings; the list goes on. Ultimately, you will need to produce information in a format that is human-friendly, so you need to be able to write data to files.

</details>
<details><summary>Implementation</summary> 

## Write
To create or open a file in write mode, you simply set the mode to "w" and provide the relative name/path to the file
```python
# Each time this code is executed, a file called new_file.txt will have the first and second lines added, with previous content erased.
with open("new_file.txt", "w") as new_file:
 new_file.write("first line\n")
 new_file.write("second line")
```
While in write mode, you can use the seek method to change your cursor position: any write commands you execute will overwrite previous data
```python
with open("new_file.txt", "w") as new_file:
 new_file.write("first write\n")
 new_file.write("second write\n")
 new_file.seek(0)  # moves the cursor to the start of the file
 new_file.write("third write\n")  # this will overwrite the "first write" text
 new_file.write("write")  # this will overwrite "second" in the second write statement
```

## Append
The code you write for "append" mode is going to look similar to the code for "write" mode, with the main difference being that the file you work with will not have its data truncated
```python
# Each time this code is executed, a file called new_file.txt will have the first and second lines appended to the end of the file, with old content untouched.
with open("new_file.txt", "a") as new_file:
 new_file.write("first line\n")
 new_file.write("second line")
```
Keep in mind that the behavior of the write method is consistent whether in "write" or "append" mode, so if you move the cursor to a line with data and write over it, the old content will be replaced with whatever new data you write.

</details>
<details><summary>Summary</summary>

- Content can be added to files by opening the file in "write" or "append" mode.
- "Write" mode will create a new file or truncate an existing file when it is opened.
- "Append" mode will create a new file or set the cursor to the end of an existing file when it is opened.
- `w+` and `a+` respectively will also allow you to perform a read action on the file.
- Any write action will overwrite pre-existing data.

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
