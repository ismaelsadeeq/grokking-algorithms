Dynamic Programming

This is an art of solving a problem by breaking the problem down into sub problems;
solve the sub problems and then combine the solution.

Example of a problem that can be solved with dynamic programming is knapsack problem.

<b>Knapsack Problem:</b>
Given a set of items, each with a weight and a value, determine the maximum value that can be obtained by selecting a subset of the items such that the total weight does not exceed a given limit (knapsack capacity).

The solution with dynamic programming is below:
```python
class KnapSack:
    def __init__(self):
        # Initialize the knapsack with zero capacity and an empty set of items.
        self.capacity = 0
        self.items = {}

    # Method to update the knapsack capacity.
    def update_capacity(self, new_capacity):
        self.capacity = new_capacity

    # Method to add an item to the knapsack with a given name, value, and weight.
    def add_item(self, item_name, value, weight):
        self.items[item_name] = {'value': value, 'weight': weight}

    # Method to find the maximum value of items that can fit into the knapsack.
    def find_items_to_fit_in_knapsack(self):
        # Edge case: if the knapsack has zero capacity, the maximum value is zero.
        if self.capacity == 0:
            return 0, []

        # Initialize the grid representing the dynamic programming table.
        rows = len(self.items.keys())
        cols = self.capacity
        grid = [[{'value': 0, 'items': []}] * cols for _ in range(rows)]

        # Initialize the maximum value to track the optimal solution.
        max_value = -1
        max_value_items = []

        # Loop through all items in the knapsack.
        for i in range(rows):
            for j in range(cols):
                curr_item = list(self.items.keys())[i]
                current_item_weight = self.items[curr_item]['weight']
                current_item_value = self.items[curr_item]['value']

                # Base case: if this is the first item.
                if i == 0:
                    # If the item can fit in the current capacity, set the grid value.
                    if current_item_weight <= (j + 1):
                        grid[i][j] = {'value': current_item_value, 'items': [curr_item]}
                        max_value = current_item_value
                        max_value_items = [curr_item]

                    continue

                # Case when the current item weight exceeds the current capacity.
                if current_item_weight > (j + 1):
                    grid[i][j] = grid[i - 1][j]
                    continue

                # Check if there is space left, then fill it.
                current_items = [curr_item]
                if current_item_weight < (j + 1):
                    remaining_weight = (j + 1) - current_item_weight
                    current_item_value += grid[i - 1][remaining_weight - 1]['value']
                    current_items = current_items + grid[i - 1][remaining_weight - 1]['items']

                # Update the grid with the maximum value.
                if grid[i - 1][j]['value'] > current_item_value:
                    grid[i][j] = grid[i - 1][j]
                else:
                    grid[i][j] = {'value': current_item_value, 'items': current_items}

                # Update the maximum value if the current grid cell has a higher value.
                if grid[i][j]['value'] > max_value:
                    max_value = grid[i][j]['value']
                    max_value_items = grid[i][j]['items']

        # Print the dynamic programming table (grid) for visualization.
        # print(grid)
        return max_value, max_value_items


# Example usage:
k = KnapSack()
k.update_capacity(4)
k.add_item('item1', 1500, 1)
k.add_item('item2', 2000, 3)
k.add_item('item3', 3000, 4)
k.add_item('item4', 2000, 1)
k.add_item('item5', 1000, 1)

# Find the maximum value of items that can fit into the knapsack.
print(k.find_items_to_fit_in_knapsack())

```

Another application of dynamic programming is solving longest substring and longest subsequence in a string.

Given two string find the largest substring in them and also the subsequence

The strings "ABABC", "BABCA" and "ABCBA" have only one longest common substring, viz. "ABC" of length 3. Other common substrings are "A", "AB", "B", "BA", "BC" and "C".
https://en.wikipedia.org/wiki/Longest_common_substring


A longest common subsequence (LCS) is the longest subsequence common to all sequences in a set of sequences (often just two sequences). It differs from the longest common substring: unlike substrings, subsequences are not required to occupy consecutive positions within the original sequences.
https://en.wikipedia.org/wiki/Longest_common_subsequence


```python
def find_substring(a, b):
    """
    Find the length of the longest common substring between two strings.

    Args:
        a (str): The first string.
        b (str): The second string.

    Returns:
        int: The length of the longest common substring.
    """
    # Get the lengths of the input strings
    col = len(a)
    row = len(b)

    # Create a 2D array to store the lengths of common substrings
    arr = [[0] * col for _ in range(row)]

    # Initialize the maximum length to 0
    max_length = 0

    # Loop through each character in both strings
    for i in range(row):
        for j in range(col):
            # For the first row, set the value to 1 if characters match, 0 otherwise
            if i == 0:
                if b[i] == a[j]:
                    arr[i][j] = 1
                    max_length = max(arr[i][j], max_length)
                continue

            # If characters match, extend the length of the common substring
            if b[i] == a[j]:
                arr[i][j] = arr[i - 1][j - 1] + 1
                max_length = max(arr[i][j], max_length)

    # Print the 2D array for visualization
    print(arr)
    return max_length


def find_subsequence(a, b):
    """
    Find the length of the longest common subsequence between two strings.

    Args:
        a (str): The first string.
        b (str): The second string.

    Returns:
        int: The length of the longest common subsequence.
    """
    # Get the lengths of the input strings
    col = len(a)
    row = len(b)

    # Create a 2D array to store the lengths of common subsequences
    arr = [[0] * col for _ in range(row)]

    # Initialize the maximum length to 0
    max_length = 0

    # Loop through each character in both strings
    for i in range(row):
        for j in range(col):
            # For the first row, set the value to 1 if characters match, 0 otherwise
            if i == 0:
                arr[i][j] = 1 if b[i] == a[j] else 0
                max_length = max(arr[i][j], max_length)
                continue

            # If characters match, extend the length of the common subsequence
            if b[i] == a[j]:
                arr[i][j] = arr[i - 1][j - 1] + 1
            else:
                # If characters do not match, take the maximum length from the adjacent cells
                arr[i][j] = max(arr[i - 1][j], arr[i][j - 1])

            # Update the maximum length
            max_length = max(arr[i][j], max_length)

    # Print the 2D array for visualization
    print(arr)
    return max_length


# Example usage:
print(find_substring("fish", "hish"))
print(find_substring("fish", "hiah"))
print(find_substring("", "hhi"))

print(find_subsequence("fish", "fosh"))
print(find_subsequence("fort", "fosh"))

```