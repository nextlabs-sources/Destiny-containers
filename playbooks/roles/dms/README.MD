# dms

Role for handling dms related configuration

## Notes

This role is meant to install dms in a tomcat container. A entrypoint script will be put at /usr/local/bin/entrypoint. Pass `dms` as first argument to the script to let the entrypoint configure the server properly using environment varibles. Environment variable list:

* SSL_PASSPHRASE (string): Password for Control Center's keystore and truststore
* DATABASE_USERNAME (string): Database username
* DATABASE_PASSWORD (string): Database encrypted password
* DATABASE_CONNECTSTRING (string): Database connect string
* EXTERNAL_HOST (string): External DNS name of the server, (for example, LB that route traffic of TCP port 8443 to this backend), if not set will use hostname

## Tunables

* artifacts_path (string): Path to artifacts

## Dependencies

* None

## Example Usage

```bash
# For using postgres
docker run -it -e 'SSL_PASSPHRASE=123next!' \
    -e DATABASE_USERNAME=clarion \
    -e 'DATABASE_PASSWORD=123next!' \
    -e DATABASE_CONNECTSTRING=postgresql://pf-linux01.qapf1.qalab01.nextlabs.com:5432/clarion \
    <image_name>
# For using oracle
docker run -it -e 'SSL_PASSPHRASE=123next!' \
    -e DATABASE_USERNAME=clarion \
    -e 'DATABASE_PASSWORD=123next!' \
    -e DATABASE_CONNECTSTRING=oracle:thin:@ccsgdcora12c.qapf1.qalab01.nextlabs.com:1521:orcl \
    <image_name>
# For using mssql
docker run -it -e 'SSL_PASSPHRASE=123next!' \
    -e DATABASE_USERNAME=clarion \
    -e 'DATABASE_PASSWORD=123next!' \
    -e DATABASE_CONNECTSTRING=sqlserver://ccsgdcsql2012.qapf1.qalab01.nextlabs.com:1433;DatabaseName=clarion; \
    <image_name>
```

## Contributors

* Duan Shiqiang <shiqiang.duan@nextlabs.com>
