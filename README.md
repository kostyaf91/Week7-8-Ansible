# CI/CD with Azure DevOps & Dockers
### This project is part of the DevOps Bootcamp by Sela.

## In this project I'm creating CI/CD pipeline for our bootcamp app - Node Weight Tracker

### To this project I need some prerequisites:
1. My terraform template that creates 2 identical environments : [Week 6 - IaC](https://github.com/kostyaf91/terraform_azure)
2. Our bootcamp app - Node Weight Tracker: [Node Weight Tracker](https://github.com/kostyaf91/bootcamp-app)

### Every environment looks:
* One vnet.
* Two subnets - one public and one private, with some security.
* VM linux scale set, with auto-scaling setting.
* Public load balancer that speaks with the scale set.
* Managed postgres that speaks only to the scale set.


At this project I'm creating new pipeline, importing the project from GitHub to Azure Repositories.
And then creating Image with docker that pushed to ACR - Azure Container Registry.

Also, there is an implementation of 'feature branch workflow' by adding branch policy fot the master branch.

## CI

When there is any change in the feature branch the CI process builds a Docker Image.

Only when a feature branch integrated to the master branch the CI process get back into action and in addition to building a new image pushes the image to the Azure Container Registry.

## CD

The continuous deployment and continuous delivery pipelines are similar except that the continuous delivery requires manual approval.

To make the continuous delivery pipline wait for approval I chose the environment I want and then `Approvals and checks > Add check > Approvals`.

To manage the dockers I've used ansible that pull the latest image from the Azure Container Registry and deploys it to the vms.
