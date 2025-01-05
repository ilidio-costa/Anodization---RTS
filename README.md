# Anodization Process Simulator

## Overview
This Python package simulates the anodization process of metals, specifically designed for aluminum oxide (Al₂O₃) formation. The simulator models the growth of oxide layers and current decay during the anodization process using fundamental electrochemical equations.

## Core Equations
The simulation is governed by three main equations:

1. **Oxide Layer Growth (Faraday's Law)**:
   ```
   d = (I * t * M) / ((x * y) * ρ * F * A)
   ```
   where:
   - d: Coating thickness (m)
   - I: Current (A)
   - t: Time (s)
   - M: Molar mass (kg/mol)
   - x, y: Stoichiometric coefficients of the oxide (AlxOy)
   - ρ: Density (kg/m³)
   - F: Faraday's constant (C/mol)
   - A: Surface area (m²)

2. **Resistance Calculation**:
   ```
   R = (d * ρ) / A
   ```
   where:
   - R: Resistance (Ω)
   - ρ: Resistivity (Ω·m)

3. **Current Decay (Ohm's Law)**:
   ```
   I = U / R
   ```
   where:
   - U: Applied voltage (V)

## Features
- Time-dependent simulation of oxide layer growth
- Current decay modeling
- Customizable process parameters
- Real-time visualization of results
- Support for porous oxide formation

## Installation Requirements
- Python 3.7+
- NumPy
- Matplotlib
- SciPy

## Usage Example
```python
params = {
    'M': 0.102,      # Molar mass of Al2O3 (kg/mol)
    'x': 2,          # Number of Al atoms
    'y': 3,          # Number of O atoms
    'Density': 3950, # Density of Al2O3 (kg/m³)
    'rho': 8e5,      # Resistivity of Al2O3 (Ω·m)
    'F': 96485,      # Faraday's constant (C/mol)
    'A': 0.2,        # Surface area (m²)
    'I0': 0.7,       # Initial current (A)
    'V': 60,         # Applied voltage (V)
}

simulator = AnodizationSimulator(**params)
results = simulator.simulate()
simulator.plot_results(results)
```

## Class Structure
- `SimulationResults`: Dataclass for storing simulation results
- `AnodizationSimulator`: Main simulation class
  - `__init__`: Initialize simulation parameters
  - `simulate`: Run the simulation
  - `plot_results`: Visualize the results
  - `current_decay`: Calculate current at each time step
  - `thickness_rate`: Calculate oxide growth rate

## Parameters
### Required Parameters
- `M`: Molar mass of the oxide compound (kg/mol)
- `x`, `y`: Stoichiometric coefficients for the oxide (AlxOy)
- `Density`: Material density (kg/m³)
- `rho`: Material resistivity (Ω·m)
- `F`: Faraday's constant (C/mol)
- `A`: Surface area (m²)
- `I0`: Initial current (A)
- `V`: Applied voltage (V)

### Optional Parameters
- `pores_density`: Fraction of porous space (default: 0.6)
- `total_time`: Total simulation time in seconds (default: 18000)
- `num_points`: Number of simulation points (default: 1000)
- `efficiency`: Anodization efficiency factor (default: 1)

## Output
The simulator generates two plots:
1. Oxide layer thickness vs. time
2. Current vs. time

Results can be saved as high-resolution images (300 DPI) if a save path is specified.

## Error Handling
- Input validation for positive parameters
- Minimum thickness threshold handling
- Exception handling for invalid parameters

## Notes
- The simulator assumes ideal conditions and uniform oxide growth
- Pore formation is modeled through density adjustment
- The efficiency factor can be adjusted to account for real-world losses
