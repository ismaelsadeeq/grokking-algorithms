<b>Classification Algorithm</b>

Classification algorithms are tools utilized to determine whether an object belongs to a specific category.

For instance, when presented with oranges and grapes, the algorithm classifies and identifies each item as either an orange or a grape based on distinct features such as size and color. It can be asserted that all oranges have sizes below a particular threshold and exhibit a certain percentage of darkness. Conversely, all grapes surpass this threshold in size and share a specified percentage of darkness.


Orange -> (Size < Threshold, Darkness < Percentage)


Grape -> (Size > Threshold, Darkness > Percentage)

But what about the objects that fall within these ranges? Those objects will be classified based on their nearest neighbors. The highest number of neighbors close to the objects will determine their object type. If the majority of neighbors are oranges, then the object is classified as an orange. Conversely, if the majority of neighbors are grapes, then the object is classified as a grape.

This algorithm is known as the Kth Nearest Neighbor Classification Algorithm.

Implementation of Kth Nearest Neighbor

```python

import math

# Sample dataset - feature vectors for oranges and grapes
data = {
    'oranges': [[5, 20], [6, 25], [7, 18], [4, 15]],
    'grapes': [[8, 30], [6, 22], [9, 28], [3, 12]]
}

# Function to calculate Euclidean distance between two points
def euclidean_distance(point1, point2):
    # Check if the points have the same number of dimensions
    if len(point1) != len(point2):
        raise ValueError("Points must have the same number of dimensions")
    
    # Calculate the sum of squared differences for each dimension
    squared_diff_sum = sum((point1[i] - point2[i]) ** 2 for i in range(len(point1)))
    
    # Return the square root of the sum as the Euclidean distance
    return math.sqrt(squared_diff_sum)

# Function to classify a new object using Kth Nearest Neighbor Classification Algorithm
def knn_classify(new_object, k=3):
    distances = []
    
    # Iterate through each category (oranges and grapes) in the dataset
    for label, points in data.items():
        # Calculate the Euclidean distance between the new object and each point in the category
        for point in points:
            distance = euclidean_distance(point, new_object)
            distances.append((label, distance))
    
    # Sort distances and get the k nearest neighbors
    neighbors = sorted(distances, key=lambda x: x[1])[:k]
    
    # Count the occurrences of each label among the neighbors
    label_counts = {'oranges': 0, 'grapes': 0}
    for neighbor in neighbors:
        label_counts[neighbor[0]] += 1
    
    # Classify the new object based on the majority label
    predicted_label = max(label_counts, key=label_counts.get)
    
    return predicted_label

# Test the  Kth Nearest Neighbor Classification Algorithm with a new object
new_object = [7, 22]  # Replace with your new object's features
predicted_class = knn_classify(new_object, k=3)
print(f"The new object is classified as: {predicted_class}")

```

<b>Recommendation Algorithms</b>

We can use  Kth Nearest Neighbor Classification Algorithm, to find the people that might have similar interest based on features, using  Kth Nearest Neighbor Classification Algorithm we can determine the nearest neighbors of a person and then. recommend similar stuffs to them.
E.g this can be used in movie streaming platform to recommend movies to a person beased on what they rate, commedy action e.t.c and then implement  Kth Nearest Neighbor Classification Algorithm to find their nearest neighbor, then whichever movies the nearest neigbor watches recommend to the person and vice versa.

| Category  | Alice | Bob | Charlie | David | Emma |
|-----------|-------|-----|---------|-------|------|
| Romance   | 3     | 4   | 5       | 2     | 1    |
| Comedy    | 5     | 2   | 4       | 2     | 1    |
| Action    | 2     | 3   | 4       | 1     | 5    |
| Fantasy   | 4     | 1   | 2       | 3     | 5    |
| Adventure | 1     | 4   | 3       | 2     | 5    |


In this to find who are closer to charlie

We use the euclidean distance formaular to find the distance between each person with charlie, and then see who are his nearest neighbors.

To find the nearest neighbors of Charlie using the k-Nearest Neighbors (KNN) algorithm, you can calculate the Euclidean distance between Charlie and each other person in the dataset. The formula for Euclidean distance between two points (x1,y1,…,n1) and (x2,y2,…,n2) is:

Euclidean Distance=sqrt((x1​−x2​)^2+(y1​−y2​)^2+…+(n1​−n2​)^2)


In this case, you can consider each category rating as a dimension, and Charlie's ratings as one point, and then calculate the distance to each other person's ratings..

Implementation

