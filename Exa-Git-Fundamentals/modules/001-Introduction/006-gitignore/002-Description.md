<br>

The `.gitignore` file is a text file that tells Git which files or folders to ignore in a project. Files already tracked by Git are not affected. Each line in a `gitignore` file specifies a pattern. When deciding whether to ignore a path, Git normally checks gitignore patterns from multiple sources, with the following order of precedence, from highest to lowest.

Whatever files and folders from any project you want to ignore those files you will place in the `.gitignore` file by using the following patterns.

- `*` is used as a wildcard match.
- `/` is used to ignore pathnames relative to the `.gitignore` file.
- `#` is used to add comments to a `.gitignore` file.
- `**` can be used to match any number of directories.
- `!` to negate a file that would be ignored.
```properties
*.log
!example.log
```
In this example, example.log is not ignored, even though all other files ending with .log are ignored.