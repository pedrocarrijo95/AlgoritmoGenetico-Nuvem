# 🧬 Genetic Algorithm for Cloud Resource Optimization

## 🚀 Context

In a growing tech company, the engineering team faced a recurring challenge: **efficiently allocating CPU and memory resources** on cloud servers for multiple clients — all without autoscaling capabilities. Manual adjustments became costly and unsustainable.

---

## 🎯 The Challenge

The main objective was to **minimize operational costs and response times** by dynamically adjusting server configurations (CPU and RAM) to meet client demands, while respecting fixed and variable costs.

---

## 🧠 The Genetic Solution

We implemented a **Genetic Algorithm (GA)** to optimize resource allocation in a simulated cloud environment.

### ⚙️ GA Flow:

1. **Initialization** – Randomly generate multiple server configurations.
2. **Evaluation** – Calculate performance based on client demand, using:
   - Response Time ⏱️
   - Operational Cost 💰
3. **Selection** – Choose the best-performing configurations.
4. **Crossover** – Mix CPU and memory values from selected pairs.
5. **Mutation** – Randomly mutate server configs to explore new possibilities.
6. **Iteration** – Repeat for multiple generations, keeping the best solution each round.

---

## 📊 Fitness Function

The **fitness function** was designed to minimize the weighted sum of:

- ⏱ **Average response time (70%)**
- 💰 **Operational cost (30%)**

```python
fitness = 0.7 * avg_response_time + 0.3 * operational_cost
```

## 🧪 Experiment Parameters

To simulate the optimization of server configurations, we defined a set of parameters to guide the behavior of the genetic algorithm.

| Parameter            | Description                                 | Value              |
|----------------------|---------------------------------------------|--------------------|
| **Population Size**  | Number of server configurations per generation | `100`            |
| **Generations**      | Number of iterations the algorithm runs     | `500`              |
| **Mutation Probability** | Chance of altering an individual’s configuration | `80%`        |
| **Clients Simulated**| Number of unique client demand entries      | `100`              |
| **CPU Range**        | Range of CPU units available per server     | `1 – 100`          |
| **Memory Range**     | Range of memory (RAM) per server (in GB)    | `8 – 1000`         |
| **Fixed Cost**       | Static cost per server                      | `50.0`             |
| **CPU Cost per Unit**| Cost per unit of CPU                        | `0.5`              |
| **Memory Cost per GB**| Cost per unit of RAM                       | `0.2`              |

These parameters reflect a realistic scenario in which server resources must be provisioned efficiently in a fixed-capacity cloud environment without autoscaling.

🔁 All server configurations are evaluated against the same 100 simulated client demands.

## 📉 Optimization Strategy

The genetic algorithm follows a structured evolutionary approach to find the best server configuration:

### 🔁 Per Generation Steps

1. **Fitness Evaluation**
   - Each individual (server configuration) is evaluated using a fitness function that balances:
     - ⏱ **Average Response Time** (70% weight)
     - 💰 **Operational Cost** (30% weight)

2. **Sorting**
   - The population is sorted by fitness (ascending), ensuring the best solutions are prioritized.

3. **Elitism**
   - The best-performing configuration is automatically carried over to the next generation.

4. **Selection**
   - Two parents are randomly chosen from the **top 10 best solutions**.

5. **Crossover**
   - Parents are combined (CPU from one, memory from the other) to create a new child configuration.

6. **Mutation**
   - With a high probability (80%), the child is mutated by assigning new random CPU and memory values.

7. **Replacement**
   - The new child is added to the new generation. This continues until the population is fully rebuilt.

8. **Update Best Solution**
   - If a new best fitness is found, it's logged and stored for future reference.

---

🔍 **Goal**:  
Gradually evolve the population to minimize **response time and cost**, achieving optimal configurations over generations.

## 📈 Sample Output

Throughout the execution of the genetic algorithm, we tracked the best configuration and fitness in each generation.

### 🖨️ Console Log Example

```bash
Generation 34: Best solution = (62, 715)
Generation 35: Best solution = (62, 715)
//////
New Best: (60, 734)
Generation 36: Best fitness = 186.01 | Best solution = (60, 734)
//////
Generation 37: Best solution = (60, 734)
...
Generation 152: Best fitness = 183.76 | Best solution = (58, 749)
```

## 🧠 Interpretation
- The fitness value represents a weighted combination of response time and cloud cost.
- A new best solution is printed only when it outperforms the previous generation’s top result.
- Over time, the population converges toward more optimal server configurations.
