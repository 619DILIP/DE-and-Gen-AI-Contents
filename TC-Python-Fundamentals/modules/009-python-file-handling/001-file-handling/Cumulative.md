<details><summary>Learning Objectives</summary>

After completing this module, associates should be able to:
- Open files using Python
- Understand the differences between read, write, and append mode

</details>

<details><summary>Description</summary>

A file has two key properties: a filename (usually written as one word) and a path. The path specifies the location of a file on the computer. For example, you could have a file called "myproject.docx" in the path `C:\Users\project\Documents`. The part of the filename after the last period is called the file's extension and tells you a file's type. The filename "myproject.docx" is a Word document: "Users", "project", and "Documents" all refer to folders (also called directories).

## Text Files
Each line of a text file includes a sequence of characters that form the file. Each line of a file is terminated with a special character, called the EOL or End of Line character, like a comma `{,}` or a newline character. It ends the current line and tells the interpreter a new one has begun. 

When opening files, you need to decide what "mode" to use to open the file. There are six options:
- `r`: open an existing file for a read operation.
- `w`: open an existing file for a write operation. If the file already contains some data, then it will be overridden.
- `a`: open an existing file for an append operation. It won't override existing data.
- `r+`: to read and write data into the file. The previous data in the file will be overridden.
 - The cursor will start at the beginning of the file.
 - If the file does not exist, an error will be raised.
- `w+`: to write and read data. It will override existing data.
 - If the file does not exist, a new file will be created.
 - If the file does exist, its data will be truncated.
- `a+`: to append and read data from the file.

</details>
<details><summary>Real World Application</summary>

You can't always expect data to take the form necessary for your application: often, you will need to transform data into a compatible format. This will typically require opening the file or files with the data you need and parsing through the content to find what you need. 

Alternatively, when you need to provide others with data, you will more likely than not be required to provide data in a human-friendly format. This means you need to know how to create files and fill them with the necessary data in whatever expected format you or your company uses. 

</details>
<details><summary>Implementation</summary> 

# Ways to interact with files
There are two basic ways to interact with a file:
```python
# option one
my_file = open("to_open.txt", "r")

for line in my_file:
    print(line)

my_file.close()
```
```python
# option two
with open("to_open.txt", "r") as my_file:
    for line in my_file:
        print(line)
```
The key difference between the two is that the second option will automatically close the file when your code is done.

</details>
<details><summary>Summary</summary> 

- Each line of a file includes a sequence of characters that form the file. 
- Each line of a file is terminated with an EOL character.
- You can manually open and close a file in your code, or use the "with" keyword to close the file when you are done with it automatically.

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
