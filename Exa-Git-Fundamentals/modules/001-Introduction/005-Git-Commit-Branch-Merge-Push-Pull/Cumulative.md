<details><summary>Learning Objectives</summary>

<br>

After completing this module, associates should be able to:

  - Perform the following in Git:
  - Commit changes
  - Merge changes
  - Push to a Git repository
  - Pull from a Git repository
</details>
<details><summary>Description</summary>

### Git Merge

Merging is Git's way of putting a forked history back together again. The `git merge` command lets you take the independent lines of development created by `git branch` and integrate them into a single branch.

Note that all of the commands presented below merge into the current branch. The current branch will be updated to reflect the merge, but the target branch will remain completely unaffected. This means that `git merge` is often used in conjunction with `git checkout` for selecting the current branch and `git branch -d` for deleting the obsolete target branch.

### How it works
`git merge` will combine multiple sequences of commits into one unified history. In the most frequent use cases, `git merge` is used to combine two branches. The following examples in this document will focus on this branch merging pattern. In these scenarios, `git merge` takes two commit pointers, usually the branch tips, and finds a common base commit between them. Once Git finds a common base commit, it will create a new "merge commit" that combines the changes of each queued merge commit sequence.

### New merge commit node
Merge commits are unique compared to other commits in that they have two parent commits. When creating a merge commit, Git will attempt to automatically merge the separate histories for you. If Git encounters a piece of data that is changed in both histories, it will be unable to automatically combine them. This scenario is a version control conflict, and Git will need user intervention to continue.

### Preparing to merge
Before performing a merge, there are a couple of preparation steps to ensure the merge goes smoothly.
- Confirm the receiving branch:
  - Execute `git status` to ensure that you are pointing to the correct merge-receiving branch. 
  - If needed, execute `git checkout` to switch to the receiving branch. In our case, we will execute `git checkout main`.
- Fetch the latest remote commits:
  - Make sure the receiving branch and the merging branch are up to date with the latest remote changes. 
  - Execute `git fetch` to pull the latest remote commits. 
  - Once the fetch is completed, ensure the main branch has the latest updates by executing `git pull`.

### Merging
Once the previously discussed "preparing to merge" steps have been taken, a merge can be initiated by executing `git merge`. 
</details>
<details><summary>Real World Application</summary>

### Merge conflicts
It’s always nice when merges happen seamlessly, but on occasion, you could run into merge conflicts.

Merge conflicts happen when both branches you’re trying to merge change some part of the same file. Sometimes, Git is able to figure things out.

However, Git often isn’t able to decide which version it should use if multiple people made changes to the same line in a file (or something similar), so it gives up right before creating the merge commit. That way, you can solve the problem.

### Solving merge conflicts
First, you need to understand what caused the merge conflict. Did someone delete a file you made changes to? Or maybe you added a file with the same name as an existing file?

Regardless, Git will inform you that you have “unmerged paths,” meaning conflicts stopped your branches from merging.

Fortunately, Git uses visual markers (`<<<<<<<`, `=======`, and `>>>>>>>`) to help you find the problem area easily.

The equal signs separate the two branches being merged. The branch below the equal signs is the branch you’re merging, whereas the branch above the equal signs is the receiving branch.

Once you find these conflicting sections, you can edit them until they work well. You may have to collaborate with the contributors or team members involved to make sure everything looks right.

After fixing the sections, it’s time to finish the merge. Execute `git add` on the conflicting file(s) to let Git know you’ve fixed everything. Then, execute the `git commit` command to create the merge commit and finish up.
</details>
<details><summary>Implementation</summary> 

<br>

This video goes through the steps involved in merging branches in Git:
[Merging branches in Git](https://www.youtube.com/watch?v=XX-Kct0PfFc)

# Steps to Resolve a Merge Conflict on GitHub:

Sometimes, when working on a project, we make multiple pushes to the remote repository without first pulling the most updated version of our application. When this happens, we are likely to encounter a merge conflict.

Don't worry; often, these conflicts can have easy resolutions when you know how to fix them. For this example, we will be using GitHub to resolve a merge conflict. In the second example, we will use GitBash.

### Step 1:

In your repository, click on the "Pull Requests" tab at the top of the page.

![Pull Requests Picture](https://docs.github.com/assets/cb-52309/mw-1440/images/help/repository/repo-tabs-pull-requests.webp)

### Step 2:

In the "Pull Requests" list, click the pull request with the merge conflict you'd like to fix.

### Step 3:

Near the bottom of the pull request, click "Resolve conflicts."

![Resolve conflict Picture](https://docs.github.com/assets/cb-69659/mw-1440/images/help/pull_requests/resolve-merge-conflicts-button.webp)

### Step 4:

Choose which version of the code you'd like to keep or make necessary changes to the code as needed. 

NOTE: Make sure that you delete the conflict markers `<<<<<<<`, `=======`, and `>>>>>>>`. 

Also, if you have more than one merge conflict, you can feel free to do this step for all of them until the conflict is resolved. 

### Step 5:

After you've fixed all of your merge conflicts, you can click on the "Commit merge" button to merge the branch into the main branch.

![Commit merge Picture](https://docs.github.com/assets/cb-198829/mw-1440/images/help/pull_requests/merge-conflict-commit-changes.webp)

# Steps to Resolve a Merge Conflict on GitBash:

Sometimes, the merge conflicts will be too complex to handle on GitHub, so you will need to resolve them through your local computer. Here is how to achieve that.

### Step 1:

In GitBash, go to the local Git repository that has the merge conflict by using this command:

`cd <Repository-Name>` 

Where you should replace `<Repository-Name>` with the name of the repository.

### Step 2:

Get a list of the files affected by the merge conflict by using the `git status` command.

### Step 3:

Open a text editor, such as VS Code, and go to the file with the merge conflict.

### Step 4:

Just like in GitHub, the beginning of the conflict will be marked by `<<<<<<< MAIN`, `=======` will show you where the main branch code ends and where the branch conflict starts, and `>>>>>>>` will show you where the branch ends.

Figure out which part you'd like to keep or what further changes need to be made, and make those changes. 

REMEMBER: You need to delete the `<<<<<<<`, `=======`, and `>>>>>>>` from your code before you commit the changes.

### Step 5:

Commit your changes as usual with the `git add` and `git commit -m "Write your message here"` commands. 
</details>
<details><summary>Summary</summary> 

<br>

- Merging is Git's way of putting a forked history back together again. 
- The `git merge` command lets you take the independent lines of development created by `git branch` and integrate them into a single branch.
- `git merge` will combine multiple sequences of commits into one unified history. 
  - In the most frequent use cases, `git merge` is used to combine two branches. 
  - `git merge` takes two commit pointers, usually the branch tips, and finds a common base commit between them. 
  - Once Git finds a common base commit, it will create a new "merge commit" that combines the changes of each queued merge commit sequence.
</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
