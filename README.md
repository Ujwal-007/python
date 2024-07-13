# Genetic Algorithm for Solving Quadratic Equations

This project implements a genetic algorithm to find the solution for a quadratic equation of the form `3x^2-7x+2=0` using binary encoding, uniform crossover, and mutation.

## Table of Contents
- [Introduction](#introduction)
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Algorithm Details](#algorithm-details)
  - [Fitness Function](#fitness-function)
  - [Binary Encoding](#binary-encoding)
  - [Uniform Crossover](#uniform-crossover)
  - [Mutation](#mutation)
- [Results](#results)

## Introduction

This project demonstrates how to use genetic algorithms to solve a quadratic equation. The genetic algorithm evolves a population of binary-encoded individuals over several generations to find the best solution.

## Features

- Binary encoding of individuals
- Uniform crossover to produce offspring
- Mutation to introduce variability
- Roulette wheel selection for choosing parents
- Fitness function based on the quadratic equation `3x^2-7x+2=0`

## Installation (Jupyter)

To run this project locally, follow these steps:

### 1. Clone the repository:

   ```bash
   git clone https://github.com/Ujwal-007/python.git
   cd Genetic_Algorithm
   ```

### 2. Create a virtual environment (optional but recommended):

   It's good practice to use virtual environments to isolate project dependencies.

   ```bash
   python3 -m venv venv
   source venv/bin/activate   # On Windows use `venv\Scripts\activate`
   ```

### 3. Install Jupyter Notebook and dependencies:

   Install Jupyter Notebook and other dependencies using `pip`.

   ```bash
   pip install jupyter
   pip install -r requirements.txt
   ```

   Replace `requirements.txt` with the actual file containing your project dependencies, if applicable.

### 4. Start Jupyter Notebook:

   Launch Jupyter Notebook to run the genetic algorithm notebook.

   ```bash
   jupyter notebook
   ```

### 5. Open the notebook:

   Navigate to the `genetic_algorithm.ipynb` file in your Jupyter Notebook interface and open it to execute the genetic algorithm code.

### 6. Run the genetic algorithm:

   Follow the instructions within the notebook to run the genetic algorithm and view results.

### 7. Shutdown Jupyter Notebook:

   Once finished, you can shutdown Jupyter Notebook by pressing `Ctrl + C` in the terminal where it's running and confirming the shutdown.

### 8. Deactivate virtual environment (if used):

   ```bash
   deactivate   # Only if you used a virtual environment
   ```
## Algorithm Details
### Fitness Function
  The fitness function evaluates how close a given solution is to the actual solution of the quadratic equation:
```bash
 def fitness(x):
    return 1 / (abs(a*x**2 + b*x + c) + 1e-6)
```

### Binary Encoding
  Each individual in the population is represented as a binary string:

```bash
def decode(binary_string):
    sign = -1 if binary_string[0] == '1' else 1
    integer_part = int(binary_string[1:7], 2)
    fractional_part = int(binary_string[7:], 2) / 16
    return sign * (integer_part + fractional_part)
```
### Uniform Crossover
  Uniform crossover creates two offspring from two parents by randomly selecting each bit from either parent:

```bash
   next_generation = []
    for i in range(0, population_size, 2):
        parent1 = parents[i]
        parent2 = parents[i+1]
        crossover_point = random.randint(1, 10)  # Single-point crossover
        child1 = parent1[:crossover_point] + parent2[crossover_point:]
        child2 = parent2[:crossover_point] + parent1[crossover_point:]
        next_generation.extend([child1, child2])
```
### Mutation
  Mutation introduces random changes to an individual to maintain genetic diversity:

```bash
for i in range(len(next_generation)):
        if random.random() < mutation_rate:
            mutation_point = random.randint(0, 10)
            new_bit = '1' if next_generation[i][mutation_point] == '0' else '0'
            next_generation[i] = next_generation[i][:mutation_point] + new_bit + next_generation[i][mutation_point + 1:]
```
### Results
  After running the genetic algorithm, the best solution found will be printed along with its fitness value:
  
```text
Best individual found: 00000010100
Decoded best solution: x = 0.3125, Fitness = 0.10546875
```


