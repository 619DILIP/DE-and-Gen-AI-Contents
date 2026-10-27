# Read
```python
with open("my_file.txt", "r") as my_file:
    # do something with the open file
```
You have a few options for reading the content of the file. To access the entirety of the file, you use the read() method
```python
with open("my_file.txt", "r") as my_file:
 content = my_file.read()  # content will be equal to the entirety of the file's data in String form
    print(content)
```
If you only want to access some of the data, you can specify how many characters (starting from the beginning of the file) you want to access
```python
with open("my_file.txt", "r") as my_file:
 content = my_file.read(10)  # content will be equal to the first 10 characters in String form
    print(content)
```
If you want to get the content of the line your cursor is currently on (starting from your cursor position), you can use the readline() method. An empty string is returned if the end of the file has been reached, and an empty line is returned if the only character in the line is a new line character
```python
with open("my_file.txt", "r") as my_file:
 content = my_file.readline()  # content will be equal to the entirety of the first line of the file
    print(content)
```
File objects are iterable, so you can use a for loop to interact with the data of the file line by line
```python
with open("my_file.txt", "r") as my_file:
    for line in my_file:
        # because lines in the file end with a new line character, we need to tell the print
        # function not to add an extra new line character at the end, or you will have an extra 
        # line between the print statements
        print(line, end="") 
```
Alternatively, you can use the readlines() method to return data of the file in a list, where each line is an element of the list, and interact with the data by using the index positions
```python
with open("my_file.txt", "r") as my_file:
 lines = my_file.readlines()
    print(lines)  # will show a list object with the data of each line as a stored String element
```
Just about all actions performed on a File happen about the file cursor. To find out where your cursor is located (how far from the start of the file), you use the tell() method. A 0 result indicates you are at the start of the file.
```python
with open("my_file.txt","r") as my_file:
    print(my_file.tell())
```
To manually change the cursor position, you use the seek() method. This method requires you to give an int indicating how many positions to travel. Still, you can also provide an optional "offset" int to tell Python what position you want to start at when changing the cursor position. You can provide either 0, 1, or 2 as an option:
- 0 (default): moves the cursor starting at the beginning of the file
- 1: moves the cursor starting from its current position
- 2: moves the cursor starting from the end of the file
```python
# Moves the cursor five positions from the start
with open("my_file.txt", "r") as my_file:
 position = my_file.seek(5)
    print(position)  # will print 5
```
Note that by default, text files don't support moving the cursor backwards. To enable this behavior, you will have to open the file in binary mode by appending a "b" to the mode choice. 
```python
# Notice the b appended to the r in the mode indication string
with open("my_file.txt", "rb") as my_file:
 position = my_file.seek(-5,2)
 data = my_file.readline()
    # This will tell us what position the cursor is at and what data remains on the line
    print(position, data) 
```
Opening a file in binary mode is required for any read/write action on non-text-based files. You can still work with text files in binary mode, but some auto-formatting and data conversion will not be performed.

text file content
```txt
line one
line two
line three
line four
```
Same file in binary mode
```python
with open("my_file.txt", "rb") as my_file:
    for line in my_file:
        print(line)
```
```bash
b'line one\r\n'
b'line two\r\n'
b'line three\r\n'
b'line four'
```
Finally, writing to a file will be covered more in-depth elsewhere, but if you want to be able to read and write to a file, the "r+" mode does allow for this
```python
with open("my_file.txt","r+") as my_file:
 my_file.seek(0,2)  # move to the end of the file
 my_file.write("\nline five")  # add a new line and give it some text
 my_file.seek(0)  # move back to the start of the file
    print(my_file.read())  # view the contents of the file in its entirety
```