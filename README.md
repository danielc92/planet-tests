# Project Title
Testing usage of Planet API.

# Before you get started
- Basic python knowledge
- Basic API knowledge
- Ubuntu OS

# Setup

Environment:
- Ubuntu 19.04 Operating System
- Python 2.7 virtual environment

Securing the api key:
```sh
nano ~/.bashrc
# Add this line
export PLANET_API_KEY="topsecretkey"
```

Accessing api key in python
```python
import os
API_KEY = os.getenv('PLANET_API_KEY')
```

Installing python bindings (required to install/build `jq`)
```sh
sudo apt-get install autoconf automake build-essential libtool python-dev
```

Setting up python environment
```sh
# Find the location of the python 2.7 bin (this outputs the path /usr/bin/python for me)
which python
# Create virtual environment with it
virtualenv --python=/usr/bin/python planet-env
# Activate the env
source planet-env/bin/activate
# Install requirements
pip install requests retrying jq
```

Installing npm and geojsonio-cli
```sh
sudo apt install npm
sudo npm install -g geojsonio-cli
```

# Process
1. Setup filters in `demo_filters.py`, providing an area of interest. Filters can filter by date range, cloud cover % and coordinates. Coordinates are listed in an array of 5 long/lats (making up a square box).
2. Use `search_endpoint.py` to locate individual ids based on filters set up previously.
3. Once individual ids are located, acquire asset types
```sh
# Getting asset types
# $PLANET_API_KEY is the name of the env variable storing our api key
curl -L -H "Authorization: api-key $PLANET_API_KEY" \
    'https://api.planet.com/data/v1/item-types/REOrthoTile/items/20160707_195147_1057916_RapidEye-1/assets' \
    | jq 'keys'
# Checking status of asset, if the status is inactive move to step 4
curl -L -H "Authorization: api-key $PLANET_API_KEY" \
    'https://api.planet.com/data/v1/item-types/REOrthoTile/items/20160707_195147_1057916_RapidEye-1/assets/' \
    | jq .visual.status
```
4. Activate asset type per given id using `activation.py`
5. This will generate a download url. Open url in browser or access with `curl` or `wget`.

# Tests
- Tests performed on this project. What did you do? Which files were used? Was it successful?

# Contributors
- Daniel Corcoran

# Sources
- [Planet API Getting Started](https://developers.planet.com/docs/quickstart/getting-started/)
-[Create coordinates for areas of interest in geojson format](http://geojson.io)
- [Planet developers guide - detecting ships using .tif as input in python](https://developers.planet.com/tutorials/detect-ships-in-planet-data/)