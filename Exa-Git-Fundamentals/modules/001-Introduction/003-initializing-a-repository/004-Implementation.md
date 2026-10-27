
## Steps for Initializing a Repository

### How to Get a Git Repository

There are two ways of obtaining a Git repository:
- Turning an existing directory into a Git repository (initializing).
- Cloning a Git repository from an existing project.

### Initialize a Repository
To initialize a Git repository in an existing directory, start by using the Git Bash terminal window to go to your project's directory:

```bash
cd [directory path]
```

Where [directory path]: The path to your project directory.

### Use Git Bash to go to your project directory

Once you navigate to the project directory, initialize a Git repository by using:

```bash
git init
```

### Initializing a Git repository with git init

Initializing a repository creates a subdirectory called .git that contains the files Git needs to start tracking the changes made to the project files. The repository only starts tracking project versions once you commit changes in Git the first time.


### Clone a Repository

Use the git clone command to clone an existing repository and copy it to your system:

```bash
git clone [url] [directory]
```

Where:

[url]: The URL of the Git repository you want to clone.<br>
[directory]: The name of the directory you want to clone the repository into. Note: specifying the directory is optional; if not specified it will clone to the current directory.