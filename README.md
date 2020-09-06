--Project 5 - Cloud DevOps Engineer Capstone Project

In this project, I have applied my learning and skills which was developed throughout the Cloud DevOps Nanodegree program.

-- Project Tasks:
* Working in AWS
* Using Jenkins to implement Continuous Integration and Continuous Deployment
* Building pipelines
* Working with CloudFormation to deploy clusters
* Building Kubernetes clusters
* Building Docker containers in pipelines

-- About Project: 
**Have created a CI/CD pipeline for a basic website that deploys to a cluster in AWS EKS which is Blue/Green Deployment.

To meet the Project Requirement first have installed below mention Pre-requisite to use CI/CD pipeline:
========================================================================================================
* Jenkins
* Blue Ocean Plugin in Jenkins
* Pipeline-AWS Plugin in Jenkins
* Docker
* Pip
* AWS Cli
* Eksctl
* Kubectl

High Level Project Flow :
==========================

Pipeline 1: Create the Cluster
*********************************
step 1: Authenticate into AWS 
step 2:Create Kubernetes Cluster
step 3: Create a configuration file for Kubectl 


Pipeline 2: Deploy the Container: Build and Deploy The Docker Image, Create container and expose them then redirect trafiic from Blue to Green
****************************************
Step 1:  Linting
Step 2: Build the Docker image
Step 3: Upload the Docker image
step 4: Set current kubectl context to cluster
step 5 : Create blue replication controller with it's docker image 
step 6 : Create Green replication controller with it's docker image 
step 7: Create service in Kubernetes cluster in charge of routing traffic to blue replication controller and exposing it to outside world, by setting the
selector to App = Blue
step 8 : Wait unti the user give the instructor to proceed further
step 9 : Update the service to re-direct to green by changing the selector app = green.


Project Files :
====================

1. /Create-clusters-pipeline : CloudFormation Script of Cluster Pipeline file .

2. /Deploy-containers-pipeline : Deployment Script of Containers Pipeline file. File details are mention below :-
-- Jenkinsfile : Jenkinsfile for Creating Pipeline
-- Dockerfile : Dockerfile for building the image 
-- green-controller.json : Create a replication controller green pod
-- green-service.json : Create the green service
-- blue-controller.json : Create a replication controller blue pod
-- blue-service.json : Create the blue service
-- index.html : Web site Index file.


**Project Screenshots are captured in Project5_screenshots.docx.

GIT HUB LInk : https://github.com/anuguptaudacity/udacitycapstone



