# Ways to interact with files
there are two basic ways to interact with a file:
```python
# option one
my_file = open("to_open.txt", "r")

for line in my_file:
    print(line)

my_file.close()
```
```python
# option two
with open("to_open.txt", "r") as my_file:
    for line in my_file:
        print(line)
```
The key difference between the two is the second option will automatically close the file when your code is done


