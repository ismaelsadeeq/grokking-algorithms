Recursion

* A function that call itself, it hase a base case and recursive case.

* Call stack is how program functions are executed in memory, in a stack data structure.

```python
def countdown(i):
    print i
    if i <= 0: # Base case
        return
    else: # Recursive case
        countdown(i-1)                                                                          

```