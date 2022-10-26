## Jenkins build "destiny_artifacts"

### Requirements

The jenkins server should have packer executable in PATH. Packer is the tool used to build the docker images, it's a standalone binary file. Download it from [Packer office website](https://www.packer.io/downloads.html).

Currently the build can only be done on a Linux Jenkins server. The jenkins server should have docker engine installed and the jenkins user should be allowed to call docker commands without `sudo` (this normally can be done by adding the jenkins user to docker group).

### Requirement

Jenkins server should have the pipeline related plugins installed. In addition, plugins list below should also be installed:

* Docker Pipeline
* Pipeline Utility Steps


### Parameters

* destiny_artifacts: (Required) The path to the destiny_artifacts folder on jenkins server.
* docker_image_tag: (Required) The tag to the images to be built.
* DOCKER_REGISTRY_URL: (Optional) The docker registry url to publish the images onto.
* DOCKER_REGISTRY_CREDENTIAL_ID: (Optional) The credential to the docker registry stored in the jenkins server.
