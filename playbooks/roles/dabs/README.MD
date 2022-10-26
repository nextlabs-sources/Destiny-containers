# dabs

Role for handling dabs related configuration

## Notes

This role is meant to install dabs in a tomcat container. A entrypoint script will be put at /usr/local/bin/entrypoint. Pass `dabs` as first argument to the script to let the entrypoint configure the server properly using environment varibles. Environment variable list:

* SSL_PASSPHRASE (string): Password for Control Center's keystore and truststore
* DMS_HOST (string): DMS's DNS hostname
* DMS_PORT (number): (OPTIONAL) DMS's TCP port, if not specified, will use 8443
* EXTERNAL_HOST (string): External DNS name of the server, (for example, LB that route traffic of TCP port 8443 to this backend), if not set will use hostname

## Tunables

* artifacts_path (string): Path to artifacts

## Dependencies

* None

## Example Usage

* None

## Contributors

* Duan Shiqiang <shiqiang.duan@nextlabs.com>
