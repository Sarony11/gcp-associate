# Section 1 - Introduction
## Cloud Advantages
* Variable vs fixed expense
* Stop guessing capacity thanks to elasticity
* Benefit from massive economies of scale
* Stop sependding money running and mantaining data centers
* Go global in minutes


# Section 5 - GCloud CLI
* Command line interface to interact with GCP resources.
  * Compute Engine
  * Managed Instace Groups
  * Databases
  * And many more
* Create/delete/update/read existing resources and perform actions like deployments as well.
* **IMPORTANT**: Some GCP resources have specific CLI tools:
* Other CLI applications
  * Cloud Storage - gsutil
  * Cloud BigQuery - bq
  * Cloud Bigtable -cbt
  * Kubernetes - kubectl
## Instalation and use of Gcloud CLI
GCloud is part of Google Cloud SDK
Cloud SDK requires Python
Instructions to install Cloud SDK -> https://cloud.google.com/sdk/docs/install
You can also use Gcloud on Cloud Shell
## Initialize Gcloud CLI
Cheatsheet -> https://gist.github.com/pydevops/cffbd3c694d599c6ca18342d3625af97
`$ gcloud init`
* Create new configuration
* Create configuration name
* Choose account to authenticate
* Pick project to use
* Configure default Region and Zone
* **All this configuration is local** and doesnt affect to other configurations.
`$ gcloud config list`
List all the configuration in your gcloud CLI

