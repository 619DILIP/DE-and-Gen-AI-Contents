# Reading the Contents of Files
When you open a file in read mode, you can view the contents of the file, but you can't change it. This is a convenient way of ensuring you don't accidentally adjust the contents of the file. Since writing to a file tends to be a more process-intensive operation, file reads tend to be faster.

# Read vs Read & Write
The "r" (read) and "r+" (read and write) mode types will both provide read access to your file, but "r+" will also allow you to edit the contents of the file. This is useful if you want to create edits to the file without truncating the contents before you start adding new data.