<details><summary>Learning Objectives</summary>
<br>

* Understand binary data and its representation in computer systems.
* Learn how to work with binary data in Python using the `bytes` and `bytearray` data types.
* Explore encoding and decoding of binary data using different character encodings.

</details>

<details><summary>Description</summary>
<br>

Binary data in computer systems refers to data that is represented using only two possible values, typically 0 and 1.

In Python, binary data can be handled using the `bytes` and `bytearray` data types, allowing manipulation and conversion of binary data.

## Introductory Concepts about Binary Data:

* Binary data represents information at the lowest level in a computer system, using binary digits (bits): 0 and 1.

* Binary data is commonly used for storing and transmitting data efficiently, especially for non-textual data like images, audio, and video.

* Python provides built-in data types `bytes` and `bytearray` for handling binary data.

### Key Characteristics of Binary Data Handling:

#### 1. `bytes`:

> An immutable sequence of bytes, often used for read-only binary data.

#### 2. `bytearray`:

> A mutable sequence of bytes, suitable for modifying binary data in place.

Encoding and decoding of binary data can be accomplished using different character encodings such as UTF-8, ASCII, and more.

Understanding how to work with binary data is essential for tasks involving file I/O, network communication, and low-level data manipulation in Python.

</details>

<details><summary>Real World Application</summary>

### Binary data handling in Python is commonly used for:

#### 1.  File I/O Operations:

> Reading and writing binary files, such as image, audio, and video files.

#### 2. Network Communication:

> Sending and receiving binary data over network protocols like TCP/IP, UDP, and HTTP.

#### 3. Data Encryption and Hashing:

> Encoding and decoding binary data for cryptographic operations like encryption, decryption, and hashing.

#### 4. Low-Level Data Processing:

> Manipulating binary data at a low level for tasks like parsing binary file formats and data structures.

Efficient handling of binary data is crucial for various applications, including data storage, communication, and security protocols.

</details>

<details><summary>Implementation</summary> 

## Working with Binary Data in Python:

### Creating Binary Data:

#### Create a `bytes` object from a sequence of integers:

```python
binary_data = bytes([0b01000001, 0b01000010, 0b01000011])
```

* This code snippet creates a `bytes` object named `binary_data` containing binary values representing ASCII characters 'A', 'B', and 'C'.

#### Create a `bytearray` object from a binary string:

```python
binary_string = "01010100 01001001 01001110 01011000"
binary_bytes = bytearray([int(byte, 2) for byte in binary_string.split()])
```

* This code snippet converts a binary string into a `bytearray` object named `binary_bytes`, representing ASCII characters in binary form.

### Encoding and Decoding Binary Data:

#### Encoding binary data to a string:

```python
binary_data = bytes([0b01000001, 0b01000010, 0b01000011])
binary_str = binary_data.decode('utf-8')
```

* The `decode()` method converts binary data (`bytes`) into a string using UTF-8 encoding.

#### Decoding a binary string to binary data:

```python
binary_string = "01010100 01001001 01001110 01011000"
binary_bytes = bytearray([int(byte, 2) for byte in binary_string.split()])
decoded_data = binary_bytes.decode('ascii')
```

* The `decode()` method converts a binary string to binary data (`bytes`) using ASCII encoding.

### Manipulating Binary Data:

#### Extracting bits from binary data:

```python
binary_data = bytes([0b01010100, 0b01001001, 0b01001110, 0b01011000])
bit_mask = 0b00001111  # Mask to extract lower 4 bits
extracted_bits = bytes([byte & bit_mask for byte in binary_data])
```

* This code snippet extracts the lower 4 bits from each byte in `binary_data` using a bit mask.

#### Modifying binary data in place:

```python
binary_data = bytearray([0b01010100, 0b01001001, 0b01001110, 0b01011000])
binary_data[1] = 0b01000001  # Modify the second byte
```

* The `bytearray` type allows modification of binary data in place, providing flexibility for data manipulation.

</details>

<details><summary>Summary</summary> 
<br>

* Binary data in Python is represented using the `bytes` and `bytearray` data types.

* `bytes` is immutable, while `bytearray` is mutable, allowing modification of binary data.

* Binary data can be encoded and decoded using different character encodings like UTF-8, ASCII, etc.

* Understanding how to work with binary data is essential for file I/O operations, network communication, and low-level data processing in Python.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
