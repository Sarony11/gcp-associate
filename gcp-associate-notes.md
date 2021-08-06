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

# Section 6 - Group Instances
* A managed Instance Group is a group of VMs created using the same instance template.
  * **Health checks**: Detect applicatiosn failures and if an instance crashes, it lunches another instance.
  * **Autoscaling**: Increase and drecrease horizontally based on load.
  * **Load Balacer**: Distribute load among the different instances.
  * **Regional**: Create instances in multiple zones in the same region, giving higher availability.
  * **Realises**: Release new versions without downtime.
    * Rolling updates: Release new versions gradually, once instance at a time.
    * Canary deployment (A/B): Test new version with a group of instances before releasing across all the instances.

## Creating an instance group
https://www.youtube.com/watch?v=AXbuyAnGkiQ
* Instance group is mandatory
* Configure auto-scaling to automatically adjust number of instances based on load
  * Minimum number of instances.
  * Maximum number of instances.
  * Autoscaling metris: How do you want the scale happens (CPU, Load Balacing or any other metric) using StackDriver.
    * Cool-down period: How long to wait before looking at auto scaling metrics again?
    * Scale in controls: Scale down slowly to prevent sudden drop.
   * Autohealing: Configure health check with initial delay (how long show you wait for you app until first health check?)

## Updating a Managed Instance Group
* Update strategy
  * Rolling update - Gradual update instance by instance with the new template.
  * Canary A/B:
* Other options
  * When should the update happen? - Proactive (start now) or Opportunistic (when MIG resizes later)
  * How should the update happen? - 
    * Maximum surge: How many instances are added at a time?
    * Maximum unavailable: How many instances can be offline during update?
 * **Rolling Restart/replace:** Gradual restart or replace of instaces in the group
   * **No changes** in the template **BUT replace/restart** existing VMs
   * You can configure options like maximum unavailability, surge, etc

## MIG Scenarios
You application to survive Zonal Failures <- Create multiple zone MIG
You want to preserve VM state in the group <- Configure Stateful MIG. Recomended for statful workloads (database, dataprocessing apps)
You want a group of apps with high availability even when hardware/software updates <- Use instance template and enable automatic restart policy and migrate on-host maintenance. These options ensures live migration and automatic restarts.
You want unhealthy instances to be automatically replaced <- Configure health check on the MIG
You want to avoid scale problems in a group of apps <- Configure cool-down period/initial delay

# Section 7 - Cloud Balancing
* Distributes traffic across instances of an application in single region or multiple regions
* Fully distributed, software defined managed service
* Importante featured
  * Health check - Route to healthy instances
  * Auto scaling
  * Global load balacing with single anycast IP
  * Also supports internal load balancing
* When to use it?
  * High availability
  * Auto scaling
  * Resiliency

## Understanding HTTP, HTTPS, UDP and TCP
* Layer 3 (Network)     -> IP
* Layer 4 (Transport)   -> TCP, TLS UDP
* Layer 7 (Application) -> HTTP, HTTPS, SMTP

* Network layer: IP (Internet Protocol): Transfer bytes. Unrealiable.
* Transport Layer:
  * TCP (Transmission Control): Reliability over performance.
  * TLS (Transport Layer Security): Secure TCP. Reliability and security over performance.
  * UDP (User Datagram Protocol): Performance over reliability.
* Application Layer:
  * HTTP (Hypertext Transfer Protocol): Stateless request response cycle.
  * HTTPS (Secure HTTP)
  * SMTP, FTP, SSH, etc.

Most applications typically communicate at application layer
* Web apps/REST API (HTTP/HTTPS), Email Server (SMTP), File Transfers (FTP)
* All these applications use TCP/TLS at network layer

However other applications need high performance, and they communicate directly in network layer.
* Gamming applications, live video streaming use UDP.
