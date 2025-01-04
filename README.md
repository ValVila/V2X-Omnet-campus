# V2X-Omnet-Campus

This project is part of a thesis focusing on GNSS vs. GPS V2X communication within a campus environment. It integrates OpenStreetMap data, SUMO (Simulation of Urban MObility), and OMNeT++ to simulate vehicular and pedestrian movements, evaluate trajectory data, and analyze communication scenarios.

## Folder Structure

- **track mapping**: Contains coordinate data from a walk, mapped onto a graphical map. This serves as a real life baseline to simulate GNSS vs. GPS coordinates.
- **routes testings**: Includes `.rou` files generated for testing various routing scenarios in the simulation.
- **Graphs**: Contains extracted coordinates from vehicle routes, plotted as graphs for trajectory evaluation and movement pattern analysis.
- **results**: Stores outputs generated during simulations, including files for analyzing trajectories, trip information, and Floating Car Data (FCD). This folder is essential for post-simulation analysis and visualization.

## Key Files

- `campus.sumocfg`: Configuration file for running the SUMO simulation. It defines simulation parameters, input files, and additional settings.
- `campus.rou.xml`: Defines pre-determined routes for vehicles in the simulation.
- `map1.osm.xml`: OpenStreetMap (OSM) data of the campus, used to generate the road network.
- `campus.net.xml`: Network file generated from the OSM data using `netconvert`.
- `Traci Script for Positional noise.ipynb`: Jupyter Notebook that uses TraCI (Traffic Control Interface) to introduce positional noise for trajectory testing.
- `positional deviation and trajectory calculation.ipynb`: Notebook for analyzing positional deviations and evaluating calculated trajectories.
- `randomTrips.py`: SUMO script for generating random trips based on the campus network. Used to create realistic `.rou` files for testing.

## Workflow Overview

1. **Generate Network**:
   - Use OpenStreetMap (OSM) data (`map1.osm.xml`) and convert it into a SUMO network (`campus.net.xml`) using the `netconvert` tool:
     ```bash
     netconvert --osm-files map1.osm.xml -o campus.net.xml
     ```

2. **Generate Routes**:
   - Use the `randomTrips.py` script to generate random routes for the vehicles based on the network:
     ```bash
     python randomTrips.py -n campus.net.xml -o campus.rou.xml
     ```

3. **Configure SUMO Simulation**:
   - Define the simulation parameters in `campus.sumocfg`, specifying the network file, route file, and other necessary additions and configurations.

4. **Integrate with OMNeT++**:
   - Ensure OMNeT++ is installed and properly configured.
   - Use CMake to build the project:
     ```bash
     cmake --build build --target campus
     ```
   - Configure the `omnetpp.ini` file to set up the simulation environment, including paths to the SUMO configuration and network files.

5. **Run Simulation**:
   - Execute the simulation through OMNeT++, which will interface with SUMO to simulate the defined scenarios.

6. **Analyze Results**:
   - The `results` folder contains output files for trajectory analysis and visualizations.
   - Use Jupyter Notebooks, such as `positional deviation and trajectory calculation.ipynb`, for detailed evaluation.

## Software and Tools

- **OMNeT++**: A discrete-event network simulator used for the simulation framework.
- **SUMO**: A traffic simulation tool used for defining and managing vehicle movements.
- **TraCI**: A Python interface for controlling and extracting data from SUMO simulations.
- **netconvert**: Converts OSM files into SUMO-readable network files.
- **randomTrips.py**: SUMO script for generating random routes in the network.

## Prerequisites

- **OMNeT++**: Ensure OMNeT++ is installed on your system. [Installation Guide](https://omnetpp.org/)
- **SUMO**: Install SUMO for traffic simulation. [Installation Guide](https://sumo.dlr.de/docs/Installing.html)
- **Veins Framework**: Install Veins for vehicular network simulations. [Veins GitHub Repository](https://github.com/sommer/veins)
- **INET Framework**: Install INET for internet protocol simulations. [INET GitHub Repository](https://github.com/inet-framework/inet)

## Building and Running

1. **Set Up the Environment**:
   - Clone this repository:
     ```bash
     git clone https://github.com/ValVila/V2X-Omnet-campus.git
     ```
   - Navigate to the project directory:
     ```bash
     cd V2X-Omnet-campus
     ```

2. **Build the Project**:
   - Create a build directory and navigate into it:
     ```bash
     mkdir build
     cd build
     ```
   - Run CMake to configure the project:
     ```bash
     cmake ..
     ```
   - Build the project using CMake:
     ```bash
     cmake --build build --target campus
     ```

3. **Analyze the Results**:
   - After the simulation completes, the files in the `results` directory correspond to the logs and 'fcd_output.xml' and 'tripinfo_output.xml' for the floating car data and trip data so you can analyze the output using the provided Jupyter Notebooks under python notebook scripts.
