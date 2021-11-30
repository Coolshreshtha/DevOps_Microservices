
[![Coolshreshtha](https://circleci.com/gh/Coolshreshtha/DevOps_Microservices.svg?style=svg)](https://app.circleci.com/insights/github/Coolshreshtha/DevOps_Microservices)

#Operationalizing a DevOps_Microservices
## Project Overview

In this project, we operationalize a Machine Learning Microservice API using a pre-trained, `sklearn` model that has been trained to predict housing prices in Boston according to several features, such as average rooms in a home and data about highway access, teacher-to-pupil ratios, and so on. You can read more about the data, which was initially taken from Kaggle, on [the data source site](https://www.kaggle.com/c/boston-housing). 
This project uses a Python flask app—in a provided file, `app.py`—that serves out predictions (inference) about housing prices through API calls. This project could be extended to any pre-trained machine learning model, such as those for image recognition and data labeling.

## Files included
- requirements.txt : a list of all the required packages to be downloaded for the project
- app.py : source code for the prediction application 
- Makefile : a script to setup environment, and built, test and lint the project
- Dockerfile : blueprint for the docker image for our project
- model_data/* : Data to process for predictions. The two files are as follows:
    - boston_housing_prediction.joblib 
    - model_data/housing.csv
- .circleci/config.yml : a YAML script for running the CircleCI pipeline which includes a build job with multiple setup steps.
- run_docker.sh : a shell script to build a docker image with a tag, list out all docker images and start the flask app
- run_kubernetes.sh : a shell script to start a kubernetes cluster based on a docker image created earlier and forward the container to a host
- upload_docker.sh: a shell script to push a docker image to docker repository after authenticating and tagging it
- output_txt_files/* : These files contain the output on running our prediction app. Contains the following files:
    - docker_out.txt : Output for running ./run_docker.sh and ./make_prediction.sh
    - kubernetes_out.txt : Output for running ./make_prediction.sh after setting up the kubernetes cluster

## Setup the Environment

* Create a virtualenv with Python 3.7 and activate it. Refer to this link for help on specifying the Python version in the virtualenv. 
```bash
python3 -m pip install --user virtualenv
# You should have Python 3.7 available in your host. 
# Check the Python path using `which python3`
# Use a command similar to this one:
python3 -m virtualenv --python=<path-to-Python3.7> .devops
source .devops/bin/activate
```
* Run `make install` to install the necessary dependencies

### Running `app.py`

1. Standalone:  `python app.py`
2. Run in Docker:  `./run_docker.sh`
3. Run in Kubernetes:  `./run_kubernetes.sh`

### Kubernetes Steps

* Setup and Configure Docker locally
* Setup and Configure Kubernetes locally
* Create Flask app in Container
* Run via kubectl
