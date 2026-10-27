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
Once Pylint is downloaded you can target your modules to perform static code analysis. The following module is the target of the example analysis
```python
for num in range(11):
 print(num)
```
```cli
pylint example.py
************* Module example
example.py:2:0: C0304: Final newline missing (missing-final-newline)
example.py:2:0: W0311: Bad indentation. Found 1 spaces, expected 4 (bad-indentation)
example.py:1:0: C0114: Missing module docstring (missing-module-docstring)
```
The linter tells you the following information
- what module the code smell was detected in
- the line of the code smell
- the category of the code smell
- what the code smell actually is

## Batch Analysis
If you want to target multiple modules in a directory you can target the directory and set "--recursive" equal to "y"
```cli
pylint --recursive=y my-directory
************* Module example
my-directory\example.py:2:0: C0304: Final newline missing (missing-final-newline)
my-directory\example.py:2:0: W0311: Bad indentation. Found 1 spaces, expected 4 (bad-indentation)
my-directory\example.py:1:0: C0114: Missing module docstring (missing-module-docstring)
************* Module example_two
my-directory\example_two.py:3:0: C0304: Final newline missing (missing-final-newline)
```