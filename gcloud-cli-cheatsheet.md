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

## MIG
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
