## Implementation

- For this implementation, let's say we have a input file named as "input_file.txt" which has some text data. And now, we are interested in finding the frequency of each word of that input_file.txt file.

- For this, we will be make a main program which will read our input file and then this file is sent to the mapper function where each word is tokenized and stored in key-value format where the key will be the word itself and the value for each word will be assigned to 1. Then, the output of mapper function will be sent to combiner function, which will then work as a reducer and combine all the same words in a same key and updates its count. 

- For this mapper-combiner program, we use python language. 

**Map-Combine Program in Python** 

```python
import sys

def combiner(token):
    dict1 = {}
    value = 1
    for key in token:
        if key in dict1:
            value = dict1[key]
            dict1[key] = value + 1
        else:
            dict1[key] = 1
    
    return dict1


def mapper(data):
    token = [] 
    for word in data.split():
        token.append(word)
    
    return token


file = open("input_file.txt", "r")
read = file.read()
word = mapper(read)
word_combine = combiner(word)

output_file= open("file.txt", "w")
output_file.write(str(word_combine))

print("file written successfully")
sys.exit(1)

```
- Here, the output returned by the combiner function gets stored in the output file as "file.txt". 

---

