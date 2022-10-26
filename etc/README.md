## Jenkins build "destiny_artifacts"

The destiny_artifacts jenkinsfile is Jenkins pipeline file that builds a destiny_artifacts folder for the container build. It takes the destiny build artifacts zip path and oauth2 jwt plugin zip path as input and produces proper build artifacts to be used by container build.

### Requirement

Jenkins server should have the pipeline related plugins installed. In addition, plugins list below should also be installed:

* Pipeline Utility Steps
* Workspace Cleanup Plugin
* File Operations Plugin

### Parameters

* DESTINY_BUILD_ARTIFACTS_ZIP_FILE: (Required) Path to the destiny build zip.
* DESTINY_XLIB_ARTIFACTS_ZIP_FILE: (Required) Path to the destiny xlib zip.
* OAUTH2JWTSECRET_PLUGIN_ZIP:(Required) Path to the oauth2 zip.
* DestinyDockerBuildJob: (Optional) The docker build job in same jenkins server to trigger after this build is done.
