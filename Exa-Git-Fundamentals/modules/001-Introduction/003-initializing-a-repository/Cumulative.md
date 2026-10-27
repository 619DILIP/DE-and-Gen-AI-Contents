<details><summary>Learning Objectives</summary>
<br>

After completing this module, associates should be able to:

- Explain how to initialize a repository in Git.
- Use Git to create a new repository and/or clone an existing repository.

</details>
<details><summary>Description</summary>

### What is a Git Repository?

A Git repository tracks and saves the history of all changes made to the files in a Git project. It saves this data in a directory called `.git`, also known as the repository folder.

Git uses a version control system to track all changes made to the project and save them in the repository. Users can then delete or copy existing repositories or create new ones for ongoing projects.

</details>
<details><summary>Real World Application</summary>
<br>

Here are some reasons for using a Git repository:

- __Cloud repositories__
  - It is generally more secure. 
  - It is easier to work collaboratively. Any team member can download the latest version of the repository from any machine. 
  - It is cheaper than a traditional server.
- __Distributed file system__
  - Git is distributed, meaning that every local copy of the global repository is a fully working copy. 
  - In case there is a problem with the server and the global repository is corrupted or lost, any local copy can recreate the full history.
  - In a centralized version control system, the global server contains all changes in the project, and the local copies are just light versions of it. If the server goes down, you lose all the history.
- __Perfect for working with others__
  - Git is designed for creating projects where many contributors develop software in parallel. 
- __Good documentation__
  - Git has been around for many years, and it's really easy to find good documentation.
- __Branches allow for simultaneous code versions__
  - Branches are one of the best features of version control software and are used to develop in parallel to the main repository. 
  - A branch is a fork of the main code used to develop a new feature. 
- __Encourages code reviews__
  - Code reviews are a good practice that every developer team should follow. 
  - Git facilitates code reviews with an operation called a pull request.
- __Simpler to roll back mistakes__
  - Every commit is referenced with a hash that uniquely identifies it; see this example. 
  - With Git, we can revert to any past commit and fix a mistake.
- __It's the current de facto open-source umbrella__
    - If you want to develop open-source code, the biggest repository is GitHub. 
    - Here you can find the most popular repositories on GitHub; it includes Bootstrap, React, D3, TensorFlow, Angular, etc.

</details>
<details><summary>Implementation</summary> 

## Steps for Initializing a Repository

### How to Get a Git Repository

There are two ways to obtain a Git repository:
- Turning an existing directory into a Git repository (initializing).
- Cloning a Git repository from an existing project.

### Initialize a Repository
To initialize a Git repository in an existing directory, start by using the Git Bash terminal window to go to your project's directory:

```bash
cd [directory path]
```

Where `[directory path]` is the path to your project directory.

### Use Git Bash to go to your project directory

Once you navigate to the project directory, initialize a Git repository by using:

```bash
git init
```

### Initializing a Git repository with `git init`

Initializing a repository creates a subdirectory called `.git` that contains the files Git needs to start tracking the changes made to the project files. The repository only starts tracking project versions once you commit changes in Git for the first time.

### Clone a Repository

Use the `git clone` command to clone an existing repository and copy it to your system:

```bash
git clone [url] [directory]
```

Where:

`[url]`: The URL of the Git repository you want to clone.<br>
`[directory]`: The name of the directory you want to clone the repository into. Note: specifying the directory is optional; if it is not specified, it will clone to the current directory.

</details>
<details><summary>Summary</summary> 
<br>

- A Git repository tracks and saves the history of all changes made to the files in a Git project. 
- It saves this data in a directory called `.git`, also known as the repository folder.
- Git uses a version control system to track all changes made to the project and save them in the repository. Users can then delete or copy existing repositories or create new ones for ongoing projects.

</details>
<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)</details>
