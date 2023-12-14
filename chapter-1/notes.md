### Chapter 1 Notes

Binary Search

* To determine the number of steps required for executing a binary search on a set of elements, utilize the logarithm base 2 of the total number of elements. Logarithm base 2, denoted as log2, operates as the inverse of exponential functions. For instance, log2(64) equals 6, and multiplying 2 by itself six times results in 64, i.e., 2 * 2 * 2 * 2 * 2 * 2.

* Binary search significantly reduces the steps necessary to locate an element within a sorted list. In a conventional linear search, a total of n steps, in the worst-case scenario, is needed to search for an element. However, with binary search, only log2(n) steps are required, where n represents the total number of elements.

* Note: Binary search is applicable only to sorted elements. In cases where elements are unsorted, a linear search should be employed.


```python
def search(numbers, value):
    left = 0
    right = len(numbers) - 1
    while left <= right:
        # To avoid integer overflow
        mid = int(left + (right - left) / 2)
        if numbers[mid] == value:
            return mid
        if numbers[mid] < value:
            left = mid + 1
        else:
            right = mid - 1
    return - 1
```

Algorithm

* This is the sequence of steps needed to execute an instruction on a given input data.

Running Time of an algorithm

* The running time of an algorithm is measured by the number of basic operations it performs relative to the size of the input, not by the actual seconds it takes to execute on specific data

* Instead of looking at the time an algorithm takes in seconds, we focus on how many basic operations it does based on the size of the problem it's solving. This helps us compare and understand how well algorithms work, no matter the specific computer hardware they're running on.

* Linear Steps:
If an algorithm has linear steps, it means it goes through each piece of data one by one, especially in the worst-case scenario.

* Logarithmic Steps:
For logarithmic steps, think of the algorithm's efficiency growing like a logarithm (log2) as the amount of data (n) increases.

* Apart from linear and logarithmic, there are different ways to describe how fast algorithms are, like exponential or factorial times.

Big O Notation

* Big O notation is the method we use to calculate the running time of an algorithm.
We determine the speed and efficiency of an algorithm by examining its Big O in relation to 'n,' where 'n' is considered the total input data.

For instance, when an algorithm is linear, we state its running time as O(n), signifying that it takes 'n' steps to execute that algorithm in the worst case. Similarly, when the algorithm is logarithmic, we represent it as O(log(n)), indicating that it takes log(n) steps to complete the algorithm in the worst case.


