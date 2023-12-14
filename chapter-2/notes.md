Array

* An array is a data structure that stores a series of elements contiguously, one after the other, sequentially.

* You initialize an element in an array with values, or empty arrays, and the next memory locations after the array can be filled up with another data. So, whenever you want to add an element, if the next memory location is filled up, you have to move the whole array to some contiguous memory locations that will fit all the previous items in the array and the next item to be inserted.

* Some programming languages enable you to reserve the total space you assume your array data will fill throughout its lifetime, and you don't need to move the array during insertion. However, note that the reserved memory locations will be wasted if the memory locations are not utilized, the reserved memory locations will not be used by other aspect of the program, and If you get more elements than the reserved memory locations, you have to move the array anyway.


Insertion to an array is O(n)

Deletion is O(n)

Lookup is O(1)

Arrays are good when you know the exact size of its elements and you frequently need to lookup data item.


Linked List

* A linked list is a data structure that lets you store data items in random memory locations. The linked list points to the first item in the list, and each item contains the data and the memory location address of the next item in the list, forming a chain. This makes it easier to store items whose exact size is not known. Linked lists are good for insertions and deletions but not efficient in lookups, as you have to traverse the list from the beginning to get to an item and may go through up to the end in the worst case.
        
Insertion to a linked list is O(1)

Deletion is O(1) (To delete first and last / if you know the node of the mid item)

Lookup is O(n)

Linked lists are useful when handling data of uncertain size, and you constantly add and remove its elements.


Sorting

* Sorting is the process of arranging elements in a list in a specific order, such as ascending or descending numerical order.

Selection Sort

* This sorting algorithm involves traversing the list, selecting the smallest or largest element based on the objective, adding it to another array, and repeating the process for the next smallest or largest element until the entire list is exhausted.

Running time of selection sort is O(n^2)


```python
def find_smallest_index(arr):
    if len(arr) == 0:
        return -1
    smallest_index = 0
    for i in range(1, len(arr)):
        if arr[smallest_index] > arr[i]:
            smallest_index = i
    return smallest_index


def selection_sort(arr):
    if len(arr) <= 1:
        return arr

    sorted_arr = []
    while(len(arr) > 0):
        smallest_index = find_smallest_index(arr)
        sorted_arr.append(arr.pop(smallest_index))
    return sorted_arr

```



