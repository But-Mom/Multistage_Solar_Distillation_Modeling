# Heat and Mass Transfer Modeling for Multistage Solar Distillation 
Predict water productivity of an MSD module with inputs from environmental factors (wind, atm transmittance, solar flux, ambient temperature) and top insulation configurations. 

This code simulates heat and mass transfer in multi-stage solar distillation (MSD) modules. It calculates water productivity, efficiency, and temperature of each stage for various operating conditions and design 
parameters. 

<details><summary>Click to expand system requirements and installation guide. </summary>

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
</details>

## 3. DEMO

3.1 Quick Start Demo
--------------------
This demo runs a simple 6-stage simulation with default parameters.

Instructions:
1. Navigate to the project folder
2. Launch Jupyter:
   - Anaconda: jupyter notebook 
   - Or use: jupyter lab
3. Open: demo.ipynb
4. Click "Run" → "Run All" (or press Shift+Enter on each cell)

3.2 Expected Output
-------------------
The demo will:
- Simulate a 6-stage solar still with 6 mm aerogel cover under outdoor 2 m/s wind, 1kW/m² solar flux, 25°C condition
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

Expected Run Time: 1 second

3.3 Parametric study -- getting your hands a bit dirty
-------------------
To model MSD performance under different environmental conditions or module parameters, modify simulation parameters in the "params" cell. 
For instance, to change the solar flux from 1000 to 500 W/m² :
```python
params = {
    "q_sun": 500,           # Solar flux (W/m²)
    # ... other parameters
}
```
To change the condition from outdoor to indoor (where sky cooling is absent):
```python
params = {
    "condition": 'indoor',            
    # ... other parameters
}
```
Change the ambient temperature, and the code will update air properties, convective heat transfer coefficient (h_a), and backwall temperature (T_b_c). In this model, the backwall temperature is set to be 5°C higher than the ambient temperature.
```python
params = {
    "T_amb_c": 25,           # Ambient air temperature (Celsius)      
    # ... other parameters
}
```
Change the wind speed, and the code will update convective heat transfer coefficient (h_a) accordingly:
```python
params = {
    "v": 6.0,                # Wind speed (m/s)      
    # ... other parameters
}
```
You can also modify the module parameters such as width, unit stage thickness, or the thickness of sidewall insulation:
```python
params = {
    "a": 1.2,               # Device width (m)
    "b": 0.005,             # Unit stage thickness (m)
    "t_ins": 0.005,           # Insulation thickness (m)            
    # ... other parameters
}
```
To change stage number, adjust ```number of stages``` in the last cell:
```python
# --- Run the Simulation ---
if __name__ == "__main__":
    number_of_stages = 6  
    run_multistage_simulation(number_of_stages, params)
```

The demo allows the following aerogel thicknesses: 0 (no aerogel insulation), 2 mm, 4 mm, 6 mm, 8 mm, 12 mm. Due to lack of transmittance data, other thickness values are not accepted (for now). In the future, we may update the transmittance function based on thickness input. 
To change aerogel thickness, adjust the following parameter:
```python
params = {
    "t_ag": 0.006,           # Aerogel thickness (m); you can change it to the following values: [0, 0.002, 0.004, 0.006, 0.008, 0.012]     
    # ... other parameters
}
```

## 4. INSTRUCTIONS FOR USE

4.1 Basic Usage - Reproducing Figure 3 (for all configurations) and Figure S15 (for no cover and glass) 
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

