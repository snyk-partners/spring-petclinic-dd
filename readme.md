# Spring PetClinic with Datadog Integration
This repo uses the Spring-Petclinic application from the Spring community and instruments it for use in the Datadog Continuous Profiler. Datadog's Continuous Profiler provides software engineers, architects, and application operators with insight into an application's performance and shows reached vulnerabilities.

## Spring Petclinic deployed to Google Cloud using Kubernetes
This version of Spring Petclinic deploys to Kubernetes. The pipelines leverage GCP to create a Kubernetes cluster. See the pipeline's section below for details on each pipeline. This application can deploy to a local version of Kubernetes but will need some Ingress point.

## DataDog

## Pipeline
A detailed list of each pipeline with description, requirements, and how to trigger the pipeline

### Build and Push Image
The pipeline builds the SPC artifact, the container image, and pushes the Image to Docker Hub. The pipeline defines the container image registry and repo in the pipeline. 

**Trigger:** On Push or PR based on directory. \
Ignored directories \
 kubernetes/** \
 .github/workflows/** \
 datadog/** 

**Required Secrets:** 
Docker_Key - Docker API Key

### GCP Setup
This pipeline creates a K8s cluster on GCP. It requires a service account and key with K8s admin credentials.

**Trigger:** Manual from GH Actions Tab

**Requirements:**
GCP Service Account with K8s admin privileges

**Required Secrets:**
Google_Application_Credentials - Service Account Key \
Project_ID - GCP Project Id \
GKE_Cluster_Name - Name of K8s cluster \

### Install Datadog Agent
This pipeline installs the Datadog agent using Helm to your K8s cluster. It needs your Datadog API Key and Datadog App Key from the Datadog UI.

**Trigger:** Manual from GH Action Tab

**Required Secrets:**
Datadog_API_Key \
Datadog_App_Key \

### Upload Datadog Data
This pipeline uses the Snyk CLI to generate a dependency graph used by the Datadog solution to map vulnerabilities to the application at deployment.

**Trigger:** Manual from GH Actions Tab

**Requirements:**
Snyk Account - Free \
Datadog Account - Free \

**Required Secrets:**
Datadog_API_Key \
Datadog_App_Key \
Snyk_API_Token \

### Deploy-App-K8s
This pipeline deploys the SPC application to your K8s cluster. It creates a load balancer on GCP.

**Required Secrets:**
GKE_Cluster_Name

**Trigger:** Manual from GH Actions Tab

**Required Secrets:**
GKE_Cluster_Name \

