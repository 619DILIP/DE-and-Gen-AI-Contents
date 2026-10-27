<details><summary>Learning Objectives</summary>
<br>

After completing this module, associates should be able to:
- Explain the `.gitignore` file and its purpose.

</details>
<details><summary>Description</summary>
<br>

The `.gitignore` file is a text file that tells Git which files or folders to ignore in a project. Files already tracked by Git are not affected. Each line in a `.gitignore` file specifies a pattern. When deciding whether to ignore a path, Git normally checks gitignore patterns from multiple sources, with the following order of precedence, from highest to lowest.

You can place any files and folders from your project that you want Git to ignore in the `.gitignore` file using the following patterns:

- `*` is used as a wildcard match.
- `/` is used to ignore pathnames relative to the `.gitignore` file.
- `#` is used to add comments to a `.gitignore` file.
- `**` can be used to match any number of directories.
- `!` is used to negate a file that would otherwise be ignored.

```properties
*.log
!example.log
```
In this example, `example.log` is not ignored, even though all other files ending with `.log` are ignored.

</details>
<details><summary>Real World Application</summary>
<br>

The `.gitignore` file is essential for managing a Git repository effectively. Here's why it's important:

- **Preventing Unnecessary Files from Being Tracked**: The `.gitignore` file allows you to specify patterns for files or directories that Git should ignore. This prevents unimportant or generated files (e.g., build artifacts, log files, temporary files) from being accidentally tracked by Git. Ignoring such files helps keep the repository clean and focused on versioning the source code and essential project files.

- **Reducing Repository Size**: By ignoring unnecessary files, you reduce the size of your Git repository. This is especially important when working with large binary files or auto-generated files that frequently change. Ignoring these files can significantly reduce the repository's size, making cloning, fetching, and pushing operations faster and more efficient.

- **Avoiding Accidental Commits of Sensitive Information**: The `.gitignore` file helps prevent accidental commits of sensitive information such as passwords, API keys, and configuration files containing sensitive data. By explicitly ignoring files containing sensitive information, you reduce the risk of exposing confidential data in the version control system.

In summary, the `.gitignore` file is crucial for maintaining a clean, efficient, and secure Git repository. It helps prevent unnecessary files from being tracked, reduces repository size, and avoids accidental commits of sensitive information.

</details>
<details><summary>Implementation</summary> 
<br>

In this section, you will learn how the `.gitignore` file works with step-by-step examples. This is an optional exercise.

