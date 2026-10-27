<br>

- The git push command is used to upload local repository content to a remote repository. 
- Pushing is how you transfer commits from your local repository to a remote repo. 
- It's the counterpart to git fetch, but whereas fetching imports commits to local branches, pushing exports commits to remote branches.
- Pushing has the potential to overwrite changes, caution should be taken when pushing.
- git push is one component of many used in the overall Git "syncing" process. 
  - The syncing commands operate on remote branches which are configured using the git remote command. 
  - git push can be considered and 'upload' command whereas, git fetch and git pull can be thought of as 'download' commands. 
  - Once change sets have been moved via a download or upload a git merge may be performed at the destination to integrate the changes.