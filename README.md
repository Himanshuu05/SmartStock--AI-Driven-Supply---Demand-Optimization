# Smart Inventory Optimization

## Overview
This project implements a **Genetic Algorithm** for optimizing inventory levels in e-commerce or retail. It utilizes **Fuzzy Logic** for demand prediction and optimizes stock levels to minimize holding and shortage costs.

## Features
- **Fuzzy Logic Demand Prediction**: Estimates demand based on historical sales and seasonality.
- **Genetic Algorithm Optimization**: Uses evolutionary principles to find the optimal inventory level.
- **Cost Minimization**: Reduces inventory holding and shortage costs dynamically.

## How It Works
1. **Predict Demand**: Fuzzy logic determines demand based on sales and seasonality factors.
2. **Optimize Inventory**: The Genetic Algorithm iteratively evolves inventory levels to minimize costs.
3. **Final Recommendation**: Returns the most optimal inventory level for the given demand and cost structure.

## Installation & Usage
### Prerequisites
- Python 3.x

### Clone the Repository
```bash
git clone https://github.com/your-username/inventory-optimization.git
cd inventory-optimization
```

### Run the Script
```bash
python inventory_optimization.py
```

## Code Explanation
### Demand Prediction
```python
def predict_demand(sales, seasonality):
    if sales > 80 and seasonality > 70:
        return 100  # High demand
    elif sales > 50 and seasonality > 50:
        return 75  # Medium demand
    else:
        return 50  # Low demand
```

### Fitness Function
```python
def calculate_fitness(inventory, demand, holding_cost, shortage_cost):
    holding = (inventory - demand) * holding_cost if inventory > demand else 0
    shortage = (demand - inventory) * shortage_cost if inventory < demand else 0
    return 1 / (holding + shortage + 1)
```

### Genetic Algorithm for Inventory Optimization
```python
def optimize_inventory(demand, holding_cost, shortage_cost, population_size=10, generations=50):
    population = [random.uniform(0, 200) for _ in range(population_size)]
    for _ in range(generations):
        fitness = [calculate_fitness(ind, demand, holding_cost, shortage_cost) for ind in population]
        sorted_population = sorted(zip(population, fitness), key=lambda x: x[1], reverse=True)
        parent1, parent2 = sorted_population[0][0], sorted_population[1][0]
        new_population = [(parent1 + parent2) / 2 + random.uniform(-10, 10) for _ in range(population_size)]
        population = [max(0, min(child, 200)) for child in new_population]
    return max(population, key=lambda ind: calculate_fitness(ind, demand, holding_cost, shortage_cost))
```

## Example Output
```
Predicted Demand: 75
Optimal Inventory Level: 88.47
```

## Future Improvements
- Implement machine learning models for demand forecasting.
- Enhance genetic algorithm selection and mutation strategies.
- Integrate real-time data from sales databases.

## License
This project is open-source under the **MIT License**.

---
Contributions are welcome! Feel free to open an issue or submit a pull request. 🚀

