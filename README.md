# Autonomous Delivery Agent System - Technical Report

**Created and adapted by Vedant Patil**

---

## 1. Environment Model

### Grid Representation
The system uses a 2D grid environment where each cell represents a location in the city. The grid supports:

- **Static obstacles:** Buildings that cannot be crossed
- **Terrain costs:** Different movement costs for various terrain types
- **Dynamic obstacles:** Moving vehicles with deterministic schedules

### Terrain Types and Costs
- **Road:** Cost 1 (fastest movement)  
- **Grass:** Cost 2 (moderate movement)  
- **Water:** Cost 3 (slower movement)  
- **Mountain:** Cost 4 (slowest movement)  
- **Building:** Impassable (infinite cost)

### Movement Model
- 4-connected movement (up, down, left, right)  
- Agent can move one cell per time step  
- Movement cost depends on terrain type  
- Dynamic obstacles can block paths and require replanning

---

## 2. Agent Design

### Core Components
- **State Management:** Tracks position, time, fuel, and package status  
- **Task Management:** Handles multiple delivery tasks with priorities  
- **Planning Module:** Selects and executes search algorithms  
- **Replanning System:** Detects path invalidity and triggers replanning  

### Planning Strategies
The agent supports six planning strategies:

1. **Breadth-First Search (BFS)**  
2. **Uniform-Cost Search**  
3. **A* with Manhattan Distance**  
4. **A* with Euclidean Distance**  
5. **Hill-Climbing**  
6. **Simulated Annealing**

---

## 3. Search Algorithms

### Uninformed Search
- **BFS:** Optimal for unweighted graphs  
- **Uniform-Cost Search:** Optimal for weighted graphs  

### Informed Search
- **A\*:** Uses heuristics for goal-directed search  
  - Manhattan distance: |x1-x2| + |y1-y2|  
  - Euclidean distance: √((x1-x2)² + (y1-y2)²)

### Local Search
- **Hill-Climbing:** Greedy search with random restarts  
- **Simulated Annealing:** Probabilistic acceptance of worse solutions

---

## 4. Dynamic Replanning

### Triggers
- Path blocked by moving obstacles  
- Agent reaches end of current path  
- New tasks are added

### Process
1. Detect invalid path  
2. Clear current path  
3. Replan using current strategy  
4. Continue execution

---

## 5. Experimental Results

### Test Maps
- Small (10x10)  
- Medium (20x20)  
- Large (50x50)  
- Dynamic (15x15)

### Metrics
- Success Rate  
- Path Cost  
- Nodes Expanded  
- Planning Time  
- Replanning Events

### Expected Results
- **A* (Manhattan):** Best overall performance  
- **Uniform-Cost Search:** Optimal solutions, slower  
- **BFS:** Simple, fast, but poor for weighted maps  
- **Local Search:** Variable, fast for large problems

---

## 6. Analysis & Conclusions
- **Heuristic Quality Matters** – Manhattan distance guides better than Euclidean  
- **Replanning is Essential** – Handles moving obstacles efficiently  
- **Strategy Selection** – Different algorithms fit different scenarios  
- **Scalability** – A* balances performance and size effectively  

### Future Improvements
- Adaptive strategy selection  
- Multi-agent coordination  
- Handling uncertainty in obstacles  
- Real-time optimization

---

## 7. Implementation Details

### File Structure

├── environment.py
├── search_algorithms.py
├── delivery_agent.py
├── cli.py
├── demo.py
├── test_system.py
├── requirements.txt
└── README.md



### Dependencies
- Python 3.7+  
- NumPy  
- Matplotlib  

### Usage
```bash
# Create test maps
python cli.py create-maps

# Run algorithm comparison
python cli.py compare --map small --start 0,0 --goal 9,9

# Run delivery simulation
python cli.py simulate --map medium --strategy astar_manhattan

# Run comprehensive experiment
python cli.py experiment

# Generate analysis plots
python cli.py analyze

# Run demonstration
python demo.py



