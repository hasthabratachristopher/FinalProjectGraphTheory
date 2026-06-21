# Teori Graf: Pemodelan Wilayah Jakarta sebagai Graf Berbobot (COVID-19)

A graph theory project that models Jakarta's sub-districts (*kecamatan*) as a network graph, using COVID-19 case data to compute edge weights, visualize the network, and find its Minimum Spanning Tree (MST).

## Overview

Each **node** in the graph represents a *kecamatan* (sub-district) in Jakarta. **Edge weights** between nodes are derived from COVID-19 statistics, expressed under two scenarios:

- **Pesimis (Pessimistic)**: `Positif / Total Populasi` — confirmed positive cases over total population
- **Optimis (Optimistic)**: `(Positif + ODP) / Total Populasi` — confirmed positive cases plus *Orang Dalam Pemantauan* (people under monitoring) over total population

For each edge connecting two sub-districts, the weight is calculated as the **average of the two nodes' pessimism/optimism values**.

## Data

- **Source**: `Data Untuk Teori Graf.xlsx`
- **Key columns**:
  - `Nama Kec.` — sub-district name (used as graph nodes)
  - `Bobot Pesimis` — pessimistic weight per sub-district
  - `Bobot Optimis` — optimistic weight per sub-district

## Workflow

1. **Load & Inspect Data** — read the Excel dataset, check shape, structure, and missing values
2. **Define Nodes & Weights** — extract sub-district names as nodes; extract pessimistic/optimistic weight values
3. **Build the Graph**:
   - Construct an undirected graph (`networkx.Graph`) with sub-districts as nodes and adjacency relationships as edges
   - Assign each edge a weight equal to the average pessimism (or optimism) value of its two endpoint nodes
4. **Visualize the Graph** — draw the full network of Jakarta's sub-districts using a spring layout
5. **Minimum Spanning Tree (MST)** — compute and visualize the MST of the weighted graph using `networkx.minimum_spanning_tree`

## Tools & Libraries

- `pandas`, `numpy`
- `matplotlib`, `seaborn`
- `networkx` (graph construction, layout, MST)

## How to Run

```bash
pip install pandas numpy matplotlib seaborn networkx
```

1. Place `Data Untuk Teori Graf.xlsx` in the working directory (update the file path in the **Load Data** cell if needed).
2. Run the notebook `Tegraf.ipynb` sequentially in Jupyter or Google Colab.
3. The notebook will output:
   - The full weighted graph of Jakarta sub-districts
   - Printed edge weight calculations (pessimistic/optimistic)
   - The Minimum Spanning Tree of the network

## Output

- Network visualization of Jakarta's sub-districts as an undirected weighted graph
- Per-edge weight breakdown based on pessimistic/optimistic COVID-19 risk values
- Minimum Spanning Tree highlighting the lowest-risk connecting structure across sub-districts

## Notes

- This notebook contains a couple of unrelated/leftover code cells (e.g. a university ER diagram, an embedded snippet from a separate assignment on Orthogonal Polynomials). These are not part of the core graph analysis and can be removed for a cleaner repo.
