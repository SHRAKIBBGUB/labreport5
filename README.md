# labreport5


import random

def generate_chromosome(n):
    return [random.randint(0, n-1) for _ in range(n)]

def calculate_fitness(chromosome):
    n = len(chromosome)
    clashes = 0
    for i in range(n):
        for j in range(i+1, n):
            if chromosome[i] == chromosome[j] or abs(i - j) == abs(chromosome[i] - chromosome[j]):
                clashes += 1
    max_fitness = n * (n - 1) / 2
    return max_fitness - clashes

def selection(population, fitnesses, k=3):
    selected = random.choices(population, weights=fitnesses, k=k)
    return max(selected, key=lambda x: calculate_fitness(x))

def crossover(parent1, parent2):
    n = len(parent1)
    crossover_point = random.randint(1, n-1)
    child = parent1[:crossover_point] + parent2[crossover_point:]
    return child

def mutate(chromosome, mutation_rate=0.1):
    n = len(chromosome)
    for i in range(n):
        if random.random() < mutation_rate:
            chromosome[i] = random.randint(0, n-1)
    return chromosome

def genetic_algorithm(n, population_size=100, max_generations=1000):
    population = [generate_chromosome(n) for _ in range(population_size)]
    best_solution = None
    best_fitness = 0

    for generation in range(max_generations):
        fitnesses = [calculate_fitness(chrom) for chrom in population]
        current_best = max(population, key=lambda x: calculate_fitness(x))
        current_fitness = calculate_fitness(current_best)
        
        if current_fitness > best_fitness:
            best_solution = current_best
            best_fitness = current_fitness
        
        if best_fitness == n * (n - 1) / 2:
            print(f"Solution found in generation {generation}: {best_solution}")
            return best_solution
        
        new_population = []
        for _ in range(population_size // 2):
            parent1 = selection(population, fitnesses)
            parent2 = selection(population, fitnesses)
            child1 = crossover(parent1, parent2)
            child2 = crossover(parent2, parent1)
            new_population.extend([mutate(child1), mutate(child2)])
        
        population = new_population
    
    print("Best solution found:", best_solution)
    return best_solution


solution = genetic_algorithm(8)
print("Final Solution:", solution)
