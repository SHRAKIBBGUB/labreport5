

# ♛ N-Queens Problem Solver (Genetic Algorithm)

This program uses a **Genetic Algorithm** to solve the classic **N-Queens problem**, where the goal is to place N queens on an N×N chessboard such that no two queens threaten each other.



## 📌 Description

* Each chromosome represents a possible solution (a permutation of queen positions).
* The fitness function evaluates how conflict-free a solution is.
* Uses:

  * **Tournament selection**
  * **One-point crossover**
  * **Random mutation**



## ✅ Sample Output


Solution found in generation 57: [0, 4, 7, 5, 2, 6, 1, 3]
Final Solution: [0, 4, 7, 5, 2, 6, 1, 3]






You can change the board size or genetic parameters in:

```python
solution = genetic_algorithm(8)
```

---

## 🧠 Key Components

* `generate_chromosome(n)`: Creates a random N-queens board.
* `calculate_fitness(chromosome)`: Returns how good the board is.
* `selection(population, fitnesses)`: Selects parents via tournament.
* `crossover(parent1, parent2)`: Combines parents to produce children.
* `mutate(chromosome)`: Randomly alters genes with a small probability.
* `genetic_algorithm(n, ...)`: Evolves the population toward a solution.

---

## ⚙️ Parameters

You can customize:

* `population_size` (default: 100)
* `max_generations` (default: 1000)
* `mutation_rate` (default: 0.1)

---

## ✅ Success Condition

The algorithm stops when it finds a solution with **no conflicts** (max fitness = `n*(n-1)/2`).


