# tomcat-common

Role for handling tomcat related configuration

## Notes

This role is meant to be configure tomcat for use of internal apps.

## Tunables

* catalina_home (string): (OPTIONAL) tomcat home, if not defined will try to resolve from environment variable CATALINA_HOME
* artifacts_path (string): Path to artifcats
* tomcat_lib_jars (list): Jars that should shoudl goes to <CATALINA_HOME>/lib
* tomcat_shared_jars (list): Jars that should goes to <CATALINA_HOME>/shared/lib
* tomcat_endorsed_jars(list): Jars that should goes to <CATALINA_HOME>/endorsed

## Dependencies

* None

## Example Usage

* None

## Contributors

* Duan Shiqiang <shiqiang.duan@nextlabs.com>
