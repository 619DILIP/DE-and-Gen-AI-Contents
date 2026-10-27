# Cumulative for the  Guided Coding Example Git Workflow
<details><summary>Description</summary>

# GFT-GCE-WRKFLW
# Git Fundamentals - Git Workflow

### Contributors:
Richard Hawkins
{ Reviewers }

## Prerequisites
- Bash terminal with git installed - for most associates, installing a gitBash terminal emulator is the fastest and easiest way to accomplish this. For mac users, a zsh terminal will accept bash commands.
- [GitHub account](https://www.github.com)

# How to Complete
## 1. Create a new repository...
and navigate to it. The method of creation is not of importance, so whatever method you are most comfortable with or would like to demonstrate for the batch is fine.

## 2. Run the command...
`git status` from within the repo to report the status of the new repository to the terminal.

## 3. Create a README.md...
with some simple content in it. This should be manually created to demonstrate the git workflow, rather than allow GitHub to create a readme file as part of the repo creation.
```
~/NewRepo/README.md

Hello World!
```

## 4. Run the command...
`git add .` to add the readme file to the git staging area. Follow adding the file with `git status` to view the changes to the reported status.

## 4. Run the command...
`git commit` to commit the changes made and staged. Use the `-m` flag followed by a string (`"{string}"`) to include a commit message. Again, follow creating the commit with the `git status` command to demonstrate the changes.

## 5. Run the command...
`git push` to push local commits to a remote repository. Depending on how you created the repo in step 1 you may need to set the upstream address before you can push to the remote repository. Use `git status` to demonstrate the changes. You can also view the repository in a browser to view the current contents of the remote copy of the repository.

## 6. Create a new file...
and include some new content. You may also want to modify the existing readme file to also demonstrate changes to exiting content in the repo. Once modified/created, add, commit, and push your changes to the remote.

## 7. Create a new branch...
based off the Main branch you have been modifying so far. Use `git branch -M NewBranch` to create a new local branch, the use `git switch NewBranch` to swap to it. *You could also use `git checkout -b NewBranch` to acccomplish both steps in one command*
In the new branch make some simple changes to the existing files, or create a new file to hilight the different branches. Add, commit, and push those changes to the new branch.

## 8. View The Two Branches...
noting the differences that are on NewBranch that are not on Main.

## 9. Create a Pull Request...
to merge NewBranch back into the Main branch. Review the PR through the browser, and demonstrate a merge process through the browser. *You could also use `git merge NewBranch` from the Main branch to begin the merge process from the local repo. Once complete, you simply push the resulting merge commit to the remote repo with `git push`.*
</details>
