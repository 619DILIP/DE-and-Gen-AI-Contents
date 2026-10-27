
### Merge conflicts
It’s always nice when merges happened seamlessly, but on occasion, you could run into merge conflicts.

Merge conflicts happen when both branches you’re trying to merge change some part of the same file. Sometimes, Git is able to figure things out here.

However, Git often isn’t able to decide which version it should use if multiple people made changes to the same line in a file (or something similar), so it gives up right before creating the merge commit. That way, you can solve the problem.

### Solving merge conflicts
First, you need to understand what caused the merge conflict. Did someone delete a file you made changes to? Or maybe you added a file with the same name as an existing file.

Regardless, Git will inform you that you have “unmerged paths,” meaning conflicts stopped your branches from merging.

Fortunately, Git uses visual markers (<<<<<<<, =======, and >>>>>>>) to help you find the problem area easily.

The equal signs separate the two branches being merged. The branch below the equal signs is the branch you’re merging, whereas the branch above the equals signs is the receiving branch.

Once you find these conflicting sections, you can edit them until they work well. You may have to collaborate with the contributors/team members involved to make sure everything looks right.

After fixing the sections, it’s time to finish the merge. Execute git add on the conflicting file(s) to let Git know you’ve fixed everything. Then, execute a git commit command to create the merge commit and finish up.