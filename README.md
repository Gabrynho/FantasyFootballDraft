# Fantasy Football Draft Using Genetic Algorithm

## Optimization for AI's Exam Project

*University of Studies of Trieste* - *"Data Science and AI"* Master's Degree A.Y. 2024/2025

## Overview

This project develops an advanced optimization framework for selecting fantasy football teams using Genetic Algorithms (GA). By leveraging real-world football data from top European leagues, the system aims to maximize expected points while adhering to strict budgetary and team composition constraints.  
The implementation explores two distinct approaches: a traditional Genetic Algorithm and an enhanced version that incorporates Montecarlo sampling of Points Per Match (PPM) during the evaluation phase. This stochastic approach provides a more realistic representation of player performance uncertainty throughout the season.

## 🎯 Problem Statement

The Fantasy Football Draft problem is formulated as a variant of the **binary knapsack problem** with additional constraints:

- **Objective**: Maximize total expected Points Per Match (PPM)
- **Constraints**: Budget limits, position requirements, team diversity rules
- **Variables**: Binary selection for each available player

## 📊 Data Sources

The project uses **FBref** data covering:

- 🏴󠁧󠁢󠁥󠁮󠁧󠁿 Premier League
- 🇪🇸 La Liga  
- 🇫🇷 Ligue 1
- 🇩🇪 Bundesliga
- 🇮🇹 Serie A
- 🇧🇪 Jupiler Pro League

## 🔧 Key Features

### 1. Data Processing Pipeline

- **Multi-league data extraction** from FBref
- **Fantasy scoring system** based on Kickest rules
- **Player pricing algorithm** considering age, position, performance, and team strength
- **Transfer and promotion/relegation adjustments**

### 2. Optimization Framework

- **Genetic Algorithm** implementation using PyMOO
- **Stochastic evaluation** with Monte Carlo simulation
- **Constraint handling** with custom repair mechanisms
- **Multi-threading** for performance optimization

### 3. Mathematical Modelization

$$
\begin{align*}
\text{maximize} & \sum_{i=1}^{n} \text{PPM}_i \cdot x_i \\
\text{subject to:} \\
& \sum_{i=1}^{n} \text{price}_i \cdot x_i \leq B \\
& \sum_{i \in P_{\text{GK}}} x_i = N_{\text{GK}} \\
& \sum_{i \in P_{\text{DF}}} x_i = N_{\text{DF}} \\
& \sum_{i \in P_{\text{MF}}} x_i = N_{\text{MF}} \\
& \sum_{i \in P_{\text{FW}}} x_i = N_{\text{FW}} \\
& \max_{t \in T} \left( \sum_{i \in T_t} x_i \right) \leq M \\
& x_i \in \{0, 1\} \quad \forall i \in N
\end{align*}
$$

## 🏗️ Project Structure

```k
FantasyFootballDraft/
├── football_draft_with_GA.ipynb    # Main implementation notebook
├── analysis.ipynb                  # Results analysis and visualization
├── README.md                       # This file
├── .gitignore                     # Git ignore rules
├── requirements.txt               # Python dependencies
├── convergence_*.csv              # Algorithm convergence data
├── fantasy_teams_solutions.csv    # GA optimization results
└── fantasy_teams_optimized_lp.csv # Linear programming comparison
```

## 🚀 Getting Started

### Prerequisites

```bash
pip install -r requirements.txt
```

Required packages:

- `pandas` - Data manipulation
- `numpy` - Numerical computations
- `matplotlib`, `seaborn` - Data visualization
- `soccerdata` - Football data extraction
- `pymoo` - Multi-objective optimization
- `pulp` - Linear programming (for comparison)
- `mplsoccer` - Football pitch visualization

### Running the Project

1. **Data Extraction & Processing**:

   ```python
   # Run cells 1-15 in football_draft_with_GA.ipynb
   # This extracts data, calculates PPM, and creates player datasets
   ```

2. **Optimization**:

   ```python
   # Run cells 16-20 to execute the Genetic Algorithm
   # Results are saved to fantasy_teams_solutions.csv
   ```

3. **Analysis**:

   ```python
   # Use analysis.ipynb for results visualization and comparison
   ```

## 🧬 Genetic Algorithm Configuration

### Population & Operators

- **Population Size**: 5,000 individuals
- **Crossover**: Half Uniform Crossover (HUX)
- **Mutation**: Bitflip Mutation
- **Selection**: Tournament Selection
- **Generations**: 20

### Evaluation Methods

- **Deterministic**: Uses fixed PPM values
- **Stochastic**: Monte Carlo sampling with performance uncertainty

### Constraint Handling

- **Repair Mechanism**: Custom `FeasibleTeams` operator
- **Position Balancing**: Ensures correct formation
- **Budget Management**: Intelligent player substitution
- **Team Diversity**: Prevents over-concentration

## 📈 Results & Performance

### Key Metrics

- **Convergence Analysis**: Algorithm performance across generations
- **Budget Allocation**: Spending patterns by position
- **ROI Analysis**: Return on investment per position
- **Stochastic vs Deterministic**: Performance comparison

### Visualization Features

- **Formation Plots**: Visual team lineups using mplsoccer
- **PPM Distribution**: Player performance by position and league
- **Convergence Curves**: Algorithm optimization progress
- **Budget Analysis**: Spending efficiency metrics

## 🎨 Fantasy Scoring System

Points allocation based on Kickest rules:

- **Appearances**: 5 pts (start), 2 pts (substitute)
- **Goals**: 14-50 pts (position-dependent)
- **Assists**: 7 pts
- **Cards**: -2 pts (yellow), -5 pts (red)
- **Goalkeeping**: Clean sheets (+10), saves (+1), penalties saved (+15)
- **Field Actions**: Shots, tackles, interceptions, fouls

## 🤝 Contributing

This is an academic project for the "Optimization for AI" course. Suggestions and improvements are welcome for educational purposes.

## 🔗 References

- **Data Source**: [FBref](https://fbref.com/) - Football statistics
- **Optimization Framework**: [PyMOO](https://pymoo.org/) - Multi-objective optimization
- **Fantasy Rules**: Inspired by [Kickest](https://www.kickest.it/) fantasy football
- **Visualization**: [mplsoccer](https://mplsoccer.readthedocs.io/) - Football pitch plotting
