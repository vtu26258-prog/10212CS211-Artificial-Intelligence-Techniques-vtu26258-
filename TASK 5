import numpy as np
from numpy import inf

# Distance matrix
d = np.array([
    [0, 10, 12, 11, 14],
    [10, 0, 13, 15, 8],
    [12, 13, 0, 9, 14],
    [11, 15, 9, 0, 16],
    [14, 8, 14, 16, 0]
])

iteration = 100
n_ants = 5
n_citys = 5

# Parameters
e = 0.5     # evaporation rate
alpha = 1   # pheromone factor
beta = 2    # visibility factor

# Calculate visibility (1 / distance)
visibility = 1 / d
visibility[visibility == inf] = 0

# Initialize pheromone matrix
pheromne = 0.1 * np.ones((n_citys, n_citys))

# Initialize routes
rute = np.ones((n_ants, n_citys + 1))

for ite in range(iteration):
    rute[:, 0] = 1  # All ants start at city 1

    for i in range(n_ants):
        temp_visibility = np.array(visibility)

        for j in range(n_citys - 1):
            combine_feature = np.zeros(n_citys)
            cur_loc = int(rute[i, j] - 1)
            temp_visibility[:, cur_loc] = 0  # Can't revisit same city

            p_feature = np.power(pheromne[cur_loc, :], alpha)
            v_feature = np.power(temp_visibility[cur_loc, :], beta)
            combine_feature = p_feature * v_feature

            total = np.sum(combine_feature)
            probs = combine_feature / total
            cum_prob = np.cumsum(probs)

            r = np.random.random_sample()
            city = np.nonzero(cum_prob > r)[0][0] + 1
            rute[i, j + 1] = city

        # Add the last remaining city
        left = list(set(range(1, n_citys + 1)) - set(rute[i, :-2]))[0]
        rute[i, -2] = left

    rute_opt = np.array(rute)
    dist_cost = np.zeros((n_ants, 1))

    for i in range(n_ants):
        s = 0
        for j in range(n_citys - 1):
            s += d[int(rute_opt[i, j]) - 1, int(rute_opt[i, j + 1]) - 1]
        dist_cost[i] = s

    dist_min_loc = np.argmin(dist_cost)
    dist_min_cost = dist_cost[dist_min_loc]
    best_route = rute[dist_min_loc, :]

    # Evaporation
    pheromne = (1 - e) * pheromne

    # Update pheromone
    for i in range(n_ants):
        for j in range(n_citys - 1):
            dt = 1 / dist_cost[i]
            a = int(rute_opt[i, j]) - 1
            b = int(rute_opt[i, j + 1]) - 1
            pheromne[a, b] += dt

# Final clean output
print("Route of all the ants at the end:")
print(rute_opt.astype(int))
print()
print("Best path:", best_route.astype(int))
print("Cost of the best path:", int(dist_min_cost[0]) + d[int(best_route[-2]) - 1, 0])
