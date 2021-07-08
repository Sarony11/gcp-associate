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
