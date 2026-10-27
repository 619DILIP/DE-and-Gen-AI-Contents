<br>

This video goes through the steps involved in merging branches in Git:
[Merging branches in Git](https://www.youtube.com/watch?v=XX-Kct0PfFc)


# Steps to Resolve a Merge Conflict on GitHub:

Sometimes when working on a project, we make multiple pushes to the remote repository without first pulling the most updated version of our application. When this happens, we are likley to encounter a merge conflict.

Don't worry, often times these conflicts can have easy resolutions when you know how to fix them. For this example, we will be using GitHub to resolve a merge conflict. In the second example we will use GitBash.

### Step 1:

In your repository, click on the "Pull Requests" tab on the top of the page.

![Pull Requests Picture](https://docs.github.com/assets/cb-52309/mw-1440/images/help/repository/repo-tabs-pull-requests.webp)

### Step 2:

In the "Pull Requests" list, click the pull request with the merge conflict you'd like to fix.

### Step 3:

Near the bottom of the pull request, click "Resolve conflicts".

![Resolve conflict Picture](https://docs.github.com/assets/cb-69659/mw-1440/images/help/pull_requests/resolve-merge-conflicts-button.webp)

### Step 4:

Choose which version of the code you'd like to keep or make necessary changes to the code as needed. 

NOTE: Make sure that you delete the conflict markers `<<<<<<<`, `=======`, and `>>>>>>>`. 

Also, if you have more than one merge conflict, you can feel free to do this step for all of them until the conflict is resolved. 

### Step 5:

After you've fixed all of your merge conflicts, you can click on the "Commit merge" button to merge the branch into the main branch.

![Commit merge Picture](https://docs.github.com/assets/cb-198829/mw-1440/images/help/pull_requests/merge-conflict-commit-changes.webp)


# Steps to Resolve a Merge Conflict on GitBash:

Sometimes, the merge conflicts will be too complex to handle on GitHub, so you will need to do it through your local computer. Here is how to achieve that.

### Step 1:

In GitBash, go to the local Git repository that has the merge conflict by using this command:

`cd <Repository-Name>` 

Where you switch the `<Repository-Name>` with the name of the repository.

### Step 2:

Get a list of the files affected by the merge conflict by using the `git status` command.

### Step 3:

Open a text editor, such as VS Code, and go to the file with the merge conflict.

### Step 4:

Just like in GitHub, the beginning of the conflict will be marked by the `<<<<<<< MAIN`, the `=======` will show you where the main branch code ends and where the branch conflict starts, and the `>>>>>>>` will show you where the branch ends.

Figure out which part you'd like to keep or what further changes need to be made and make them. 

REMEMBER: You need to delete the `<<<<<<<`, `=======`, and `>>>>>>>` from your code before you commit the changes.

### Step 5:

Commit your changes as usual with the `git add` and `git commit -m "Write your message here"` commands. 