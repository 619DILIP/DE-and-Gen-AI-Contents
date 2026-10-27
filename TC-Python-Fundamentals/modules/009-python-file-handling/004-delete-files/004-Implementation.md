First thing you have to do is import the "os" module
```python
import os
```
typically you would want to confirm that the file you want destroyed actually exists before attempting to destroy it
```python
import os

if os.path.exists("file-to-delete.txt"):
    os.remove("file-to-delete.txt")
```
you can do the same for directories, though instead of using the remove function you use the rmdir method
```python
import os

if os.path.exists("directory-to-delete"):
    os.rmdir("directory-to-delete")
```
both options will raise a FileNotFoundError if a non-existent resource is provided. If you try to remove a directory you will get a PermissionError, and if you try to rmdir a directory that has files in it you will get an OSError.