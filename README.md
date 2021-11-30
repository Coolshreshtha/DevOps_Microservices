
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

## Running the project

### Setting up the environment

* Create a virtualenv with Python 3.7 and activate it. Refer to this link for help on specifying the Python version in the virtualenv. 
```bash
python3 -m pip install --user virtualenv
python3 -m virtualenv --python=<path-to-Python3.7> .devops
source .devops/bin/activate
```
* Run `make install` to install the necessary dependencies
* Ensure docker, minikube, hadolint and kubectl are installed. If not installed, run these commands
```bash
#Hadolint install linux 
sudo wget -O /bin/hadolint https://github.com/hadolint/hadolint/releases/download/v1.16.3/hadolint-Linux-x86_64
sudo chmod +x /bin/hadolint

#Virtual box
wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] http://download.virtualbox.org/virtualbox/debian $(lsb_release -cs) contrib"
sudo apt update && sudo apt install virtualbox-6.0

#Minikube
wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo cp minikube-linux-amd64 /usr/local/bin/minikube
sudo chmod 755 /usr/local/bin/minikube

#Kubectl
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
```

### Running `app.py`

1. Standalone:  `python app.py`
2. Run in Docker:  `./run_docker.sh` and `./make_prediction.sh` in a different terminal
3. Run in Kubernetes:  
    - Setup kubernetes as outlined in the next section
    - Run `minikube start` and then `./run_kubernetes.sh` to start a kubernetes cluster
    - run `./make_prediction` in a different terminal

### Kubernetes Setup

* Setup and Configure Docker locally
* Setup and Configure Kubernetes locally
* Create Flask app in Container
* Run via kubectl
