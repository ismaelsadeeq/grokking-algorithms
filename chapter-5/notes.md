Hash Tables

* A Hash table is a data structure that uses a hash function to map keys to specific memory locations, allowing for efficient storage and retrieval of values associated with those keys.

* Collision:
A collision occurs in a hash table when two or more keys hashes to the same location or bucket. Since each bucket can only store one value, collisions need to be addressed to maintain the integrity of the data structure.

* Load Factor:
The load factor is a measure of how full the dictionary is. If it gets too high, Python automatically adjusts the size to maintain efficiency.

```python

# Load factor example
my_dict = {'apple': 3, 'banana': 5, 'orange': 2}
load_factor = len(my_dict) / len(my_dict.keys())
```

* The hash function:
A hash function is an algorithm that takes an input (in the case of a hash table, a key) and returns a fixed-size string of characters, which is typically a hash code. The goal is to spread the keys uniformly across the available buckets to minimize collisions. A good hash function produces different hash codes for different inputs, and small changes in input should result in a substantially different hash code.