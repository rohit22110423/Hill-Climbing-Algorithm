# Hill-Climbing-Algorithm
#Hill Climbing Algorithm in AI
import random
graph = {
    'A': {'B': 2, 'C': 4, 'D': 1},
    'B': {'A': 2, 'C': 3, 'E': 2},
    'C': {'A': 4, 'B': 3, 'D': 2, 'E': 5},
    'D': {'A': 1, 'C': 2, 'E': 3, 'F': 6},
    'E': {'B': 2, 'C': 5, 'D': 3, 'F': 2, 'G': 1},
    'F': {'D': 6, 'E': 2, 'G': 3, 'H': 4},
    'G': {'E': 1, 'F': 3, 'I': 2},
    'H': {'F': 4, 'I': 3, 'J': 5},
    'I': {'G': 2, 'H': 3, 'J': 1},
    'J': {'H': 5, 'I': 1}
}
start_node = 'A'
goal_node = 'J'

def hill_climbing(start, goal):
    current_node = start
    current_path = [current_node]
    current_cost = 0

    while current_node != goal:
        neighbors = list(graph[current_node].keys())
        random.shuffle(neighbors)  # Shuffle neighbors to introduce randomness
        found_better_path = False
        min_cost = float('inf')
        min_neighbor = None

        for neighbor in neighbors:
            if neighbor not in current_path:
                new_cost = current_cost + graph[current_node][neighbor]
                if new_cost < min_cost:
                    min_cost = new_cost
                    min_neighbor = neighbor

        if min_neighbor is not None:
            current_path.append(min_neighbor)
            current_cost = min_cost
            current_node = min_neighbor
            found_better_path = True
        else:
            if len(current_path) > 1:
                current_path.pop()
                current_node = current_path[-1]
            else:
                print("No path found.")
                return None

    return current_path, current_cost

path, cost = hill_climbing(start_node, goal_node)

if path:
    print("Shortest Path:", "->".join(path))
    print("Total Cost:", cost)

