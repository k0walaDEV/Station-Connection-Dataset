# Station & Connection Dataset

A sample transportation network dataset designed for students, developers, and researchers working with graph theory, network analysis, and pathfinding algorithms.

This repository provides two CSV files representing stations and the connections between them. The dataset can be used to experiment with graph traversal, shortest-path algorithms, route optimization, and other network-related problems without needing to collect or structure data from scratch.

## Dataset Overview

The dataset contains:

- **13 stations**
- **18 connections**
- X/Y coordinates for representing station positions on an abstract grid
- Connection time, distance, and fare attributes

All values are illustrative. They should not be interpreted as verified real-world transportation data.

## Repository Structure

```text
.
├── stations.csv
├── connections.csv
├── README.md
└── LICENSE
```

## Files

### `stations.csv`

Contains information about individual stations.

| Column | Description |
|---|---|
| `id` | Unique identifier for each station |
| `name` | Station name |
| `x` | X-coordinate on an abstract grid |
| `y` | Y-coordinate on an abstract grid |

Example:

```csv
id,name,x,y
S1,Central Hub,4,4
S2,Civic Center,6,4
S3,Airport,13,5
```

### `connections.csv`

Contains the links between stations.

| Column | Description |
|---|---|
| `from` | Starting station ID |
| `to` | Destination station ID |
| `time` | Illustrative travel-time value |
| `distance` | Illustrative distance value |
| `fare` | Illustrative fare value |

Example:

```csv
from,to,time,distance,fare
S1,S2,4,2.4,20
S1,S12,3,2.4,15
S1,S8,8,4.4,30
```

The units for `time`, `distance`, and `fare` are not specified by the dataset. Define and document suitable units in your project before interpreting or comparing these values.

## Possible Use Cases

This dataset can be used to practice or demonstrate:

- **Dijkstra's algorithm** — shortest paths using distance, time, or fare as edge weights.
- **A* search** — heuristic-based pathfinding using station coordinates.
- **Breadth-First Search (BFS)** — reachability and minimum-hop paths.
- **Depth-First Search (DFS)** — graph traversal.
- **Bellman-Ford** — weighted shortest-path problems.
- **Floyd-Warshall** — shortest paths between all pairs of stations.
- **Minimum Spanning Tree (MST)** — minimum-cost network connectivity.
- **Graph visualization** — displaying nodes and edges.
- **Route comparison** — comparing paths using different edge attributes.

## Getting Started with Python

Install the required packages:

```bash
pip install pandas networkx
```

Load the CSV files and build a directed graph:

```python
import pandas as pd
import networkx as nx

stations = pd.read_csv("stations.csv")
connections = pd.read_csv("connections.csv")

# The connection records are represented as directed edges:
# from -> to
graph = nx.DiGraph()

for _, station in stations.iterrows():
    graph.add_node(
        station["id"],
        name=station["name"],
        x=station["x"],
        y=station["y"],
    )

for _, connection in connections.iterrows():
    graph.add_edge(
        connection["from"],
        connection["to"],
        time=connection["time"],
        distance=connection["distance"],
        fare=connection["fare"],
    )

# Example: find a route from S1 to S11 using distance as the weight.
route = nx.shortest_path(
    graph,
    source="S1",
    target="S11",
    weight="distance",
)

print("Route:", " -> ".join(route))
```

If your project treats travel as bidirectional, you can either add a reverse edge for every connection or use an undirected graph. Make that choice explicitly: the CSV itself records each connection in the direction shown by its `from` and `to` columns.

## Data Notes and Limitations

- Station IDs are intended to be unique and are used to associate connections with stations.
- Coordinates represent positions on an abstract grid; they are not verified geographic coordinates.
- Connection rows describe directed links from `from` to `to`. A reverse connection should not be assumed unless it is separately present or added by your application.
- The values in `time`, `distance`, and `fare` are illustrative, not verified measurements, schedules, or actual prices.
- `Hilltop Annex` (`S13`) is included as an isolated station with no listed connections. It can be useful when testing disconnected nodes and graph connectivity.
- The dataset is small and intended for learning, demonstrations, and testing. It is not designed to model the complexity or reliability requirements of a production transportation system.

## Intended Audience

- Computer science and software engineering students
- Students learning graph theory and pathfinding
- Developers prototyping route-finding applications
- Educators preparing programming exercises
- Anyone who needs a small CSV-based network dataset for experimentation

## Contributing

Contributions and improvements are welcome. Possible contributions include:

- Adding stations or connections
- Providing examples in other programming languages
- Adding demonstrations of pathfinding algorithms
- Improving documentation or data validation

When modifying the CSV files, please preserve the existing column names and ensure that every `from` and `to` value refers to a station ID in `stations.csv`.

## License

This repository includes a `LICENSE` file. Review it before using, modifying, or redistributing the dataset.