- First, go to your [GitHub](https://github.com/) and create a new repository called `GitIgnoreDemo`. Copy the HTTPS URL to clone the project into VS Code.

**Note:** You must first download and install Git. After that, add the Git extension to your VS Code as well. Alternatively, you can also download Git Bash.

- Open VS Code, go to "Open Folder," create a folder called `gitignoreexampledemo`, and select it.
- Clone the project using the following git clone command and check `git status` in your VS Code terminal.

```bash
git clone repository-HTTPS-URL
```

```bash
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo> git clone https://github.com/SrikanthMidathapalli/GitIgnoreDemo.git
Cloning into 'GitIgnoreDemo'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (3/3), done.
```

- The GitHub repository is successfully cloned into your local system. Now check the status by using the `git status` command. You will probably see the following error—don't worry, it is asking you to initialize git.

```bash
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo> git status
fatal: not a git repository (or any of the parent directories): .git
```

- Initialize git using the `git init` command.

```bash
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo> git init
Initialized empty Git repository in C:/Users/SrikanthMidathapalli/Desktop/gitignoreexampledemo/.git/
```

- Now create a file called `HelloWorld.java` and check the git status.

```bash
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo> git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        GitIgnoreDemo/

nothing added to commit but untracked files present (use "git add" to track)
```

**Note:** "Untracked files" means that Git does not know about them.

- Now you can see the untracked file that we newly created inside the `GitIgnoreDemo/` folder. Change to the `GitIgnoreDemo` folder, and then we can see the untracked file `HelloWorld.java` as shown below.

```bash
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo> cd .\GitIgnoreDemo\
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git status
On branch main
Your branch is up to date with 'origin/main'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        HelloWorld.java

nothing added to commit but untracked files present (use "git add" to track)
```

- We know from Git basics that for any untracked files we want Git to track, we add those files for tracking using the following git commands:

```bash
git add file-name // if we want to track one file
git add . // if we want all files to be tracked
```

- Here I am using the `git add HelloWorld.java` command to track my file, and after that, I am checking the status using the `git status` command.

```bash
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git add HelloWorld.java
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git status
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   HelloWorld.java
```

- Now the file is ready to commit, but let me add some content and check the status of the file.

```bash
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git status
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   HelloWorld.java

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   HelloWorld.java
```

- If you observe, the file is already ready to commit, and the same file is not staged for commit. This is because we already know that Git works with snapshots of data.

- Now you can run `git add HelloWorld.java` again and check the status as shown below:

```bash
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git add HelloWorld.java
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git status
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   HelloWorld.java
```

- If you want to unstage the file, you can use the restore command as well.
- Now use the following git command to commit the changes and save the files in your local system as shown below:

```bash
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git commit -m "initial commit"
[main aa8ab33] initial commit
 1 file changed, 5 insertions(+)
 create mode 100644 HelloWorld.java
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git status
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

- Now your local files are ready to be pushed to the remote repository. As we know, we use push or pull git commands to transfer files from our local system to the remote repository.

- Now let's consider a scenario where your project has some log files that are not important to push to the repository. To avoid including these files, you need Git to ignore them. This is where the `.gitignore` file comes in—let's see it in detail.

- Create a file called `user.log` inside the `GitIgnoreDemo` folder and create a `.gitignore` file as well. Check `git status` and you will see both files are untracked.

```bash
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git status
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore
        user.log

nothing added to commit but untracked files present (use "git add" to track)
```

- Now write `user.log` inside the `.gitignore` file and check `git status`:

```bash
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git status
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore

nothing added to commit but untracked files present (use "git add" to track)
```

**Note:** The status shows that you have committed some files that are ready to push to the remote repository:
```bash 
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)
```

- You can see only one file, `.gitignore`, needs to be tracked. Now add this file for tracking using the `git add -A` or `git add .` git commands as shown below and check the `git status`.

```bash
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git add -A
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git add .  
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git status
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   .gitignore
```

- Now the file is ready to commit. Run the same `git commit -m "initial gitignore commit"` command and check `git status`.

```bash
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git commit -m "initial gitignore commit"
[main 16e5398] initial gitignore commit
 1 file changed, 1 insertion(+)
 create mode 100644 .gitignore
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git status
On branch main
Your branch is ahead of 'origin/main' by 2 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

- Now it's time to check if Git is tracking any modifications you make to the `user.log` file.

- Open the `user.log` file, add some content, save the file, and check the `git status` as shown below.

```bash
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git status
On branch main  
Your branch is ahead of 'origin/main' by 2 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

- No files are showing as modified because you added the `user.log` file to the `.gitignore` file, so Git is ignoring it and not tracking that modified file.

- This helps when you are working on a project and want files to not be tracked by Git—you place those files in the `.gitignore` file.

Similarly, create a folder called `users/` and add one more file inside the `users/` folder like `logginguser.log` (that is, `users/logginguser.log`). Follow the commands provided below.

- Before the `users/` folder is written in the `.gitignore` file, it will show:

```bash
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git status
On branch main
Your branch is ahead of 'origin/main' by 2 commits.
  (use "git push" to publish your local commits)

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        users/

nothing added to commit but untracked files present (use "git add" to track)
```

- After the `users/` folder is written in the `.gitignore` file:

```bash
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git status
On branch main
Your branch is ahead of 'origin/main' by 2 commits.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   .gitignore

no changes added to commit (use "git add" and/or "git commit -a")
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git add -A
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git add .
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git commit -m "updated gitignore commit"
[main ac1268b] updated gitignore commit
 1 file changed, 2 insertions(+), 1 deletion(-)
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git status 
On branch main
Your branch is ahead of 'origin/main' by 3 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

- Now open the `logginguser.log` file, write some content, and check the `git status`. You will see that there is no modification message.

```bash
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git status
On branch main
Your branch is ahead of 'origin/main' by 3 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

- This confirms that any files you want Git to ignore can be placed inside the `.gitignore` file.

- To demonstrate ignore patterns, create a file called `user1.log`. Inside the `.gitignore` file, instead of adding individual files like `user.log` and `user1.log`, you can use a wildcard like `*.log`. This way, any files with a `.log` extension will be ignored.

</details>
<details><summary>Summary</summary> 
<br>

- The `.gitignore` file is a text file that tells Git which files or folders to ignore in a project. 
- Using `.gitignore` can help keep the repository clean and focused on versioning the source code and essential project files.
- Using `.gitignore` can help reduce the repository's size, making cloning, fetching, and pushing operations faster and more efficient.
- The `.gitignore` file helps prevent accidental commits of sensitive information such as passwords, API keys, and configuration files containing sensitive data.

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>