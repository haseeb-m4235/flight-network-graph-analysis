# Global Flight Network Analysis

Graph analysis of the worldwide air travel network using real-world airport and route data. Identifies the most critical airports by three distinct centrality metrics and plots them on interactive world maps.

---

## Overview

The global air travel network can be modeled as a graph where **airports are nodes** and **flight routes are edges**. This project builds that graph from raw OpenFlights data and applies graph theory to rank airports by their structural importance — not just by passenger volume, but by how central they are to the network's connectivity.

Three centrality questions are answered:

| Metric | Question answered |
|---|---|
| **Degree Centrality** | Which airports have the most direct connections? |
| **Betweenness Centrality** | Which airports are critical bridges between distant regions? |
| **Eigenvector Centrality** | Which airports are connected to other well-connected airports? |

---

## Dataset

Uses the [OpenFlights](https://openflights.org/data.html) dataset:

- **`airports.dat`** — ~7,600 airports worldwide with name, city, country, latitude, longitude
- **`routes.dat`** — ~67,000 airline routes between source and destination airports

> **Note:** These data files are not included in the repo. Download them from the OpenFlights website and place them in the project root.

---

## Key Findings

### Degree Centrality — Most Connected Hubs
Top airports by raw number of direct route connections:

| Rank | Airport | Centrality |
|---|---|---|
| 1 | Amsterdam Airport Schiphol | 0.02276 |
| 2 | Frankfurt am Main Airport | 0.02239 |
| 3 | Charles de Gaulle International Airport | 0.02202 |
| 4 | Atatürk International Airport | 0.02138 |
| 5 | Hartsfield-Jackson Atlanta International Airport | 0.01991 |

### Betweenness Centrality — Critical Transit Points
Top airports that lie on the most shortest paths between other airports (removing them would most disrupt global connectivity):

| Rank | Airport | Centrality |
|---|---|---|
| 1 | Charles de Gaulle International Airport | 0.00542 |
| 2 | Los Angeles International Airport | 0.00514 |
| 3 | Ted Stevens Anchorage International Airport | 0.00513 |
| 4 | Dubai International Airport | 0.00463 |
| 5 | Frankfurt am Main Airport | 0.00450 |

> Anchorage appearing in the top 3 for betweenness (but not degree) reflects its geographic role as a transiting hub between North America and Asia.

### Eigenvector Centrality — Influence in the Network
Top airports connected to other highly-connected airports (similar to PageRank):

| Rank | Airport | Centrality |
|---|---|---|
| 1 | Amsterdam Airport Schiphol | 0.16788 |
| 2 | Frankfurt am Main Airport | 0.16639 |
| 3 | Charles de Gaulle International Airport | 0.15947 |
| 4 | Munich Airport | 0.14850 |
| 5 | Leonardo da Vinci–Fiumicino Airport | 0.13633 |

---

## Visualizations

Each centrality metric produces an interactive Plotly scatter-geo map. Bubble size encodes centrality score. Hover to see city name.

- Top 10 by Degree Centrality
- Top 10 by Betweenness Centrality
- Top 10 by Eigenvector Centrality

---

## Tech Stack

- **Python 3**
- **NetworkX** — graph construction and centrality computation
- **Plotly / Plotly Express** — interactive geographic visualizations
- **Pandas** — data manipulation for plotting
- **Jupyter Notebook** — analysis environment

---

## Setup

```bash
# Clone the repo
git clone <repo-url>
cd Analyzing-a-real-world-graph-dataset-of-a-global-flight-network

# Install dependencies
pip install networkx plotly pandas

# Download dataset files
# Get airports.dat and routes.dat from https://openflights.org/data.html
# Place both files in the project root

# Run the notebook
jupyter notebook main.ipynb
```

---

## Project Structure

```
.
├── main.ipynb        # Full analysis notebook
├── airports.dat      # Airport data (download separately)
├── routes.dat        # Route data (download separately)
└── README.md
```

---

## Concepts Demonstrated

- **Graph construction** from raw CSV data using NetworkX
- **Degree centrality** — normalized count of direct neighbors
- **Betweenness centrality** — fraction of all-pairs shortest paths passing through a node
- **Eigenvector centrality** — recursive importance based on neighbor importance
- **Geographic visualization** of network metrics using Plotly scatter-geo
