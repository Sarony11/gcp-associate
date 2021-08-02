### gcloud COMMAND --help
* Gives you help in how to use the command
* Syntax - `gcloud COMMAND --help`
  * COMMAND - config, list, set
* Some examples
  * `gcloud --help`
  * `gcloud list --help`
  * `gcloud config --help`

### gcloud init
* Inicializates the glcoud cli configuration
* Syntax - `gcloud init`
  * All this configuration is local and doesnt affect to other configurations.

### gcloud config list
* List the configuration of gcloud
* Syntax - `gcloud config list`

### gcloud config set
* Sets the specified property in your active configuration
* Syntax - `gcloud config set SECTION/PROPERTY VALUE`
  *  SECTION - core, compute
  *  PROPERTIES - project, region, zone
  *  Specifying core **is optional** as it is the default SECTION
*  Some examples
  * `gcloud config set core/project VALUE`
  * `gcloud config set compute/region VALUE`
  * `gcloud config set compute/zone VALUE` 

### gcloud config unset
* Unset an already configured property in your active configuration
* Syntax - `gcloud config unset SECTION/PROPERTY`
* Some examples
  * `gcloud config unset core/project`

### gcloud config configurations [create/delete/describe/activate/list]
* Allows you to work with multiple gcloud configurations, needed in case you are working in more than one project at once.
* Syntax - `gcloud config configurations ARGUMENT CONFIGURATION_NAME`
  * ARGUMENT - create, delete, describe, activate, list
  * CONFIGURATION_NAME - the name of the configuration you want to create, delete, describe or activate
* Some examples
  * `gcloud config configurations list` - List all the configurations
  * `gcloud config configurations create dev-configuration` - Creates and activates a configuration called dev-configuration
  * `gcloud config configurations activate prod-configuration` - Activates a configuration called prod-configuration
  * `gcloud config configurations activate prod-configuration` - Describe all the configuration of prod-configuration

## Section 6 - MIG
### gcloud compute instance-group managed list
* List all your instance-groups templates and their options
* Syntax - `gcloud compute instance-groups managed list`

### gcloud compute instance-group managed [create/update]
* Create or update an instance group with a new configuration
* Syntax - `gcloud compute instance-groups managed create MIG_NAME --template <template_name>
  * --zone
  * --size
  * --health-check
  * --initial-delay 
* examples
  * gcloud compute instance-groups managed create my-mig --zone us-central1-a --template my-instance-template --size 1 --health-check=my-health-check --initial-delay 300

### gcloud compute instance-group managed [delete/describe]
* Delete or describe the indicated MIG
* Syntax - `gcloud compute instance-groups managed delete/describe MIG_NAME`

### gcloud compute instance-group managed set-autoscaling
* Configure auto-scaling in a MIG
* Syntax - `gcloud compute instance-groups managed set-autoscaling MIG_NAME --max-num-replicas=<number>
  * --cool-down-period
  * --scale-based-on-cpu
    * --target-cpu-utilization
  * --scale-based-on-load-balacing
    * --target-load-balancing-utilization
  * --min-number-replicas
    * --mode (off/on/only-scale-out)
  * --max-number-replicas
* examples
  * gcloud compute instance-groups managed set-autoscaling MIG_NAME --max-num-replicas=10


### gcloud compute instance-group managed [resize]
* Update and resize a MIG
* Syntax - `gcloud compute instance-groups managed resize MIG_NAME --size=5`

### gcloud compute instance-group managed [recreate-instance]
* Recreates and already existing instance from a MIG. Used in case a very specific problem is happening and you need manual recreation without affecting the MIG
* Syntax - `gcloud compute instance-groups managed recreate-instance MIG_NAME --instances=<instance1_name>, <instance2_name>, etc`


### gcloud compute instance-group managed [update-instance]
* Updates an specific instance from a MIG without affecting the whole MIG
* Syntax - `gcloud compute instance-groups managed update-instance MIG_NAME --instances=<instance1_name>, <instance2_name>, etc`
  * --minimal-action=(none/refresh/replace/restart)
  * --most-disruptive-allowed-action=(none/refresh/replace/restart)

### gcloud compute instance-group managed [set-instance-template]
* Set the template of an specific instance from a MIG
* Syntax - `gcloud compute instance-groups managed set-instance-template MIG_NAME --template=v2-template`

### gcloud compute instance-group managed [rolling-action] [restart/replace/start-update]
* Set the template of an specific instance from a MIG
* Syntax - `gcloud compute instance-groups managed rolling-action [restart/replace/start-update] MIG_NAME ARGUMENT`
  * restart (start&stop) - reboot instances
    * --max-surge=number (2) or percentage (15%) (max number of instances updated at a time)
    * example - `gcloud compute instance-groups managed rolling-action restart my-mig --max-surge=3
  * replace (delete&recreate) - replace instancesç
    * Syntax - `gcloud compute instance-groups managed rolling-action replace MIG_NAME ARGUMENT`
    *  --max-surge=number (2) or percentage (15%) (max number of instances updated at a time)
    *  --max-unavailable=number (2) or percentage (15%)(max number of instances that can be down for the update)
    *  --replace-method=recreate/substitute (recreate creates instances with new names. Substitutes reuses names)
    * example - `gcloud compute instance-groups managed rolling-action restart my-mig --max-surge=3 --max-unavailable=10% --replace-method=substitute
  * start-update - updates instances to a new template
    * --version=template=<template_name>
    * --canary-version=<new_template_name>
      * --target-size=10%
    * example - `gcloud compute instance-groups managed rolling-action start-update --version=template=v1-template --canary-version=template=v2-template
