# Spring PetClinic with Datadog Integration
This repo uses the Spring-Petclinic application from the Spring community and instruments it for use in the Datadog Continuous Profiler. Datadog's Continuous Profiler provides software engineers, architects, and application operators with insight into an application's performance and shows reached vulnerabilities.

## Spring Petclinic deployed to Google Cloud using Kubernetes
This version of Spring Petclinic deploys to Kubernetes. The pipelines leverage GCP to create a Kubernetes cluster. See the pipeline's section below for details on each pipeline. This application can deploy to a local version of Kubernetes but will need some Ingress point.

## DataDog

## Pipeline
A detailed list of each pipeline with description, requirements, and how to trigger the pipeline

### Build and Push Image
The pipeline builds the SPC artifact, the container image, and pushes the Image to Docker Hub. The pipeline defines the container image registry and repo in the pipeline. 

**Trigger:** On Push or PR based on directory

**Required Secrets:** 
Docker_Key - Docker API Key
