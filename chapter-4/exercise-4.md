EXERCISES

4.1 Write out the code for the earlier sum function.

```python
def sum_of_arr(arr):
    if len(arr) == 0:
        return 0
    value = arr[0]
    arr.pop(0)
    return value + sum_of_arr(arr)
```
4.2 Write a recursive function to count the number of items in a list.

```python
def count_arr(arr):
    if len(arr) == 1:
        return 1
    arr.pop(0)
    return 1 + count_arr(arr)
```
4.3 Find the maximum number in a list.

```python
def count_arr(maximum_element, arr):
    if len(arr) == 0:
        return maximum_element
    if maximum_element < arr[0]:
        maximum_element = arr[0]
    arr.pop(0)
    return count_arr(maximum_element, arr)
```

4.4 Remember binary search from chapter 1? It’s a divide-and-conquer
algorithm, too. Can you come up with the base case and recursive
case for binary search?

```python
def binary_search(l, r, element, arr):
    if l > r:
        return - 1
    mid = int(l + (r - l) / 2)
    if arr[mid] == element:
        return mid
    if arr[mid] < element:
        l = mid + 1
    else:
        r = mid - 1
    return binary_search(l, r, element, arr)
```

How long would each of these operations take in Big O notation?

4.5 Printing the value of each element in an array.

O(n)

4.6 Doubling the value of each element in an array.

O(n)

4.7 Doubling the value of just the first element in an array.

O(1)

4.8 Creating a multiplication table with all the elements in the array. So
if your array is [2, 3, 7, 8, 10], you first multiply every element by 2,
then multiply every element by 3, then by 7, and so on.

O(n^2)