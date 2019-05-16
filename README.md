# Project Title
Testing usage of Planet API.

# Before you get started
- 

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

```


# Tests
- Tests performed on this project. What did you do? Which files were used? Was it successful?

# Contributors
- Daniel Corcoran

# Sources
- [Planet API Getting Started](https://developers.planet.com/docs/quickstart/getting-started/)