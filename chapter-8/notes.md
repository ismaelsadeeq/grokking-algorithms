Greedy algorithms

Greedy algorithms are algorithms that solve a problem in series of steps whereby 
in a each intermediate step it select the best possible optimal choice with the
overall goal of having an optimal result.

Example of greedy algorithm is solving a scheduling problem.
- Where you have a set of classes that happens from morning to noon, either simultaneously or not

ART - 9:00 - 10:00

ENG - 9:30 - 10:30

MATH - 10:30 - 11:00

CS - 10:30 - 11:30

MUSIC - 11:00 - 12:00

Your aim is to select classes to attend, you cant attend overlappig classes, and also cant attend classes that have begin without you.

A solution to this problem can be attained with a greedy algorithm

1. Select the class that ends the soonest
2. Pick the class the starts right after the first selected class, that also ends the soones.
3. Repeat 2 untill all classes are exhausted

When you apply this algorithm you will end up with 3 classes
Art starts at 09:00 and ends at 10:00

Math starts at 10:00 and ends at 11:00

Music starts at 11:00 and ends at 12:00

```python
class Course:
    def __init__(self, name, start_hour, start_mins, end_hour, end_mins):
        self.name = name
        self.start_hour = start_hour
        self.start_mins = start_mins
        self.end_hour = end_hour
        self.end_mins = end_mins

    # Implement < operator
    def __lt__(self, other):
        # Compare courses based on end time
        return (self.end_hour, self.end_mins) < (other.end_hour, other.end_mins)

    # Implement <= operator
    def next_fav(self, other):
        return (self.end_hour, self.end_mins) < (other.start_hour, other.start_mins) or (self.end_hour, self.end_mins) == (other.start_hour, other.start_mins)

    def get_course(self):
        return f"{self.name} starts at {self.start_hour:02d}:{self.start_mins:02d} and ends at {self.end_hour:02d}:{self.end_mins:02d}"

# Create a method that takes a list of classes
def select_classes(classes):
    # Handle edge case
    if len(classes) == 0:
        return []
    
    # Sort classes by end time
    classes = sorted(classes)

    # Select the first class
    selected_classes = [classes[0]]

    # While we have more classes
    for i in range(1, len(classes)):
        # Select the next class where start time >= current end time
        last_selected_class = selected_classes[len(selected_classes) - 1]
        candidate_class = classes[i]
    
        if  last_selected_class.next_fav(candidate_class):
            selected_classes.append(candidate_class)

    # Return selected classes
    return selected_classes

#Simple test
art = Course("Art", 9, 0, 10, 0)
eng = Course("ENG", 9, 30, 10, 30)
cs = Course("Math", 10, 0, 11, 0)
math = Course("CS", 10, 30, 11, 30)
music = Course("Music", 11, 0, 12, 0)

classes = [art, eng, math, cs, music]

classes_to_attend = select_classes(classes)
for current_class in classes_to_attend:
    print(current_class.get_course())

```

This scheduling algorithm has a time complexity of O(nlogn) and a spece complexity of O(n)


Knapsack Problem

This problem arises when you are given a set of items, each with an associated value and weight, Along with a knapsack with a limited weight capacity, the objective is to select items for the knapsack in a way that maximizes the total value, while adhering to the constraint of the knapsack's limited weight capacity.


You can apply a greedy algorithm by selecting high-value items and adding them to the knapsack. However, this does not guarantee an optimal solution, as the weight of a single high-value item might fill up the knapsack's weight capacity. Conversely, combining some mid-value items with small weights could lead to a more optimal solution.

Set covering problem

Suppose you have a set of items with elements in them, you want to get the minimum number of sets that combining them will give you all the elements in the set.

A more practical example:

Suppose you're starting a radio show and aim to reach listeners in all 50 states. You have a list of radio stations, each covering a specific region with some overlap. The goal is to decide on the smallest set of stations to play on to cover all 50 states, minimizing costs.

RADIO STATION AVAILABLE IN

KONE         | ID, NV, UT

KTWO         | WA, ID, MT

KTHREE       | OR, NV, CA

.....


List every possible subset of stations. This is called the power set. There are 2^n possible subsets. this is inefficient

A more efficient approach is to use a greedy Algorithm called Approximation Algorithm

Steps

1. Select the radio station that covers the most states that has not been covered
2. Repeat untill there are no more states left and retun the radio stations


Implementation

