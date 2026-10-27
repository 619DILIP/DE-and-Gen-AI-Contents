<br>

This is a practical example of git push and an optional exercise.

- Start by creating a new repository on GitHub. If you’re not already logged into your GitHub account, the link will take you to the login page. Just sign in to continue.
- Open your Git Bash
- Create your local project in your desktop directed towards a current working directory
  - pwd stands for 'print working directory', which is used to print the current directory.
  - If necessary, move to the specific path in your local computer by cd 'path_name'. 
  - Create or copy some files into this directory. You don't have to do this step in GitBash; you can use a file explorer GUI instead.

```bash
$ pwd
<prints out current working directory>
$ cd 'path name' // replace path name with the desired directory for working with Git
```

- Initialize the git repository
  - Use git init to initialize the repository. 
  - It is used to create a new empty repository or directory consisting of files' with the hidden directory. 
  - '.git' is created at the top level of your project, which places all of the revision information in one place.
```bash
$ git init
```
- Add the file to the new local repository
  - Use git add . in your bash to add all the files to the given folder.
  - Use git status in your bash to view all the files which are going to be staged to the first commit.
```bash
$ git add .
$ git status
```

- Commit the files staged in your local repository by writing a commit message
  - You can create a commit message by git commit -m 'your message', which adds the change to the local repository.
  - git commit uses '-m' as a flag for a message to set the commits with the content where the full description is included. It is recommended that you write in double-quotes an imperative sentence in 50 characters that describes what changed and why. For example, "Corrected println error in helloworld.java"
```bash
git commit -m 'your message"
```

- Push the code in your local repository to GitHub
  - git push is used for pushing local content to GitHub.

```bash
git push
```
