# GFT-GCE-IGNORE
# Git Fundamentals - .gitignore

### Contributors:
Richard Hawkins
{ Reviewers }

## Prerequisites
- Bash terminal with git installed - for most associates, installing a gitBash terminal emulator is the fastest and easiest way to accomplish this. For mac users, a zsh terminal will accept bash commands.
- [GitHub account](https://www.github.com)

# How to Complete
## 1. Create a repository...
or select an existing repository **that does NOT have a .gitignore file**.

## 2. Create a new file...
`DoNotIgnore.md` with some simple content. A `.md` or `.txt` file will work best, but any file that can be modified easily for demonstrations will work.

```
~/SampleRepo/DoNotIgnore.md

I'm important! Don't ignore me!
```

## 3. Create a second new file...
`IgnoreMe.md` with similar dummy content.

```
~/SampleRepo/IgnoreMe.md

I'm not important, you can ignore me!
```
## 4. Creat a `.gitignore` file...
in the root level of the repository. Add the `IgnoreMe.md` file to the .gitignore.


```
~/SampleRepo/.gitignore

IgnoreMe.md
```

## 5. Add, commit, and push...
the new files to the repo. Use `git status` commands after adding and committing to monitor the progress of the new files. Highlight the inclusion of the `.gitignore` and `DoNotIgnore.md` files, and the exclusion of the `IgnoreMe.md`file from the process.

## 6. Discuss the applications...
of the `.gitignore` file for the exclusion of undesired files in a repo. Highlight common use cases, like system configuration and build artifacts.

## 7. Generate a folder...
named `TmpDir` and move the `IgnoreMe.md` file from the root of the repo into the new folder.

```
-SampleRepo
|-.gitignore
|-DoNotIgnoreMe.md
|-TmpDir
  |-IgnoreMe.md
```

## 8. Add `TmpDir`...
to the repository staging, and use `git status` to review the staging area. *Staging should now include the `IgnoreMe.md` file.*

## 9. Run the command...
`git rm` to remove the `IgnoreMe.md` file from the staging area.

## 10. Update the `.gitignore`...
to include the `IgnoreMe.md` file. This can be done in two steps to demonstrate available options:
- Updating to include the directory path (`/TmpDir/IgnoreMe.md`), and running `git add .` and `git status` to demonstrate the effect.
- Updating to include wildcard characters (`*/IgnoreMe.md`), and again running `git add.` and `git status` to demonstrate effectiveness.

## 11. Add TmpDir...
to the `.gitignore` file to ignore all contents.

```
~/SampleRepo/.gitignore

IgnoreMe.md
/TmpDir/IgnoreMe.md # Direct file path to specify the file and location.
*/IgnoreMe.md # Single wildcard character matches anything EXCEPT the `/` character, requiring specific folder depth.
**/IgnoreMe.md # Double Wildcard matches at any folder depth.
/TmpDir/* # Include all contents in `TmpDir` folder
```

## 12. Create a new file...
`KeepMeToo.md` inside the `TmpDir` folder.

## 13. Update the `.gitignore`...
with an exclusion for the new file. Use `!` characters to specify a pattern to exclude from the `.gitignore`. *Excluding a file from the `.gitignore` will always include it in the repo.*

```
~/SampleRepo/.gitignore

IgnoreMe.md
/TmpDir/IgnoreMe.md # Direct file path to specify the file and location.
*/IgnoreMe.md # Single wildcard character matches anything EXCEPT the `/` character, requiring specific folder depth.
**/IgnoreMe.md # Double Wildcard matches at any folder depth.
/TmpDir/* # Include all contents in `TmpDir` folder
!**/KeepMeToo.* # Use `!` to exclude a pattern from being ignored.
```

# Next Steps
Use this demonstration as a starting point for more practical use of the `.gitignore` file. Review common files and folders that are ignored for your particular tech stack. Consider introducing common resources for template `.gitignore` files. For more complex repository structures (like monorepos, which contain more than one project, or more than one language) consider experimenting with multiple `.gitignore` files in the repo in seeparate folders. More information on `.gitignore` hierarchy is available throuh the [git documentation](https://git-scm.com/docs/gitignore).
