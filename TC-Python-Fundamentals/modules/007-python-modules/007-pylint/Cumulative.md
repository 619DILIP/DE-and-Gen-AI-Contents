# Cumulative for the pylint

<details><summary>Learning Objectives</summary>

# Learning Objectives
After completing this module, associates should be able to:
- Explain what Pylint is
- Explain the basics of static code analysis
- Perform static code analysis on their code using Pylint


</details>

<details><summary>Description</summary>

# Introduction 
When writing code, it can be easy to forget or miss small things such as naming conventions, language best practices, or even poorly written code. Static code analysis is the process of having software look for these "code smells," non-programmatic problems with our code, and reporting them to us. Pylint is a third-party package you can download to your project that can perform this analysis for you.

Keep in mind that most IDEs will have some dedicated linter or provide the option for installing one to analyze your code as you write it. Pylint is a tool that can be used alongside these other linters. With that being said, Pylint does support implementing plugins to customize the way it analyzes your code, which can turn it into a powerful tool for maintaining high-quality coding standards.

</details>
<details><summary>Real World Application</summary>

# Real World Application for Pylint
Most organizations are going to have some form of coding standard they expect their employees to adhere to, even if it is just the standard conventions of the language. When these standards are followed, it becomes significantly easier to review, maintain, and fix code bases. The shared understanding of how code should be written also provides common ground for developers when they need to collaborate. You don't have to spend time deciding how to name variables, how to structure your source code, or how to save the work. You simply let the standards dictated by your organization/language do that for you.

</details>
<details><summary>Implementation</summary> 

# Implementation

## Install
Pylint is stored in the PyPI repository, so you can install it using pip
```cli
pip install pylint
```
You can confirm it is ready for use by checking its version
```cli
pylint --version
```

## Perform Static Code Analysis
Once Pylint is downloaded, you can target your modules to perform static code analysis. The following module is the target of the example analysis
```python
for num in range(11):
    print(num)
```
```cli
pylint example.py
************* Module example
example.py:2:0: C0304: Final newline missing (missing-final-newline)
example.py:2:0: W0311: Bad indentation. Found one space, expected 4 (bad-indentation)
example.py:1:0: C0114: Missing module docstring (missing-module-docstring)
```
The linter tells you the following information:
- What module the code smell occurred in
- The line of the code smell
- The category of the code smell
- What the code smell actually is

## Batch Analysis
If you want to target multiple modules in a directory, you can target the directory and set '--recursive' equal to 'y'
```cli
pylint --recursive=y my-directory
************* Module example
my-directory/example.py:2:0: C0304: Final newline missing (missing-final-newline)
my-directory/example.py:2:0: W0311: Bad indentation. Found one space, expected 4 (bad-indentation)
my-directory/example.py:1:0: C0114: Missing module docstring (missing-module-docstring)
************* Module example_two
my-directory/example_two.py:3:0: C0304: Final newline missing (missing-final-newline)
```

</details>
<details><summary>Summary</summary> 

# Summary 

- Pylint is a static code analysis tool
- Pylint can analyze individual modules or entire directories
- Pylint supports customization to better suit your analysis needs
