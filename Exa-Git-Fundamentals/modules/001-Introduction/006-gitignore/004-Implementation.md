<br>

In this section, you will learn about how the `.gitignore` file will work with examples step-by-step. This is an optional exercise.

- First, go to your [https://github.com/](https://github.com/) and create a new repository `GitIgnoreDemo`. Copy the HTTPS URL to clone the project into the VS Code.

***`Note:`*** First you must download a git and install. After that add the git extension in your VS Code as well. Otherwise, you can also download git bash.
- Open your VS code go to open folder create a folder `gitignoreexampledemo` and select it.
- Clone the project using the following git clone command and check `git status` in your VS code terminal.
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
- The GitHub repository is successfully cloned into your local system. Now Check the status by using the `git status` command. You probably see the following error do not worry it is asking to initialize the git.
```bash
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo> git status
fatal: not a git repository (or any of the parent directories): .git
```
- Initialize the git using the `git init` command.
```bash
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo> git init
Initialized empty Git repository in C:/Users/SrikanthMidathapalli/Desktop/gitignoreexampledemo/.git/
```

- Now create a file `HelloWorld.java` and check the git status.
```bash
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo> git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        GitIgnoreDemo/

nothing added to commit but untracked files present (use "git add" to track)
```
***`Note:`*** Here untracked files means that git does not know them.
- Now you can see the untracked file which we newly created inside the `GitIgnoreDemo/` folder now change the folder to `GitIgnoreDemo` then we can see the untracked file `HelloWorld.java` as shown below.
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
- We all know that from git basics any untracked files we want git to track we will add those files to track by using the following git command.
```bash
git add file-name // if we want to track one file
git add . // if we want all the files should be tracked
```
- Here I am using the `git add HelloWorld.java` command to track my file and after that, I am seeing the status by using the `git status` command.
```bash
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git add HelloWorld.java
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git status
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   HelloWorld.java
```
- Now the file is ready to commit, but now let me add some content and check the status of the file.
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
- Here If you observe that the file is already ready to commit and the same file is not staged for commit it's because we already know that git works with data.
- Now you can do again `git add HelloWorld.java` and check the status as shown below
```bash
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git add HelloWorld.java
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git status
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   HelloWorld.java
```
- Here if you want to unstage the file you can follow the restore command as well
- Now use the following git command to change the commit to save the files in your local system as shown below.
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
- Now your local file is ready to push and pull them to the remote repository. As we know that we will use push or pull git commands to push the files from our local system to the remote repository.
- Now let's consider a scenario where in your project you are having some log files which are not important to push to the repository. Therefore to achieve that you need to ignore those files that are saved inside the project folders. here you need a git that needs to ignore the files. To achieve this we use the `.gitignore` let's see in detail
- Create a file which is a `user.log` inside the `GitIgnoreDemo` and create the file `.gitignore` as well and check `git status` you will see both files are untracked.
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
- Now write the `user.log` inside the `.gitignore` file and check `git status` 
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
***`Note:`*** Here it says that you have committed some files that are ready to push into the remote repository. 
```bash 
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)
```
- you can see only one file which is `.gitignore` has to be tracked. Now you just add this file to tracked using the `git add -A` and `git add .` git commands as shown below and check the `git status`.
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
- Now the file is ready to commit just to do the same `git commit -m "initial gitignore commit` and check `git status`.
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
- Now it's time to check if any modifications that you have performed on the `user.log` file git are tracking that file or not.
- Open the `user.log` file and add some content and save the file and check the `git status` as shown below.
```bash
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git status
On branch main  
Your branch is ahead of 'origin/main' by 2 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```
- None of the files are showing that files are modified its because you have added the `user.log` file in the `.gitignore` file so git is ignoring it to track that modified file.
- This helps you when you are working on the project and you want that the files which you worked on are not to tracked by git we will use this file `.gitignore`.
Similarly, create a folder `users/` and add one more file inside the `users/` folder like `logginguser.log`. that is `users/logginguser.log`. Perform the following commands as provided below.
- Before the `users/` folders are written in the `.gitignore` file it will show
```bash
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git status
On branch main
Your branch is ahead of 'origin/main' by 2 commits.
  (use "git push" to publish your local commits)

Untracked files:
  (use "git add <file>..." to include what will be committed)
        users/

nothing added to commit but untracked files present (use "git add" to track)
```
- After `users/` folder written `.gitignore` file.
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
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git commit -m "initial gitignore commit"
[main ac1268b] initial gitignore commit
 1 file changed, 2 insertions(+), 1 deletion(-)
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git status 
On branch main
Your branch is ahead of 'origin/main' by 3 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```
- Now open the `userlogging.log` file and write some content and check for the `git status` you see that no modified message.
```bash
PS C:\Users\SrikanthMidathapalli\Desktop\gitignoreexampledemo\GitIgnoreDemo> git status
On branch main
Your branch is ahead of 'origin/main' by 3 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```
- By this, you can say that whatever files you want that git to ignore to track those you can place inside the `.gitignore` file.
- To demonstrate the ignore patterns create a file `user1.log` file inside the `.gitignore` file instead of adding individual files like `user.log` and `user1.log` you can use a wildcard like `*.log` inside the `.gitignore` here whatever the files are named `.log` those files will be ignored.
