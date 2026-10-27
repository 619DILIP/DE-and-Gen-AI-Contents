<details><summary>Learning Objectives</summary>
<br>

After completing this module, associates should be able to:

- Explain the following terms:
  - VCS
  - CVCS
  - DVCS
- Explain how Git implements Source Control Management (SCM)
</details>
<details><summary>Description</summary>
<br>

Version control, also known as revision control or source control management (SCM), is a process that manages a collection of source code and changes, providing you with many capabilities, such as:

- Maintaining multiple versions of code
- The ability to go back to any previous version
- Enabling developers to work in parallel
- Providing audit traceability with a clear picture of who made changes, what those changes were, when and where the changes occurred
- Synchronizing the code
- Copying, merging, or undoing changes
- Identifying differences between versions
- Providing full backup without occupying much space
- Reviewing the history of changes
- Being capable of both small and large-scale projects
- Allowing the sharing and collaborative work on code across the globe

In simpler terms, a version control system (VCS) allows you to manage and keep track of all your source code, ensuring that all your changes are stored in a repository.

### Importance of Version Control Systems
Let’s consider an example of an organization with a project team of five developers.

Two of them are in one location, and the other three are in a different location. They received a project and started developing the code, but they encountered the following situations while working on it:
- Each developer was working on one module at a time while others waited for them to complete their tasks so they could start working.
- Whenever they completed their work and decided to deploy the code, each took a full backup of the project. One day, they couldn’t do it because the disk was full.
- One day, one of them deleted a module, which they couldn’t recover, requiring them to rework on the same module.
- They were unable to identify who made specific changes and when those changes were made.
- They couldn’t experiment with new features without interfering with others' work.
- They needed to send code via email, as they were in different locations.

These situations underscore the need for a version control system, which can help avoid all the above issues while providing benefits to the development environment.
- A version control system ensures that all previous versions of your code can be retrieved and that all changes can be traced over time.
- It helps identify what changes were made to which file, when, why, and by whom.
- It also allows you to see what a file looked like on a specific date or at a specific release, while enabling the comparison of differences between any two versions of a file.
- A version control system provides the ability to work in parallel.

### Types of Version Control Systems
There are two types of version control systems: the centralized version control system (CVCS) and distributed version control system (DVCS).

### Centralized Version Control
A centralized version control system operates on a client-server relationship where the server is the repository and the clients are the developers. The source code is stored on a single, centralized server and clients contribute directly to this main repository. Additionally, file locking and branching can be used to prevent conflicts. 

### Distributed Version Control
With a distributed version control system, every user has a local copy of the repository. Users can make commits, create branches, and merge code in their local version of the code.

For example, a project on Github can be cloned on multiple developers' computers. Each developer has a complete copy of the source code and can make edits locally. These changes can be merged into the "main" repository (the one hosted on Github) following code reviews from peers/managers. 

</details>
<details><summary>Real World Application</summary>

### Benefits of Version Control Systems

- A version control system acts as a database for all your code, enabling revisions instead of duplicating files, which helps save significant disk space.
- It keeps the history of all files, providing full traceability and audibility of what changes were made to each file, when, why, and by whom.
- It allows you to revert to the last revision or any previous stage as needed.
- It mitigates the risk of losing functioning code or breaking test scripts by overwriting files, as you can always retrieve the last working code at any point.
- It helps you identify differences in any set of files, compare revisions, and merge changes as required.
- It enables you to maintain entirely independent code versions, if you wish to keep different development branches, with the ability to merge files into a final working version when ready.
- It facilitates distributed teamwork with full collaboration across the globe, saving time and effort for everyone, eliminating the need to wait for others to complete their work.
</details>
<details><summary>Summary</summary> 
<br>

- Version control, also known as revision control or source control management (SCM), is a process that manages a collection of source code and changes, providing you with many capabilities.
- A version control system (VCS) allows you to manage and keep track of all your source code, ensuring that all your changes are stored in a repository.
- There are two types of version control systems: the centralized version control system (CVCS) and the distributed version control system (DVCS).
  - The concept of CVCS operates on a client-server relationship, with the repository located in one place and providing access to many clients.
  - Conversely, in DVCS, every user has a local copy of the repository in addition to the central repository on the server side.
</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
