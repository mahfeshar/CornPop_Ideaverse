---
up:
  - "[[Py Module]]"
related: 
created: 2024-05-13
tags: 
Link: https://favtutor.com/blogs/uuid-python
---
- Generate random IDs
- When coders work with a certain database, it’s a standard procedure to employ a sort of unique ID field that can provide each row of a table, with a special kind of identifier.
- UUID stands for Universally Unique Identifier
- In Python, UUID is a 128
- character string of alphanumeric variable type, that uniquely identifies an object, entity, or resource in both space and time of a table
- UUID is an inbuilt module
- The module has a UUID class used to generate UUIDs of different versions: versions 1, 3, 4, and 5.
### How to generate UUID in Python?
1. Import the UUID module
2. Use one of the functions in the uuid module to generate a UUID.
3. The function uuid.uuid1() creates a UUID by utilizing the computer's MAC address and the current time.
4. Creates a random UUID using uuid.uuid4().
5. Creates a UUID based on a namespace and a name using the function uuid.uuid5(namespace, name).
6. Use the UUID which was created in the given module and print it out to see the output.

```python
import uuid
random_uuid = uuid.uuid4()
print(random_uuid)
```

### Example of UUID generation

Python's UUID module must first be imported before it can be used. Here's an illustration:

```python
import uuid

# generate a random UUID
random_uuid = uuid.uuid4()

# generate a UUID based on a namespace and a name
namespace = uuid.NAMESPACE_URL
name = 'https://example.com'
uuid_from_name = uuid.uuid5(namespace, name)

# print the UUIDs
print(random_uuid)
print(uuid_from_name)

**Output:**

9c773958-78b2-4b4a-bbee-1f0e70026cf9
4fd35a71-71ef-5a55-a9d9-aa75c889a6d0
```

Two UUIDs: one created at random and the other using the namespace and name provided—will be the generated output.

### Various functions of the UUID module

UUID1(): Here, the MAC address and current time component are used to create a unique number that identifies a field in the table uniquely. 
```python
import uuid

# Generate a UUID1
uuid1 = uuid.uuid1()

# Print the UUID1
print(uuid1)

**Output:**
5a91c607-c0e9-11ed-af63-8cc6818b4b8c
```

UUID3(): This UUID-based module generates a unique identifier based on a namespace and time. UUID 3 utilizes MD5 hashing.
```python
import uuid

# Generate a UUID3 for a namespace and name
namespace = uuid.uuid3(uuid.NAMESPACE_DNS, 'example.com')
uuid3 = uuid.uuid3(namespace, 'some string')

# Print the UUID3
print(uuid3)

**Output:**
387d0c39-f671-333b-b6ea-33585a0bb24e
```

UUID4(): For safety purposes, this kind of UUID is the wisest option. Here, a pseudo-random number generator is used and thus, a random UUID is used in the databases. 
```python
import uuid

# Generate a UUID4
uuid4 = uuid.uuid4()

# Print the UUID4
print(uuid4)

**Output:**
07d22f38-7561-464c-a461-0665f2da1a5b
```

UUID5(): To generate UUID, it employs cryptographic hashes and text strings supplied by the application. UUID 5 employs SHA-1 hashing. 
```python
import uuid

# Generate a UUID5 for a namespace and name
namespace = uuid.uuid5(uuid.NAMESPACE_DNS, 'example.com')
uuid5 = uuid.uuid5(namespace, 'some string')

# Print the UUID5
print(uuid5)

**Output:**
b1267b47-9e39-5ae8-92bd-668a30547a35
```
