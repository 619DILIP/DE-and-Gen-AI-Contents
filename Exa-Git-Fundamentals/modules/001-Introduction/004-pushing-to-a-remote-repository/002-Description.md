<br>

The git push command is used to upload local repository content to a remote repository. Pushing is how you transfer commits from your local repository to a remote repo. The fetch and push commands are counterparts; fetch imports remote commits to the local repository while push exports local commits to the remote repository. 

### Git push usage

```bash
git push <remote> <branch>
```

Push the specified `<branch>` to `<remote>`, along with all of the necessary commits and internal objects. 

```bash
git push <remote> --all
```

Push all of your local branches to the specified remote.

Git push is one component of many used in the overall Git "syncing" process. The syncing commands operate on remote branches which are configured using the git remote command. git push can be considered an 'upload' command whereas, git fetch and git pull can be thought of as 'download' commands. Once change sets have been moved via a download or upload a git merge may be performed at the destination to integrate the changes.

