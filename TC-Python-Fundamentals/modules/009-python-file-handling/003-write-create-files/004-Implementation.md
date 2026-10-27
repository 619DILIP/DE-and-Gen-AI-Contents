## Write
To create or open a file in write mode you simply set the mode to "w" and provide the relative name/path to the file
```python
# each time this code is executed a file called new_file.txt will have the first and second lines added, with previous content erased
with open("new_file.txt", "w") as new_file:
    new_file.write("first line\n")
    new_file.write("second line")
```
While in write mode you can use the seek method to change your cursor position: any write commands you do will overwrite previous data
```python
with open("new_file.txt", "w") as new_file:
    new_file.write("first write\n")
    new_file.write("second write\n")
    new_file.seek(0) # moves the cursor to the start of the file
    new_file.write("third write\n") # this will overwrite the "first write" text
    new_file.write("write") # this will overwrite "secon" in the second write statement
```

## Append
The code you write for "append" mode is going to look similar to the code for "write" mode, with the main difference being that the file you work with will not have its data truncated
```python
# each time this code is executed a file called new_file.txt will have the first and second lines appended to the end of the file, with old content untouched
with open("new_file.txt", "a") as new_file:
    new_file.write("first line\n")
    new_file.write("second line")
```
Keep in mind the behavior of the write method is consistent whether in "write" or "append" mode, so if you move the cursor to a line with data and write over it the old content will be replaced with whatever new data you write in.