# dpc

Role for handling dpc related configuration

## Notes

This role is meant to install dpc in a tomcat container. A entrypoint script will be put at /usr/local/bin/entrypoint. Pass `dpc` as first argument to the script to let the entrypoint configure policy controller properly using environment varibles. Environment DABS_HOST is used to configure ICENET server host.

## Tunables

* catalina_home (string): (OPTIONAL) tomcat home, if not defined will try to resolve from environment variable CATALINA_HOME
* artifacts_path (string): Path to artifacts

## Dependencies

* tomcat-common

## Example Usage

* None

## Contributors

* Duan Shiqiang <shiqiang.duan@nextlabs.com>
