
### Git Merge

Merging is Git's way of putting a forked history back together again. The git merge command lets you take the independent lines of development created by git branch and integrate them into a single branch.

Note that all of the commands presented below merge into the current branch. The current branch will be updated to reflect the merge, but the target branch will be completely unaffected. Again, this means that git merge is often used in conjunction with git checkout for selecting the current branch and git branch -d for deleting the obsolete target branch.

### How it works
Git merge will combine multiple sequences of commits into one unified history. In the most frequent use cases, git merge is used to combine two branches. The following examples in this document will focus on this branch merging pattern. In these scenarios, git merge takes two commit pointers, usually the branch tips, and will find a common base commit between them. Once Git finds a common base commit it will create a new "merge commit" that combines the changes of each queued merge commit sequence.

### New merge commit node
Merge commits are unique against other commits in the fact that they have two parent commits. When creating a merge commit Git will attempt to auto magically merge the separate histories for you. If Git encounters a piece of data that is changed in both histories it will be unable to automatically combine them. This scenario is a version control conflict and Git will need user intervention to continue. 

### Preparing to merge
Before performing a merge there are a couple of preparation steps to take to ensure the merge goes smoothly.
- Confirm the receiving branch
  - Execute git status to ensure that you are pointing to the correct merge-receiving branch. 
  - If needed, execute git checkout to switch to the receiving branch.
- Fetch latest remote commits
  - Make sure the receiving branch and the merging branch are up-to-date with the latest remote changes. 
  - Execute git fetch to pull the latest remote commits. 
  - Once the fetch is completed ensure the main branch has the latest updates by executing git pull.

### Merging
Once the previously discussed "preparing to merge" steps have been taken a merge can be initiated by executing git merge 