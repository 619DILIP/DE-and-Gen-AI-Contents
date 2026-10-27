<br>

- Merging is Git's way of putting a forked history back together again. 
- The git merge command lets you take the independent lines of development created by git branch and integrate them into a single branch.
- Git merge will combine multiple sequences of commits into one unified history. 
  - In the most frequent use cases, git merge is used to combine two branches. 
  - Git merge takes two commit pointers, usually the branch tips, and will find a common base commit between them. 
  - Once Git finds a common base commit it will create a new "merge commit" that combines the changes of each queued merge commit sequence.
