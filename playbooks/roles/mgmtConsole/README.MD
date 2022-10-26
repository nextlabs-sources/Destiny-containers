# mgmtConsole (administrator)

Role for handling administrator related configuration

## Notes

This role is meant to install administrator in a tomcat container. A entrypoint script will be put at /usr/local/bin/entrypoint. Pass `mgmtconsole` as first argument to the script to let the entrypoint configure the server properly using environment varibles. Environment variable list:

* SSL_PASSPHRASE (string): Password for Control Center's keystore and truststore
* DMS_HOST (string): DMS's DNS hostname
* DMS_PORT (number): (OPTIONAL) DMS's TCP port, if not specified, will use 8443
* CAS_AUTHENTICATION_SERVER_NAME (string): CAS Server's server.name value for CAS AuthenticationFilter, this is for redirect user to cas login page.
    For example: `https://example.com`
* CAS_TICKET_VALIDATION_SERVER_NAME (string): (OPTIONAL) CAS server's server.name value for CAS Validation Filter, this is for cas-client to validate ticket with cas server.
    For example: `http://internal.cas.example.com:8080` If not specified, will use value of CAS_AUTHENTICATION_SERVER_NAME.
* CAS_CLIENT_SERVER_NAME (string): CAS client's server.name value, this is for construct cas's so-call service name. Should use exposed DNS (i.e. LB's hostname)
    For exmaple: `https://application.example.com` If not specified, will use `http://${hostname}:8080`.
* EXTERNAL_HOST (string): External DNS name of the server, (for example, LB that route traffic of TCP port 8443 to this backend), if not set will use hostname

## Tunables

* artifacts_path (string): Path to artifacts

## Dependencies

* ansible-xml

## Example Usage

* None

## Contributors

* Duan Shiqiang <shiqiang.duan@nextlabs.com>
