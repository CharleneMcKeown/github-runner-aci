# github-runner-aci

This repository contains the basics for registering a self hosted runner for use with GitHub Actions, hosted on Azure Container instances. It contains: 

1. A Dockerfile. It is configured to pull a Ubuntu base image, and installs some common tools. 
1. A shell script that will run when the Docker container starts, to register a new agent with GitHub. 
1. A pipeline that will build and push the image to a container registry when the Dockerfile is updated, then deploy an Azure Container Instance to pull and run the container image.

To use this in your own GitHub repo, you will need to create 5 secrets:

ACR_SERVER - e.g. myacr.azurecr.io
ACR_USER - e.g. myacr
ACR_PASSWORD - access key from your ACR
AZURE_CREDENTIALS - this is the JSON output of running `az ad sp create-for-rbac`
GIT_PAT - a GitHub personal Access token

Additionally, the runner is registered to the repository using the env variable RUNNER_REPOSITORY_URL. Update this to your URL in the pipeline env variables -e.g. https://github.com/yourhandle/yourrepo

I haven't tried it, but you can also register runners to organisations and enterprises by using other variables. Please refer to the below repo, which I used to create this content:

https://github.com/peter-murray/github-actions-runner-container


