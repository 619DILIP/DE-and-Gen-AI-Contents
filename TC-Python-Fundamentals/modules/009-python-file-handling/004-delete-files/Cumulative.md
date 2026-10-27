<details><summary>Learning Objectives</summary>

After completing this module, associates should be able to:
- Delete files and directories via Python

</details>

<details><summary>Description</summary>

Python provides the option to delete files and directories via the "os" module.

## "os" Module
The "os" module has far more functionality than just removing files and directories, but these features will be the focus of this module. The "os" module requires importing into your code before you can use it.

Once imported, it provides helpful methods for removing files and directories, and it also has methods for discovering which files and directories are available to you.

</details>
<details><summary>Real World Application</summary>

Applications have a tendency to build up temporary files that become obsolete over time. Many of these apps do a good job of cleaning up these temporary files and removing them from your computer; without the cleanup, your laptop would slowly become inundated with unnecessary files that take up valuable space. During runtime, it can also be helpful to store information inside temporary files, but since these files are only temporary, they should be deleted when they are no longer needed. This is the benefit of deleting files programmatically: it gives you greater flexibility in how you work with data and helps you keep your computer and virtual workspace organized.

</details>
<details><summary>Implementation</summary> 

The first thing you have to do is import the "os" module
```python
import os
```
Typically, you would want to confirm that the file you wish to destroy exists before attempting to destroy it
```python
import os

if os.path.exists("file-to-delete.txt"):
 os.remove("file-to-delete.txt")
```
You can do the same for directories, though instead of using the remove function, you use the rmdir method
```python
import os

if os.path.exists("directory-to-delete"):
 os.rmdir("directory-to-delete")
```
Both options will raise a FileNotFoundError if a non-existent resource is provided. If you try to remove a directory, you will get a PermissionError, and if you try to rmdir a directory that has files in it, you will get an OSError.

</details>
<details><summary>Summary</summary> 

- Import the "os" module if you want to remove files or directories
- Use the remove function to delete files
- Use the rmdir function to delete empty directories

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
