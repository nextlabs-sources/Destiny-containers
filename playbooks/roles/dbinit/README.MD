# dbinit

Role for handling dbinit related configuration

## Notes

This role is meant to setup dbinit in a java container. A entrypoint script will be put at /usr/local/bin/entrypoint. Pass `dbinit` as first argument to the script to let the entrypoint configure the server properly using environment varibles. Environment variable list:

* DATABASE_USERNAME (string): Database username
* DATABASE_PASSWORD (string): Database encrypted password
* DATABASE_CONNECTSTRING (string): Database connect string
* ADMINISTRATOR_PASSWORD (string): OPTIONAL, if doing install action, can specify this value, will be `password` by default.

## Tunables

* artifacts_path (string): Path to artifacts

## Dependencies

* None

## Example Usage

```bash
# For install action
docker run -it \
    -e DATABASE_USERNAME=clarion \
    -e 'DATABASE_PASSWORD=123next!' \
    -e DATABASE_CONNECTSTRING=postgresql://pf-linux01.qapf1.qalab01.nextlabs.com:5432/clarion \
    <image_name> dbinit install
# For upgrade action
docker run -it \
    -e DATABASE_USERNAME=clarion \
    -e 'DATABASE_PASSWORD=123next!' \
    -e DATABASE_CONNECTSTRING=postgresql://pf-linux01.qapf1.qalab01.nextlabs.com:5432/clarion \
    <image_name> dbinit upgrade -fromV 8.0.4 -toV 8.0.6
```

## Contributors

* Duan Shiqiang <shiqiang.duan@nextlabs.com>
