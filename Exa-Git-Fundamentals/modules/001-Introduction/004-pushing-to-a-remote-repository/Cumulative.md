<details><summary>Learning Objectives</summary>

<br>

After completing this module, associates should be able to:

- Explain how to push content to a repository in Git.
- Use Git to push new content into an existing repository.
</details>
<details><summary>Description</summary>
<br>

The `git push` command is used to upload local repository content to a remote repository. Pushing is how you transfer commits from your local repository to a remote repo. The `fetch` and `push` commands are counterparts; `fetch` imports remote commits to the local repository while `push` exports local commits to the remote repository. 

### Git push usage

```bash
git push <remote> <branch>
```

Push the specified `<branch>` to `<remote>`, along with all the necessary commits and internal objects. 

```bash
git push <remote> --all
```

Push all of your local branches to the specified remote.

`git push` is one component of many used in the overall Git "syncing" process. The syncing commands operate on remote branches that are configured using the `git remote` command. `git push` can be considered an 'upload' command, whereas `git fetch` and `git pull` can be thought of as 'download' commands. Once change sets have been moved via a download or upload, a `git merge` may be performed at the destination to integrate the changes.

</details>
<details><summary>Real World Application</summary>

<br>

The following are bookmarks for videos on learning how to handle remote repositories in Git:

[Cloning through VS Code](https://www.youtube.com/watch?v=RGOj5yH7evk&t=870s)

[Git commit command](https://www.youtube.com/watch?v=RGOj5yH7evk&t=1050s)

[Git add command](https://www.youtube.com/watch?v=RGOj5yH7evk&t=1220s)

[Committing](https://www.youtube.com/watch?v=RGOj5yH7evk&t=1155s)

[Git push command](https://www.youtube.com/watch?v=RGOj5yH7evk&t=1220s)

[SSH Keys](https://www.youtube.com/watch?v=RGOj5yH7evk&t=1230s)

[Git push](https://www.youtube.com/watch?v=RGOj5yH7evk&t=1525s)

[Review workflow](https://www.youtube.com/watch?v=RGOj5yH7evk&t=1821s)

[Comparison between GitHub workflow and local Git workflow](https://www.youtube.com/watch?v=RGOj5yH7evk&t=1900s)

[Git branching](https://www.youtube.com/watch?v=RGOj5yH7evk&t=1962s)

[Undoing in Git](https://www.youtube.com/watch?v=RGOj5yH7evk&t=3390s)

[Forking in Git](https://www.youtube.com/watch?v=RGOj5yH7evk&t=3710s)
</details>
<details><summary>Implementation</summary> 

<br>

This is a practical example of `git push` and an optional exercise.

- Start by creating a new repository on GitHub. If you’re not already logged into your GitHub account, the link will take you to the login page. Just sign in to continue.
- Open your Git Bash.
- Create your local project on your desktop directed towards a current working directory.
  - `pwd` stands for 'print working directory', which is used to print the current directory.
  - If necessary, move to the specific path on your local computer by using `cd 'path_name'`. 
  - Create or copy some files into this directory. You don't have to do this step in Git Bash; you can use a file explorer GUI instead.

```bash
$ pwd
<prints out current working directory>
$ cd 'path name' // replace path name with the desired directory for working with Git
```

- Initialize the Git repository.
  - Use `git init` to initialize the repository. 
  - It is used to create a new empty repository or directory consisting of files with the hidden directory. 
  - `.git` is created at the top level of your project, which places all of the revision information in one place.
```bash
$ git init
```
- Add the files to the new local repository.
  - Use `git add .` in your bash to add all the files to the given folder.
  - Use `git status` in your bash to view all the files that are going to be staged for the first commit.
```bash
$ git add .
$ git status
```

- Commit the files staged in your local repository by writing a commit message.
  - You can create a commit message using `git commit -m 'your message'`, which adds the changes to the local repository.
  - `git commit` uses `-m` as a flag for a message to set the commits, where the full description is included. It is recommended that you write in double quotes an imperative sentence within 50 characters that describes what changed and why. For example, "Corrected println error in HelloWorld.java".
```bash
git commit -m "your message"
```

- Push the code in your local repository to GitHub.
  - `git push` is used for pushing local content to GitHub.

```bash
git push
```
</details>
<details><summary>Summary</summary> 
<br>

- The `git push` command is used to upload local repository content to a remote repository. 
- Pushing is how you transfer commits from your local repository to a remote repo. 
- It's the counterpart to `git fetch`, but whereas fetching imports commits to local branches, pushing exports commits to remote branches.
- Pushing has the potential to overwrite changes; caution should be taken when pushing.
- `git push` is one component of many used in the overall Git "syncing" process. 
  - The syncing commands operate on remote branches that are configured using the `git remote` command. 
  - `git push` can be considered an 'upload' command, whereas `git fetch` and `git pull` can be thought of as 'download' commands. 
  - Once change sets have been moved via a download or upload, a `git merge` may be performed at the destination to integrate the changes.
</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