```python
import math

# Sample dataset
data = {
    'Alice': [3, 5, 2, 4, 1], 
    'Bob': [4, 2, 3, 1, 4],
    'Charlie': [5, 4, 4, 2, 3], 
    'David': [2, 2, 1, 3, 2],
    'Emmaa': [1, 1, 5, 5, 5]
}

def euclidean_distance(point1, point2):
    """
    Calculate the Euclidean distance between two points.

    Parameters:
    - point1 (list): List representing the feature vector of the first point.
    - point2 (list): List representing the feature vector of the second point.

    Returns:
    - float: Euclidean distance between the two points.
    """
    if len(point1) != len(point2):
        # Must be the same dimension
        return ValueError("points must be of the same dimension")
    
    sum_of_elements = sum((point1[i] - point2[i]) ** 2 for i in range(len(point1)))
    return math.sqrt(sum_of_elements)

def find_neighbors(person, num_of_neighbors=3):
    """
    Find the k-nearest neighbors of a given person based on Euclidean distance.

    Parameters:
    - person (str): The person for whom neighbors are to be found.
    - num_of_neighbors (int): Number of nearest neighbors to return. Default is 3.

    Returns:
    - list: List of tuples containing (neighbor_person, distance).
    """
    person_points = data[person]
    distances = []
    
    for curr_person in data.keys():
        if curr_person == person:
            continue
        distance = (curr_person, euclidean_distance(person_points, data[curr_person]))
        distances.append(distance)
    
    # Sort distances and get the nearest_neighbors
    sorted_distances = sorted(distances, key=lambda x: x[1])[:num_of_neighbors]
    return sorted_distances

# Example usage
print(find_neighbors('Charlie'))


```

<b>Regression</b>

Regression is a well-known method for predicting how a person is likely to behave, such as rating a movie. It involves classifying a person by determining their nearest neighbors and taking the average ratings of those neighbors as the person's likely rating. For example, if Alice, Bob, Jude, and Abbati are the nearest neighbors of Charlie, and their ratings for a category of a movie are (5, 4, 4, 5), the likely rating that Charlie will give to the movies in that category is calculated as (5 + 4 + 4 + 5) / 4 = 4.5.

Implementation

```python
import math

# Sample data with features and corresponding values
"""
The data below represent a small bakery sales and the conditions of the date when
those sales heppen, the total sales of the bread.

'1-01-2024': [[5, 1, 0], 300]

1-01-2024 ---> Sales date

• Weather on a scale of 1 to 5 (1 = bad, 5 = great).
• Weekend or holiday? (1 if it’s a weekend or a holiday, 0 otherwise.)
• Is there a game on? (1 if yes, 0 if no.)

[5, 1, 0] -> 5 for weather, 1 for weekend, 0 no game that day

300 -> The store made 300 sales on the date 
"""
data = {
    '1-01-2024': [[5, 1, 0], 300],
    '2-01-2024': [[3, 1, 1], 225],
    '3-01-2024': [[1, 1, 0], 75],
    '4-01-2024': [[4, 0, 1], 200],
    '5-01-2024': [[4, 0, 0], 150],
    '6-01-2024': [[2, 0, 0], 50]
}

def euclidean_distance(point1, point2):
    """
    Calculate the Euclidean distance between two points.

    Parameters:
    - point1 (list): List representing the feature vector of the first point.
    - point2 (list): List representing the feature vector of the second point.

    Returns:
    - float: Euclidean distance between the two points.
    """
    if len(point1) != len(point2):
        # Must be the same dimension
        raise ValueError("Points must be of the same dimension")
    
    # Calculate Euclidean distance
    sum_of_elements = sum((point1[i] - point2[i]) ** 2 for i in range(len(point1)))
    return math.sqrt(sum_of_elements)

def regression(current_day, k=4):
    # Calculate distances between the current day and all other days
    distances = [(day, euclidean_distance(current_day, data[day][0]), data[day][1]) for day in data.keys()]

    # Sort distances and select the closest k days
    sorted_distances = sorted(distances, key=lambda x: x[1])[:k]

    # Print sorted distances for inspection
    print(sorted_distances)

    # Calculate the regression value based on the closest k days
    return sum(sorted_distances[i][2] for i in range(len(sorted_distances))) / k

# Example: Calculate regression for today's data point
today = [3, 0, 1]  # Replace with actual feature vector for today
result = regression(today)
print(result)

```


Choosing good features is crucial in Kth Nearest Neighbor classification algorithms. It's essential to select features that truly matter for effective classification. Another approach to normalization involves using Cosine Similarities instead of Euclidean distance to measure the distance between feature vectors.


<b>Introduction to Machine Learning</b>

The Kth Nearest Neighbor Classification, Recommendation, and Regression Algorithm serves as an exemplary illustration of a machine learning algorithm. Machine learning, a branch of computing, empowers computers to acquire intelligence and learn from provided datasets.

Optical Character Recognition

The recognition of text from a given image can be achieved using the Kth Nearest Neighbor Classification Algorithm algorithm, employing numerous images of characters to determine their distinct features.

# 7  
The image featuring (1 vertical line, 1 horizontal line) represents the numeral seven.
# 3
The image displaying (2 curves, 1 point) signifies the numeral three.
get lots of this images and determine their features and the label.

By accumulating a multitude of such images and discerning their features along with corresponding labels, we engage in the process known as feature extraction or data training. This process allows for the extraction of image features and facilitates the application of the Kth Nearest Neighbor Classification Algorithm. By running the algorithm on a given image and the remaining dataset, identifying neighbors, and determining the majority label among neighbors, we ascertain the character represented by the image.

It's essential to note that feature extraction is more intricate than outlined here. This concept extends to applications such as speech and face recognition.

Spam Filters

Another application of machine learning involves utilizing the Naive Bayes classifier to construct a spam filter. Through training datasets of email titles and content using Naive Bayes, the classifier can effectively determine whether a new email is likely to be spam or not.




