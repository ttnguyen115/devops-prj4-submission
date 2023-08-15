[![ttnguyen115](https://circleci.com/gh/ttnguyen115/devops-prj4-submission.svg?style=svg)](https://app.circleci.com/pipelines/github/ttnguyen115/devops-prj4-submission)

## Project Overview

In this project, you will apply the skills you have acquired in this course to operationalize a Machine Learning Microservice API. 

You are given a pre-trained, `sklearn` model that has been trained to predict housing prices in Boston according to several features, such as average rooms in a home and data about highway access, teacher-to-pupil ratios, and so on. You can read more about the data, which was initially taken from Kaggle, on [the data source site](https://www.kaggle.com/c/boston-housing). This project tests your ability to operationalize a Python flask app—in a provided file, `app.py`—that serves out predictions (inference) about housing prices through API calls. This project could be extended to any pre-trained machine learning model, such as those for image recognition and data labeling.

### Project Tasks

Your project goal is to operationalize this working, machine learning microservice using [kubernetes](https://kubernetes.io/), which is an open-source system for automating the management of containerized applications. In this project you will:
* Test your project code using linting
* Complete a Dockerfile to containerize this application
* Deploy your containerized application using Docker and make a prediction
* Improve the log statements in the source code for this application
* Configure Kubernetes and create a Kubernetes cluster
* Deploy a container using Kubernetes and make a prediction
* Upload a complete Github repo with CircleCI to indicate that your code has been tested

You can find a detailed [project rubric, here](https://review.udacity.com/#!/rubrics/2576/view).

**The final implementation of the project will showcase your abilities to operationalize production microservices.**

---

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

* Setup/Configure Docker locally
* Setup/Configure Kubernetes locally
```bash
    kubectl create secret docker-registry regcred \
        --docker-server=https://index.docker.io/v1/ \
        --docker-username=<DOCKERHUB_USERNAME> \
        --docker-password=<DOCKERHUB_PASSWORD> \
        --docker-email=<DOCKER_EMAIL>
  ```
* Create Flask app (making changes to app.py & build & push to dockerhub) in Container
* Run the pod using kubectl

* Here are some simple kubectl commands
```bash
    # See running pods
    kubectl get pods
    # View logs of a pod (when checking incoming request)
    kubectl logs <POD_NAME>
    # Port forward to forward a port in pod to host port (format: <HOST_PORT><POD_PORT>)
    kubectl port-forward <HOST_PORT><POD_PORT>
  ```

### Folder Structure
1. `.circleci/config.yml` : CircleCI configuration file.
2. `model_data` : Trained model data for housing prices in Boston.
3. `output_txt_files` : Docker and Kubernetes log output.
4. `app.py` : REST app for serving request making house price prediction.
5. `Dockerfile` : Dockerfile containing instructions to build image.
6. `make_prediction.sh` : Simulates API call to make prediction.
7. `Makefile` : Build file of the project.
8. `requirements.txt` : Python required libraries.
9. `run_docker.sh` : Shell script for creating and running docker container.
10. `run_kubernetes.sh` : Shell script to deploy docker container on Kubernetes cluster.
11. `upload_docker.sh` : Shell script for uploading locally built docker image to dockerhub repository.