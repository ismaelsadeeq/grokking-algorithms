Divide and Conquer

* This is an algorithm that divides a problem into a subproblems until each subproblem is solvable, the subproblem should then be solved and combine all the subproblems solutions into a single problem solution.

Quick Sort

This is a sorting algorithm that uses divide and conquer to sort and item in a list.

```python

def q_sort(arr):
    if len(arr) < 2:
        return arr
    mid = int(len(arr) / 2)
    pivot = arr[mid]
    sub_arr_greater = []
    sub_arr_lesser = []
    for i in range(0, len(arr)):
        if i == mid:
            continue
        if arr[i] < pivot:
            sub_arr_lesser.append(arr[i])
        else:
            sub_arr_greater.append(arr[i])
    return q_sort(sub_arr_lesser) + [pivot] + q_sort(sub_arr_greater)

```

This quick sort algorithm has a runtime complexity of O(nlogn) in best and average case
Whereas in a worst case it has a complexity of O(n^2)

Space complexity is also O(n)

Partition Quicksort algorithm with O(n) space complexity

```python
def q_sort_p(arr, l, r):
    # Check the base case
    if l < r:
        # Get the partition
        p = partition(arr, l, r)
        # Sort the array on the left
        q_sort_p(arr, l, p - 1)
        # Sort the array on the right
        q_sort_p(arr, p + 1, r)

def partition(arr, l, r):
    # Get the pivot
    pivot = arr[r]
    # Declare i
    i = l - 1
    # Loop through the array to r
    for j in range(l, r):
        # If the element is less than the pivot
        if arr[j] < pivot:
            # Increase the previous
            i = i + 1
            # Swap the item with the previous
            (arr[j], arr[i]) = (arr[i], arr[j])
    # Swap the array with the item that is last less than + 1
    (arr[i + 1], arr[r]) = (arr[r], arr[i + 1])
    return i + 1

```

This algorithm above is better because it has a space complexity of O(n)

The only downside is this is not a stable sort