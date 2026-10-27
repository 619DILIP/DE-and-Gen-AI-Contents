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