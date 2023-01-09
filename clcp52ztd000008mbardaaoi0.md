# Python Cheatsheet

## List

Lists are ordered collections of items that can be of any data type and can be changed (mutable).

```python
# Initialize a list
numbers = [1, 2, 3, 4]

# Access an element by index
print(numbers[0])

# Append an element to the end of the list
numbers.append(5)

# Insert an element at a specific position
numbers.insert(0, 0)

# Remove an element by value
numbers.remove(4)

# Remove an element by index
del numbers[2]

# Get the length of the list
length = len(numbers)

# Sort the list
numbers.sort()

# Reverse the list
numbers.reverse()

# Loop through the list
for number in numbers:
    print(number)
```

## Tuples

Tuples are ordered collections of items that can be of any data type and cannot be changed (immutable).

```python
# Initialize a tuple
numbers = (1, 2, 3, 4)

# Access an element by index
print(numbers[0])

# Get the length of the tuple
length = len(numbers)

# Loop through the tuple
for number in numbers:
    print(number)
```

## Dictionary

Dictionaries are unordered collections of key-value pairs that can be of any data type and can be changed (mutable).

```python
# Initialize a dictionary
d = {'a': 1, 'b': 2, 'c': 3}

# Access a value by key
print(d['a'])

# Set a value for a key
d['d'] = 4

# Delete a key-value pair
del d['b']

# Get the keys
keys = d.keys()

# Get the values
values = d.values()

# Get the items (key-value pairs)
items = d.items()

# Check if a key exists
if 'a' in d:
    print('Key exists')

# Loop through the keys
for key in d:
    print(key)

# Loop through the values
for value in d.values():
    print(value)

# Loop through the items
for key, value in d.items():
    print(key, value)
```

## Set

Sets are unordered collections of unique items that can be of any data type and can be changed (mutable).

```python
# Initialize a set
s = {1, 2, 3, 4}

# Add an element to the set
s.add(5)

# Remove an element from the set
s.remove(4)

# Check if an element is in the set
if 3 in s:
    print('Element exists')

# Get the length of the set
length = len(s)

# Loop through the set
for element in s:
    print(element)
```

## File operations

```python
# Open a file in read mode
with open('file.txt', 'r') as f:
    # Read the contents of the file
    contents = f.read()
    print(contents)

# Open a file in write mode
with open('file.txt', 'w') as f:
    # Write some text to the file
    f.write('Hello, World!')
```

## JSON operations

```python
import json

# Define a JSON string
json_string = '{"name": "John", "age": 30, "city": "New York"}'

# Parse the JSON string
data = json.loads(json_string)

# Print the parsed data
print(data)

# Convert the object to JSON
json_string_again = json.dumps(data)

# Print the JSON data
print(json_string_again)
```

## HTTP request

GET API call:

```python
import requests

# Send a GET request
response = requests.get('https://www.example.com')

# Print the status code
print(response.status_code)

# Print the content of the response
print(response.content)
```

POST API call:

```python
import requests

# Set the URL and the payload (data to be sent)
url = 'https://www.example.com/api/create'
data = {'name': 'John', 'age': 30}
headers = {'Content-Type': 'application/json'}

# Send the POST request
response = requests.post(url, json=data, headers=headers)

# Print the status code
print(response.status_code)

# Print the response content
print(response.content)
```