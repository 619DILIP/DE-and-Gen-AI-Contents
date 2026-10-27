<details><summary>Implementation</summary> 

## Working with Binary Data in Python:

### Creating Binary Data:

#### Create a bytes object from a sequence of integers:

```python
binary_data = bytes([0b01000001, 0b01000010, 0b01000011])
```

* This code snippet creates a `bytes` object named binary_data containing binary values representing ASCII characters 'A', 'B', and 'C'.

#### Create a bytearray object from a binary string:

```python
binary_string = "01010100 01001001 01001110 01011000"
binary_bytes = bytearray([int(byte, 2) for byte in binary_string.split()])
```

* This code snippet converts a binary string into a `bytearray` object named binary_bytes, representing ASCII characters in binary form.

### Encoding and Decoding Binary Data:

#### Encoding binary data to a string:

```python
binary_data = bytes([0b01000001, 0b01000010, 0b01000011])
binary_str = binary_data.decode('utf-8')
```

* The `decode()` method converts binary data (bytes) into a string using the UTF-8 encoding.

#### Decoding a binary string to binary data:

```python
binary_string = "01010100 01001001 01001110 01011000"
binary_bytes = bytearray([int(byte, 2) for byte in binary_string.split()])
decoded_data = binary_bytes.decode('ascii')
```

* The `decode()` method converts a binary string to binary data (bytes) using the ASCII encoding.

### Manipulating Binary Data:

#### Extracting bits from binary data:

```python
binary_data = bytes([0b01010100, 0b01001001, 0b01001110, 0b01011000])
bit_mask = 0b00001111  # Mask to extract lower 4 bits
extracted_bits = bytes([byte & bit_mask for byte in binary_data])
```

* This code snippet extracts the lower 4 bits from each byte in binary_data using a bit mask.

#### Modifying binary data in-place:

```python
binary_data = bytearray([0b01010100, 0b01001001, 0b01001110, 0b01011000])
binary_data[1] = 0b01000001  # Modify the second byte
```

* The bytearray type allows modifying binary data in-place, providing flexibility for data manipulation.

</details>