```python
class RadioShow:
    def __init__(self):
        self.radio_stations = {}
        self.states = set()

    def add_state(self, state):
        self.states.add(state)

    def add_station(self, station):
        if station not in self.radio_stations:
            self.radio_stations[station] = set()

    def add_state_to_station(self, station, state):
        if station not in self.radio_stations:
            self.radio_stations[station] = set()
        self.radio_stations[station].add(state)

    def select_station(self, selected_stations, selected_states):
        curr_station = None
        number_of_states = 0

        for station, states_in_station in self.radio_stations.items():

            if station not in selected_stations:
                states_not_covered = len(states_in_station - selected_states)
            
                if curr_station == None or states_not_covered > number_of_states:
                    curr_station = station
                    number_of_states = states_not_covered

        return curr_station

    def select_states(self):

        selected_states = set()
        selected_stations = set()

        while (len(selected_states) != len(self.states) and len(selected_stations) < len(self.radio_stations)):
            station = self.select_station(selected_stations, selected_states)
            if station is not None:
                selected_states.update(self.radio_stations[station])
                selected_stations.add(station)

        return selected_stations

states = ['Alabama', 'Alaska', 'Arizona', 'Arkansas', 'California', 'Colorado', 'Connecticut', 'Delaware',
          'Florida', 'Georgia', 'Hawaii', 'Idaho', 'Illinois', 'Indiana', 'Iowa', 'Kansas', 'Kentucky',
          'Louisiana', 'Maine', 'Maryland', 'Massachusetts', 'Michigan', 'Minnesota', 'Mississippi',
          'Missouri', 'Montana', 'Nebraska', 'Nevada', 'New Hampshire', 'New Jersey', 'New Mexico',
          'New York', 'North Carolina', 'North Dakota', 'Ohio', 'Oklahoma', 'Oregon', 'Pennsylvania',
          'Rhode Island', 'South Carolina', 'South Dakota', 'Tennessee', 'Texas', 'Utah', 'Vermont',
          'Virginia', 'Washington', 'West Virginia', 'Wisconsin', 'Wyoming']

stations = ['CoolWave FM', 'GroovyBeates Radio', 'Smooth Vibes FM', 'Nas FM', 'Hot FM']

radio_show = RadioShow()

for state in states:
    radio_show.add_state(state)

i = 0
for station in stations:
    total = i + 10
    while (i < total and i < len(states)):
        radio_show.add_state_to_station(station, states[i])
        i+=1
    i = i - 2

selected_stations = radio_show.select_states()

# Print the selected stations
print("Selected Radio Stations:")
for station in selected_stations:
    print(station)
```

N-P Complete Problems

These are problems whose optimal solution is computationally expensive as input data increases, problems whose optimal solutions run time complexities are exponential and factorial are basically N-P Complete problems.

We usually apply aproximation Algorithms AKA Greedy algorithm to solve those problems which gives us correct close to optimal solution.

Examples of such problems are the travelling sales person problem, set covering problem.


Solution of Traveling sales person using aproximation algorithm.

The problem

Given a list of cities and the distances between each pair of cities, what is the shortest possible route that visits each city exactly once and returns to the origin city

Solution

1. Start from any city as the current city.
2. While there are unvisited cities:

    * Select the unvisited city with the shortest distance from the current city.
    * Move to the selected city.
    * Mark the selected city as visited.

Return to the starting city to complete the tour.

Example 

City----Yola---Abuja---Lagos

Yola----0-----10-------15

Abuja--10-----0--------20

Lagos--15-----20-------0


Implementation

```python
# Define the Map class
class Map:
    def __init__(self):
        self.cities = {}

    def add_city(self, city):
        if city not in self.cities:
            self.cities[city] = {}

    def add_route(self, city, connecting_city, distance):
        if city not in self.cities:
            self.cities[city] = {}
        self.cities[city][connecting_city] = distance

    def find_distance(self):
        if not self.cities:
            return None

        # select the first city as the current city
        curr_city = next(iter(self.cities))

        # add it to the list of cities and initiate total km traveled
        cities_visited = [curr_city]
        distance_travelled = 0

        # while there are other cities to visit
        while any(city not in cities_visited for city in self.cities.keys()):
            routes = self.cities[curr_city]
            distance_to_city = float('inf')

            # select an unvisited city with the shortest distance to the current city as the next to visit
            for next_city, distance in routes.items():
                if next_city not in cities_visited and distance < distance_to_city:
                    chosen_city = next_city
                    distance_to_city = distance

            # add it to the list of cities
            cities_visited.append(chosen_city)
            # add the distance
            distance_travelled += distance_to_city
            curr_city = chosen_city

        # add the distance from the last city to the first city
        last_city = cities_visited[-1]
        first_city = cities_visited[0]
        if last_city in self.cities and first_city in self.cities[last_city]:
            distance_travelled += self.cities[last_city][first_city]

        # return the tuple of distance and list of cities used
        return cities_visited, distance_travelled

# Example Usage:
map_instance = Map()
map_instance.add_city("A")
map_instance.add_city("B")
map_instance.add_city("C")
map_instance.add_route("A", "B", 10)
map_instance.add_route("B", "C", 20)
map_instance.add_route("C", "A", 15)

result = map_instance.find_distance()
print(result)


```