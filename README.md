#  Citibike Network Analysis Using Apache Spark & GraphFrames

This project performs a graph-based analysis of New York City's Citibike system using  
**Apache Spark**, **GraphFrames**, and **Scala**.  
We model station-to-station bicycle flows as a directed graph, then apply network algorithms  
to identify:

- Stations most likely to become **over-full**  
- Stations most likely to become **empty**  
- Stations with **high clustering** (dense local connectivity)

These insights are useful for **rebalancing operations**, **resource deployment**,  
and understanding **urban mobility patterns**.

---

##  Project Overview

This project transforms raw Citibike trip data into a directed graph:

(start_station) ──(trip_count)──> (end_station)

Using this graph, we compute:

### ✔ PageRank for **over-fullness**
Measures which stations are major “sinks” in the network.

### ✔ PageRank for **emptiness** (reversed graph)
Shows major “sources” that send bikes out and risk running empty.

### ✔ Clustering coefficient per station  
Quantifies how dense and interconnected a station’s neighborhood is.

---

## � Motivation

CitiBike needs to decide where to deploy staff to:

- Remove bikes from **over-full** stations  
- Deliver bikes to **empty** stations  
- Monitor regions with **high connectivity**  

Network analysis provides a data-driven method for operational planning.

---

##  Technologies Used
- Apache Spark  
- GraphFrames  
- Scala  
- Spark SQL  
- Graph theory (PageRank, clustering coefficient)

---

##  Repository Structure

.
├── citibike-graph-analysis.ipynb # Main analysis notebook
├── data/ # Source trip and station datasets
└── README.md

---

##  Core Steps in the Analysis

### **1. Load and preprocess trip data**
- Extract station IDs  
- Count directional flows  
- Build edge list for the graph

### **2. Construct GraphFrames graph**
- Vertices = stations  
- Edges = station-to-station trips  
- Weight = number of trips  

### **3. PageRank for over-fullness**
We run PageRank on the **directed graph** to rank stations receiving heavy inflow.

> These are the stations most likely to become **too full**.

### **4. PageRank for emptiness (reversed graph)**
Reverse every edge:

start → end becomes end → start

Run PageRank again to find stations most likely to **run empty**.

### **5. Clustering coefficient**
On the undirected version of the graph:

C = actual_triangles / possible_triangles

We identify highly interconnected neighborhoods in the CitiBike system.

---

##  Example Results

### Top 5 Over-Fullness Stations
(Results will depend on dataset)

Station A
Station B
Station C
Station D
Station E

### Top 5 Emptiness Stations (Reversed PageRank)
Station X
Station Y
Station Z
Station W
Station V

### Top 20 Highest Clustering Coefficients
- Indicates stations in tightly connected communities  
- Useful for understanding local mobility dynamics  

---

##  How to Run the Notebook

1. Install dependencies:
   - Apache Spark 3.x  
   - GraphFrames package  
   - Scala kernel (Toree / Databricks / Zeppelin)

2. Place source data in the `data/` directory.

3. Launch the notebook and run cells sequentially.

4. GraphFrames requires:
--packages graphframes:graphframes:0.8.2-spark3.2-s_2.12

---

##  Insights & Interpretation

- **High PageRank (directed graph)** → stations receiving many bikes  
- **High PageRank (reversed graph)** → stations sending out many bikes  
- **High clustering coefficient** → densest neighborhoods, strong community structures  

CitiBike operations teams can use these to:

- Optimize truck routes  
- Preemptively rebalance stations  
- Identify mobility hubs  
- Improve customer experience  

---
