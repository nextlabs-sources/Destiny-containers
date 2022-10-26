
`destiny_artfifacts` is used as a parameter passing to the build jobs (jenkins and packer build env) to refer to a path (folder) containing artifacts needed for building the docker images.

The expected files/folders under `destiny_artifacts` are:

```
.
├── apps
│   ├── cas.war
│   ├── control-center-console.war
│   ├── dabs.war
│   ├── dac.war
│   ├── dcsf.war
│   ├── ddac.war
│   ├── dem.war
│   ├── dkms.war
│   ├── dms.war
│   ├── dpc.war
│   ├── dps.war
│   ├── inquiryCenter.war
│   └── mgmtConsole.war
├── certificates
│   ├── enrollment.cer
│   ├── keymanagement.cer
│   ├── policyAuthor.cer
│   └── temp_agent.cer
├── configuration
│   ├── dms
│   │   ├── configuration.digester.rules.xml
│   │   ├── Configuration.xsd
│   │   └── configuration-template.xml
│   ├── dpc
│   │   └── config
│   │       ├── agentprofile.xml
│   │       ├── commprofile.template.xml
│   │       ├── mapping.xml
│   │       └── security
│   │           └── temp_agent-keystore.jks
│   └── inquiryCenter
│       └── dashboard.xml
├── plugins
│   └── Oauth2JWTSecret-Plugin
│       ├── Control Center
│       │   ├── JwtSecretServer.properties
│       │   └── Oauth2JWTSecret-Plugin-server.jar
│       └── Policy Controller
│           ├── JwtSecretClient.properties
│           └── Oauth2JWTSecret-Plugin-client.jar
├── shared
│   ├── lib
│   │   ├── common-version.jar
│   │   ├── crypt.jar
│   │   ├── license.jar
│   │   ├── server-axis-security.jar
│   │   ├── server-base.jar
│   │   ├── server-base-internal.jar
│   │   ├── server-security.jar
│   │   └── nxl-filehandler.jar
│   ├── license.dat
│   └── xlib
│       ├── bcprov-jdk15on-151.jar
│       ├── c3p0-0.9.1.2.jar
│       ├── commons-logging-1.1.1.jar
│       ├── ojdbc6.jar
│       ├── postgresql-9.2-1002.jdbc4.jar
│       └── sqljdbc4.jar
└── tools
    ├── common
    │   ...
    ├── crypt
    │   ...
    └── dbInit
        ...
```
