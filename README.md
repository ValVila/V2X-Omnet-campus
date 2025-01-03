# V2X-Omnet-
Omnet++ project thesis on GNSS vs GPS V2X communication 

# Campus Simulation Project

This project simulates vehicular and pedestrian movements in a campus environment. It integrates OpenStreetMap data, SUMO (Simulation of Urban MObility), and OMNeT++ for realistic and dynamic simulations. The project includes data for route mapping, GNSS/GPS comparison, and trajectory evaluation.

## Folder Structure

- **track mapping**: Contains coordinate data from a walk, mapped onto a graphical map. This serves as a baseline to simulate GNSS vs. GPS coordinates.
- **routes testings**: Includes `.rou` files generated for testing various routing scenarios in the simulation.
- **Graphs**: Contains extracted coordinates from vehicle routes, plotted as graphs for trajectory evaluation and movement pattern analysis.
- **results**: Stores outputs generated during simulations, including files for analyzing trajectories, trip information, and Floating Car Data (FCD). This folder is key for post-simulation analysis and visualization.

## Key Files

- `campus.sumocfg`: Configuration file for running the SUMO simulation. It defines simulation parameters, input files, and additional settings.
- `campus.rou.xml`: Defines pre-determined routes for vehicles in the simulation.
- `map1.osm.xml`: OpenStreetMap (OSM) data of the campus, used to generate the road network.
- `campus.net.xml`: Network file generated from the OSM data using `netconvert`.
- `Traci Script for Positional noise.ipynb`: Jupyter Notebook that uses TraCI (Traffic Control Interface) to introduce positional noise for trajectory testing.
- `positional deviation and trajectory calculation.ipynb`: Notebook for analyzing positional deviations and evaluating calculated trajectories.
- `randomtrips.py`: SUMO script for generating random trips based on the campus network. Used to create realistic `.rou` files for testing.

## Workflow Overview

1. **Generate Network**:
   - Use OpenStreetMap (OSM) data (`map1.osm.xml`) and convert it into a SUMO network (`campus.net.xml`) using the `netconvert` tool:
     ```bash
     netconvert --osm-files map1.osm.xml -o campus.net.xml
     ```

2. **Generate Routes**:
   - Use the `randomtrips.py` script to generate random routes for the vehicles based on the network:
     ```bash
     python randomTrips.py -n campus.net.xml -o map1.trips.xml
     ```

3. **Compile Project**:
   - Use CMake to build the project for OMNeT++:
     ```bash
     cmake --build build --target campus
     ```

4. **Run Simulation**:
   - Use the `campus.sumocfg` configuration file to run the SUMO simulation.
   - Analyze outputs, such as `fcd_output.xml` (Floating Car Data) and `tripinfo_output.xml` (trip statistics).

5. **Analyze Results**:
   - The `results` folder contains output files for trajectory analysis and visualizations.
   - Use Jupyter Notebooks, such as `positional deviation and trajectory calculation.ipynb`, for detailed evaluation.

## Software and Tools

- **OMNeT++**: A discrete-event network simulator used for the simulation framework.
- **SUMO**: A traffic simulation tool used for defining and managing vehicle movements.
- **TraCI**: A Python interface for controlling and extracting data from SUMO simulations.
- **netconvert**: Converts OSM files into SUMO-readable network files.
- **randomtrips.py**: SUMO script for generating random routes in the network.

## Results Folder

The `results` folder serves as a repository for all simulation outputs:
- **Floating Car Data (`fcd_output.xml`)**: Logs detailed position and speed data for vehicles.
- **Trip Information (`tripinfo_output.xml`)**: Contains trip statistics such as duration, distance, and delays.
- **Graphical Analysis Outputs**: Visual representations of trajectories and movement patterns derived from simulation data.

## Building and Running

1. Extract OSM data and convert it into a SUMO network using `netconvert`.
2. Generate random routes using `randomtrips.py`.
3. Build the project with CMake:
   ```bash
   cmake --build build --target campus
