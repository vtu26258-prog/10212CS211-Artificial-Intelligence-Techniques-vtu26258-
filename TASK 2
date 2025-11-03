import random

def calculate_cost(path, graph):
    cost = 0
    for i in range(len(path) - 1):
        cost += graph[path[i]][path[i + 1]]
    cost += graph[path[-1]][path[0]]  # Return to start city
    return cost

def hill_climbing_tsp(graph, max_restarts=10):
    V = len(graph)
    best_path = None
    best_cost = float('inf')
    
    for _ in range(max_restarts):
        current_path = list(range(V))
        random.shuffle(current_path)
        current_cost = calculate_cost(current_path, graph)
        improved = True
        
        while improved:
            improved = False
            for i in range(V):
                for j in range(i + 1, V):
                    neighbor = current_path[:]
                    neighbor[i], neighbor[j] = neighbor[j], neighbor[i]
                    neighbor_cost = calculate_cost(neighbor, graph)
                    if neighbor_cost < current_cost:
                        current_path, current_cost = neighbor, neighbor_cost
                        improved = True
        
        if current_cost < best_cost:
            best_path = current_path
            best_cost = current_cost
    
    return best_path, best_cost

graph = [
    [0, 10, 15, 20],
    [10, 0, 35, 25],
    [15, 35, 0, 30],
    [20, 25, 30, 0]
]

if __name__ == "__main__":
    print("Hill Climbing TSP with Random Restarts\n")
    best_path, best_cost = hill_climbing_tsp(graph, max_restarts=20)
    print("Best Path Found:", best_path)
    print("Minimum Cost:", best_cost)
