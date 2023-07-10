# Braess-Paradox-Framework

This repository contains the code of the framework to simulate the effect of the Braess Paradox on CO2 emissions in urban areas. The framework models the traffic flows from real data and simulates the traffic using SUMO (Simulation of Urban MObility). It is possible to simulate the traffic in different cities and different scenarios. Particulary, the framework can be used to simulate different closure road strategies within the city and analyze the effect on CO2 emissions of these strategies. It can also be used as a detector of the Braess Paradox in urban areas.

## Built with

![python](https://img.shields.io/badge/Python-3776AB.svg?style=for-the-badge&logo=Python&logoColor=white)
![jupyter](https://img.shields.io/badge/Jupyter-F37626.svg?style=for-the-badge&logo=Jupyter&logoColor=white)
![numpy](https://img.shields.io/badge/NumPy-013243.svg?style=for-the-badge&logo=NumPy&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-150458.svg?style=for-the-badge&logo=pandas&logoColor=white)
![osm](https://img.shields.io/badge/OpenStreetMap-7EBC6F.svg?style=for-the-badge&logo=OpenStreetMap&logoColor=white)
![folium](https://img.shields.io/badge/Folium-77B829.svg?style=for-the-badge&logo=Folium&logoColor=white)

## Repository structure

The repository is divided in the following folders:

1. `src` - contains all the notebooks and the code.
    1. `0_prepare_Milan_GPS_dataset.ipynb` - notebook with the code to preprocess GPS data from Milan.
    2. `1_create_od_matrix.ipynb` - notebook to generate the Origin-Destination matrix from GPS data.
    3. `2_create_mobility_demand.ipynb` - notebook to generate the mobility demand from the OD matrix.
    4. `3_create_routed_paths_duarouter.ipynb` - notebook to the routed paths from the mobility demand using Duarouter.
    5. `4a_experiments.ipynb` - notebook to simulate the vehicular traffic in SUMO.
    6. `4b_results_and_road_aggregation.ipynb` - notebook to resume the results obtained from the simulation and aggregate the edges of the road network.
    7. `5a_remove_road_experiments.ipynb` - notebook to run the entire framework from the beginning and simulate the vehicular traffic in SUMO after removing some roads.
    8. `5b_results_remove_experiments.ipynb` - notebook to resume the results obtained from the simulation after removing some roads and compare the results with the baseline experiment.
    9. `6_all_experiment_results.ipynb` - notebook to aggregate the results obtained from different closure strategies.
    10. `7a_k_road_plots.ipynb` - notebook to compute the K_road, the K_source and the betweenness centrality for the road in the road network.
    11. `7b_k_road_clustering.ipynb` - notebook to classify the road of the road network in different categories using clustering technique on the K_road, the Volume-Over-Capacity and the betweenness centrality.
    12. `7c_remove_k_road_.ipynb` - notebook to remove the road in the road netwrok based on the road classification.
    13. `7d_remove_k_road_experiments.ipynb` - notebook to run the entire framework from the beginning and simulate the vehicular traffic in SUMO after removing the road based on the road classification.
    ____
    14. `plot_utils.py` - python utility functions for generating the figures.
    15. `result_utils.py` - python utility functions for computing the results.
    16. `utils.py` - python utility functions for the framework.

2. `data` - contains the data used in the framework.
    1. `road_net` - contains the road networks used in SUMO from OSM.
    2. `shapes` - contains the geojson shape of the city used in the framework.
    3. `mobility_data` - contains the mobility demand generated from each experiment.
    4. `OD_matrices` - contains the OD matrices generated from the real data.
3. `sumo_simulation_scripts` - contains the code to make experiments in SUMO from [traffiCO2](https://github.com/GiulianoCornacchia/traffiCO2)

## Getting started

### Setup SUMO

Please always refer to the [SUMO Installation page](https://sumo.dlr.de/docs/Installing/index.html)
for the latest installation instructions.

#### > Windows

To install SUMO on Windows it is necessary to download the installer [here](https://sumo.dlr.de/docs/Downloads.php#windows) and run the executable.

#### > Linux

To install SUMO on Linux is it necessary to execute the following commands:

```
sudo add-apt-repository ppa:sumo/stable
sudo apt-get update
sudo apt-get install sumo sumo-tools sumo-doc
```

#### > macOS

SUMO can be installed on macOS via [Homebrew](https://brew.sh/).

You can install and update Homebrew as following:

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
brew update
brew install --cask xquartz
```
To install SUMO:
```
brew tap dlr-ts/sumo
brew install sumo
```

### Configure SUMO

After installing SUMO you must configure your `PATH` and `SUMO_HOME` environment variables.

Suppose you installed SUMO at `/your/path/to/sumo-<version>`

#### > Windows

1. On the Windows search box search for "Edit the system environment variables" option and open it;
2. Under user variables select `PATH` and click Edit. If no such variable exists you must create it with the New-Button;
3. Append `;/your/path/to/sumo-<version>/bin` to the end of the `PATH` value (do not delete the existing values);
4. Under user variables select `SUMO_HOME` and click Edit. If no such variable exists you must create it with the New-Button;
5. Set `/your/path/to/sumo-<version>` as the value of the `SUMO_HOME` variable.

#### > Linux

1. Open a file explorer and go to `/home/YOUR_NAME/`;
2. Open the file named `.bashrc` with a text editor;
3. Place this code export `SUMO_HOME="/your/path/to/sumo-<version>/"` somewhere in the file and save;
4. Reboot your computer.

#### > macOS

First you need to determine which shell (bash or zsh) you are currently working with. In a terminal, `type ps -p $$`.

##### ZSH

In a Terminal, execute the following steps:

1. Run the command `open ~/.zshrc`, this will open the `.zshrc` file in TextEdit;
2. Add the following line to that document: `export SUMO_HOME="/your/path/to/sumo-<version>"` and save it;
3. Apply the changes by entering: `source ~/.zshrc`.

##### bash

In a Terminal, execute the following steps:

1. Run the command `open ~/.bash_profile`, this will open the `.bash_profile` file in TextEdit;
2. Add the following line to that document: `export SUMO_HOME="/your/path/to/sumo-<version>"` and save it;
3. Apply the changes by entering: `source ~/.bash_profile`.

### The framework

To execute the framework you must follow the following steps:

1. Clone the repository.:
    ```
    git clone https://github.com/Simoniuss/Braess-Paradox-Framework.git
    ```
2. Install the conda environment:
    ```
    conda env create -f environment.yml
    ```
3. Activate the conda environment:
    ```
    conda activate braess
    ```
