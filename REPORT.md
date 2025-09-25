# Autonomous Delivery Agent System - Technical Report

**Created and adapted by Vedant Patil**

---

## 1. Environment Model

### Grid Representation
The system uses a 2D grid to represent the city. Each cell corresponds to a specific location. The grid supports:

- **Static obstacles:** Buildings that cannot be crossed  
- **Terrain costs:** Different movement costs depending on terrain  
- **Dynamic obstacles:** Vehicles moving along predetermined schedules

### Terrain Types and Costs
| Terrain   | Cost |
|-----------|------|
| Road      | 1 (fastest) |
| Grass     | 2 (moderate) |
| Water     | 3 (slower) |
| Mountain  | 4 (slowest) |
| Building  | Impassable |

### Movement Model
- Agent moves one cell per step (up, down, left, right)  
- Movement cost depends on terrain  
- Dynamic obstacles may block paths, requiring replanning  

---

## 2. Agent Design

### Core Features
- **State Management:** Keeps track of position, fuel, time, and package status  
- **Task Management:** Handles multiple delivery tasks with priorities  
- **Planning Module:** Executes different search algorithms  
- **Replanning System:** Detects blocked paths and replans accordingly  

### Planning Strategies
The agent can use six strategies:

1. Breadth-First Search (BFS)  
2. Uniform-Cost Search  
3. A* with Manhattan Distance  
4. A* with Euclidean Distance  
5. Hill-Climbing (with random restarts)  
6. Simulated Annealing (probabilistic local search)

---

## 3. Search Algorithms

### Uninformed Search
- **BFS:** Explores all nodes at current depth, good for unweighted grids  
- **Uniform-Cost Search:** Expands nodes by increasing path cost, guarantees optimal paths  

### Informed Search
- **A*** uses a heuristic to guide the search:  
  - Manhattan distance: |x1-x2| + |y1-y2|  
  - Euclidean distance: √((x1-x2)² + (y1-y2)²)

### Local Search
- **Hill-Climbing:** Greedy search with random restarts to avoid local optima  
- **Simulated Annealing:** Accepts worse solutions probabilistically to explore more  

---

## 4. Dynamic Replanning

### When Replanning Happens
- Path blocked by moving obstacles  
- Agent reaches the end of current path  
- New tasks are added

### How Replanning Works
1. Detect invalid paths  
2. Clear current plan  
3. Recompute path using the current strategy  
4. Continue execution  

---

## 5. Experiments & Results

### Test Maps
- **Small (10x10):** Simple obstacles  
- **Medium (20x20):** More complex terrain  
- **Large (50x50):** Multiple building clusters  
- **Dynamic (15x15):** Moving obstacles

### Performance Metrics
- Success Rate (percentage of successful deliveries)  
- Path Cost  
- Nodes Explored  
- Planning Time  
- Replanning Events  

### Expected Observations
- **A* with Manhattan:** Best balance of speed and solution quality  
- **Uniform-Cost Search:** Guarantees optimal paths, slower  
- **BFS:** Fast for simple, unweighted maps  
- **Local Search:** Variable; good for large maps, may fail on complex constraints  

---

## 6. Analysis & Insights
- Manhattan heuristic works better than Euclidean on grid maps  
- Dynamic environments require frequent replanning  
- Choosing the right strategy depends on map size and constraints  
- A* provides scalable performance across most scenarios  

---

## 7. Future Enhancements
- Auto-select planning strategy based on the scenario  
- Multi-agent coordination for simultaneous deliveries  
- Handle unpredictable obstacle movement  
- Real-time optimization during execution  

---

## 8. Implementation Details

### File Structure
├── environment.py

├── search_algorithms.py

├── delivery_agent.py

├── cli.py

├── demo.py

├── test_system.py

├── requirements.txt

└── REPORT.md


### Dependencies
- Python 3.7+  
- NumPy  
- Matplotlib  

### Usage Examples
```bash
# Create maps
python cli.py create-maps

# Compare algorithms
python cli.py compare --map small --start 0,0 --goal 9,9

# Simulate delivery
python cli.py simulate --map medium --strategy astar_manhattan

# Run full experiment
python cli.py experiment

# Generate plots
python cli.py analyze

# Demo
python demo.py

This project demonstrates a complete autonomous delivery agent system capable of handling dynamic obstacles, multiple terrains, and various planning strategies. Developed and adapted by Vedant Patil.
