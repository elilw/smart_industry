# Solar Visualisation Simulator
___

This project aim to provide a simulation of a visualization system fo a solar grid.
The system is divided in 3 docker containers:
- **grafana**
- **influxdb**
- **postgresql_db**

And the `main.py` to simulate the data source.


## Installation

To run the containers, an installation of docker is required to proceed.

Linux (or WSL) users might install Docker Engine and Docker Compose.
It is recommended to follow https://docs.docker.com/engine/install/linux-postinstall, and add the desired local user to the `docker` group.

Otherwise, in Windows and macOS, users can install Docker Desktop to manage the containers with a GUI.
For more details user should follow the official instructions at https://docs.docker.com/get-docker/

Make sure to create a network in which the containers will communicate with:
```sh
docker network create <network_in_compose>
```

To run `main.py` users are encouraged to create a python virtual environment. 
```sh
python -m venv solar_venv
source solar_venv/bin/activate
pip install -r requirements.txt
# pip install pvlib influxdb-client NREL-PySAM
```
Optionally, users may elect to run the code in an additional container.


## Running

In `deployment/`:

```sh
docker compose up
python ../main.py
```

You may then proceed to configure the services.

For more info on Grafana, see https://grafana.com/docs/grafana/latest/.

For more info on InfluxDB, see https://docs.influxdata.com/influxdb/v2/.

___
### Roadmap

-[x] Initialize repository.
-[x] Write `README.md`.
-[x] Download weather data.
    - https://analisi.transparenciacatalunya.cat/Medi-Ambient/Dades-meteorol-giques-de-la-XEMA/nzvn-apee/about_data
-[ ] Preprocess the data from `WeatherData/Data/Dades_meteorol_giques_de_la_XEMA_20240403.csv` into a more usable format.
    -[ ] Currently, every type of measure has its own tuple. Join them into a single tuple.

-[ ] Finish `docker_compose.yml` configuration.
-[ ] Finish TODOs in `main.py` and `data_preprocessing.py`.


-[ ] OPTION 1 - Add prediction to the visualization.
    -[ ] Must include confidence intervals (or equivalent).
    -[ ] You can use any kind of Machine Learning to create the predictions.
-[ ] OPTION 2 - Create a new docker to execute `main.py`, and monitor resource usage.
    - https://docs.docker.com/language/python/containerize/
    - https://docs.docker.com/config/containers/runmetrics/
-[ ] OPTION 3 - Replace simulation of real time data, with queries to AccuWeather roughly every 5 min.
    - This page indicates how the queries should be structured: https://developer.accuweather.com/api-flow-diagram

