# Heat and Mass Transfer Modeling for Multistage Solar Distillation 
Predict water productivity of an MSD module with inputs from environmental factors (wind, atm transmittance, solar flux, ambient temperature) and top insulation configurations. 

This code simulates heat and mass transfer in multi-stage solar distillation (MSD) modules. It calculates water productivity, efficiency, and temperature of each stage for various operating conditions and design 
parameters. 

## 1. SYSTEM REQUIREMENTS 

1.1 Dependencies
-------------------------
Required Python Packages:
  - Python: 3.8 or higher (tested on 3.12.10)
  - NumPy: ≥ 1.20.0 (tested on 2.2.5)
  - SciPy: ≥ 1.7.0 (tested on 1.15.2)
  - pandas: ≥ 1.3.0 (tested on 2.2.3)
  - Jupyter Notebook or JupyterLab: ≥ 6.4.0 (tested on 7.2.2)

1.2 Hardware Requirements
-------------------------
No specialized hardware (e.g., GPU) is required.

1.3 Input Data Requirements
---------------------------
The code requires spectral transmittance data files, which are provided in the /data/ directory:
  -  AG_transmittance.csv
  - Glass_3mm_transmittance.csv 
  - PMMA_3mm_transmittance.csv


## 2. INSTALLATION GUIDE

2.1 Installing Python and Dependencies
---------------------------------------

Option A: Using Anaconda (Recommended)
1. Download and install Anaconda from https://www.anaconda.com/download
2. Open Anaconda Prompt (Windows) or Terminal (Mac/Linux)
3. Create a new environment:
   conda create -n MSD_sim python=3.12 numpy scipy pandas jupyter
4. Activate the environment:
   conda activate MSD_sim 

Option B: Using pip
1. Install Python 3.8+ from https://www.python.org/downloads/
2. Open Command Prompt/Terminal
3. Install required packages:
   pip install numpy scipy pandas jupyter

2.2 Downloading the Code
-----------------------------
Download all files to a local directory, maintaining folder structure


2.3 Typical Installation Time
------------------------------
- Anaconda installation: 15-20 minutes
- Package installation: 15-20 minutes
- Total time: ~30-40 minutes on a standard desktop computer

No compilation is required. The code runs directly in Jupyter notebooks.

## 3. DEMO

3.1 Quick Start Demo
--------------------
This demo runs a simple 6-stage simulation with default parameters.

Instructions:
1. Navigate to the project folder
2. Launch Jupyter:
   - Anaconda: jupyter notebook
   - Or use: jupyter lab
3. Open: notebooks/Demo.ipynb
4. Click "Cell" → "Run All" (or press Shift+Enter on each cell)

3.2 Expected Output
-------------------
The demo will:
- Simulate a 6-stage solar still with 6 mm aerogel cover under outdoor 2 m/s wind, 1kW/m2 solar flux, 25°C condition
- Calculate water productivity, evaporator and condenser temperature for each stage 
- Display convergence information

Expected Console Output:
```
Successfully loaded and processed Aerogel and atmospheric spectral data.

--- Running Multi-Stage Simulation for 6 Stages ---

Iteration 1: Calculated q_in,1 = 1319.44 W/m^2, Error = 406.73 W/m^2
Iteration 2: Calculated q_in,1 = 970.60 W/m^2, Error = 57.89 W/m^2
Iteration 3: Calculated q_in,1 = 922.59 W/m^2, Error = 9.88 W/m^2
Iteration 4: Calculated q_in,1 = 914.44 W/m^2, Error = 1.74 W/m^2
Iteration 5: Calculated q_in,1 = 913.01 W/m^2, Error = 0.31 W/m^2
Iteration 6: Calculated q_in,1 = 912.76 W/m^2, Error = 0.05 W/m^2

Convergence reached!

--- Per-Stage Detailed Results ---
  Stage 1: Evap Temp: 70.72°C | Condensation Temp: 66.12°C | Vapor Flux: 0.94 kg/m²/hr
  Stage 2: Evap Temp: 66.12°C | Condensation Temp: 61.09°C | Vapor Flux: 0.89 kg/m²/hr
  Stage 3: Evap Temp: 61.09°C | Condensation Temp: 55.43°C | Vapor Flux: 0.83 kg/m²/hr
  Stage 4: Evap Temp: 55.43°C | Condensation Temp: 48.86°C | Vapor Flux: 0.78 kg/m²/hr
  Stage 5: Evap Temp: 48.86°C | Condensation Temp: 40.79°C | Vapor Flux: 0.73 kg/m²/hr
  Stage 6: Evap Temp: 40.79°C | Condensation Temp: 30.00°C | Vapor Flux: 0.67 kg/m²/hr

Top Surface Temp: 33.41°C 

--- Overall Performance ---
Total Vapor Mass Flux: 4.84 kg/m²/hr
Total Efficiency (eta_tot): 317.18%
```

Expected Files Generated:
- No files are generated for demo. 
- For other notebooks, generated summary files will be stored in the /results/ folder.

Expected Run Time: 
- Total demo: 1 second


## 4. INSTRUCTIONS FOR USE

4.1 Basic Usage - Reproducing Figure 3 (for all) and Figure S15 (for no cover and glass) 
------------------------------------

Step 1: Open a notebook
  - For SSAL-insulated device: MSD_Aerogel.ipynb or MSD_Glass.ipynb or MSD_PMMA.ipynb
  - For no cover: MSD_NoCover.ipynb

Step 2: Run all cells

Step 3: Results are displayed in the notebook

Expected Run Time: 5 - 10 seconds

4.2 Output Files
----------------
Results are saved as CSV files in the results/ folder with format:
  - Filename: [cover_type]_simulation_FigXX_summary_[YYYYMMDD_HHMMSS].csv

Sample result CSV files are pre-saved in the results/ folder.


## 5. LICENSE AND ACKNOWLEDGMENTS

License: MIT

Acknowledgments:
- The code was developed based on the work by Zhang, L. et al., Modeling and performance analysis of high-efficiency thermally-localized multistage solar stills. Appl. Energy 2020, 266, 114864. DOI: 10.1016/j.apenergy.2020.114864.
- Atmospheric transmission data from UKIRT. The atmospheric transmission versus wavelength for Mauna Kea was produced using the program IRTRANS4 with the following parameters — Altitude: 4200m. Airmass: 1.0. H2O column: 1.2mm. Resolving power: 3000 


END OF README

