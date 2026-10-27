
<details><summary>Implementation</summary> 
<br>
The array method takes in two different parameters. One of which is the typecode  and the other is the initializer. 

Here's what the parameters in array(typecode, initializer) mean:

* typecode: This is a single character that specifies the type of data that will be stored in the array. For example:
  * 'i': Signed integer (4 bytes)
  * 'f': Floating point (4 bytes)
  * 'd': Double precision floating point (8 bytes)
  * 'b': Signed integer (1 byte)
  * 'u': Unicode character (2 bytes) 
  * 'l': Signed long integer (4 bytes) (platform-dependent)
* initializer: This is an optional parameter that initializes the array with elements. It can be a list, tuple, or any iterable containing the initial values for the array.


Note that the typecode selections listed above are only some of the more commonly used.


In the below example we will build an array.
```py
import array
arr = array.array('i', [1, 2, 3])
```
The above code example demonstrates how to create an array in Python. This particular example demonstrates how to create an array with the type of integer. It does this by unitizing the typecode ’i’ 
followed by the initializer which is the values that the array will hold. 

You can use the same format to create an array with any other type code. Just make sure that the values you pass into the array match the type specified by your typecode .

Creating Arrays:


```py
import array
numbers = array.array('i', [1, 2, 3, 4, 5])
```


* An array called numbers using the array() constructor from the array module that is being imported.
* The i inside the array() function call specifies the typecode or data type of the elements in the array. In this case, i stands for signed integer.


```py
import array
colors = array.array('u', "redgreenblue")
```


* An array called colors is created using the array() constructor from the array module that is being imported.
* Here, u represents a Unicode character which acts as the typecode for the array colors.

Accessing Elements:
```py
import array
fruits = array.array('u', "applebananacherry")
print(fruits[0])  # Output: 'a'
```

* An array called fruits is created using the array() constructor from the array module that is being imported.
* Typecode : u (Unicode character, 2 bytes).
* The print(fruits[0]) then prints the first element of the fruits array.



Slicing Arrays:
```py
import array
numbers = array.array('i', [1, 2, 3, 4, 5])
subset = numbers[1:4]
print(subset)  # Output: array('i', [2, 3, 4])
```


* An array called numbers is created using the array() constructor from the array module that is being imported.
* Typecode : i (Signed integer, 4 bytes)
* The line subset = numbers[1:4] creates a subset of the numbers array starting from index 1 (inclusive) up to index 4 (exclusive), which includes elements at indices 1, 2, and 3. So, subset becomes an array with elements [2,3,4].
* The line print(subset) then prints the contents of the subset array, which is [2,3,4].

Appending and Removing Elements:
```py
import array
numbers = array.array('i', [1, 2, 3])
numbers.append(4)  # Adds 4 to the end
numbers.remove(2)  # Removes the element 2
```


* An array named numbers is created using the array() constructor from the array module, which is being imported. This array has a typecode of i (representing Signed integer with 4 bytes) and initial elements [1, 2, 3].
* Then we use numbers.append(4) to add the integer 4 to the end of the numbers array, resulting in [1,2,3,4][1,2,3,4].
* Then, we use numbers.remove(2) to remove the element 2 from the numbers array. After this operation, the numbers array becomes [1,3,4] because the element 2 has been removed.

Iterating Through Arrays:
```
import array
fruits = array.array('u', "applebananacherry")
for fruit in fruits:
    print(fruit)
```


* An array named fruits is created using the array() constructor from the array module, which is being imported. This array has a typecode of u (representing Unicode Character with 2 bytes) and initial element “applebananacherry” .
* Then, a for loop is used to iterate over the fruits array, which prints each character in a separate line.

Array Operations:


Finding the length:
```
import array
numbers = array.array('i', [1, 2, 3, 4, 5])
length = len(numbers)
print(length)  # Output: 5
```
* An array named numbers is created using the array() constructor from the array module, which is being imported. This array has a typecode of i (representing Signed integer with 4 bytes) and initial elements [1, 2, 3, 4, 5].
* The result of len(numbers) (which is 5 in this case) is assigned to the variable length. This variable now holds the length of the numbers array.
* The len() function is applied to the numbers array to calculate its length. When len(numbers) is called, it returns the number of elements in the array, which in this case is 5.
* Finally, the code prints the value of the length variable using the print() function. This output confirms that the numbers array contains 5 elements.

Sorting:
```py
import array
numbers = array.array('i', [3, 1, 4, 1, 5, 9])
numbers_sorted = sorted(numbers)
print(numbers_sorted)  # Output: array('i', [1, 1, 3, 4, 5, 9])
```


* An array named numbers is created using the array() constructor from the array module, which is being imported. This array has a typecode of i (representing Signed integer with 4 bytes) and initial elements [3, 1, 4, 1, 5, 9].
* The sorted list returned by sorted(numbers) is assigned to the variable numbers_sorted. This variable now holds the sorted elements of the numbers array.
* The sorted() function is used to sort the elements of the numbers array in ascending order. This function returns a new list with the sorted elements.
* Finally, the code uses the print() function to display the sorted array numbers_sorted.


</details>
