# cas server

Role for handling cas related configuration

## Notes

This role is meant to install cas in a tomcat container. A entrypoint script will be put at /usr/local/bin/entrypoint. Pass `cas` as first argument to the script to let the entrypoint configure the server properly using environment varibles. Environment variable list:

* CAS_SERVER_NAME (string): DNS hostname of CAS Server exposed to outside, cas's `server.name` will be set to https://{CAS_SERVER_NAME}:443
* DATABASE_USERNAME (string): Database username
* DATABASE_PASSWORD (string): Database password
* DATABASE_CONNECTSTRING (string): Database connect string

## Tunables

* artifacts_path (string): Path to artifacts

## Dependencies

* tomcat-common

## Example Usage

```bash
# For using postgres
docker run -it -e CAS_SERVER_NAME=<external DNS> \
    -e DATABASE_USERNAME=clarion \
    -e 'DATABASE_PASSWORD=123next!' \
    -e DATABASE_CONNECTSTRING=postgresql://pf-linux01.qapf1.qalab01.nextlabs.com:5432/clarion \
    <image_name>
# For using oracle
docker run -it -e CAS_SERVER_NAME=<external DNS> \
    -e DATABASE_USERNAME=clarion \
    -e 'DATABASE_PASSWORD=123next!' \
    -e DATABASE_CONNECTSTRING=oracle:thin:@ccsgdcora12c.qapf1.qalab01.nextlabs.com:1521:orcl \
    <image_name>
# For using mssql
docker run -it -e CAS_SERVER_NAME=<external DNS> \
    -e DATABASE_USERNAME=clarion \
    -e 'DATABASE_PASSWORD=123next!' \
    -e DATABASE_CONNECTSTRING=sqlserver://ccsgdcsql2012.qapf1.qalab01.nextlabs.com:1433;DatabaseName=clarion; \
    <image_name>
```

## Contributors

* Duan Shiqiang <shiqiang.duan@nextlabs.com>
