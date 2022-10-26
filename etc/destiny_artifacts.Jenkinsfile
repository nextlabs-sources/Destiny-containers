#!groovy

pipeline {

  agent any

  parameters {
    string(name: 'DESTINY_BUILD_ARTIFACTS_ZIP_FILE', defaultValue: '', description: 'Required, Path to destiny build zip')
    string(name: 'DESTINY_XLIB_ARTIFACTS_ZIP_FILE', defaultValue: '', description: 'Required, Path to destiny xlib zip')
    string(name: 'OAUTH2JWTSECRET_PLUGIN_ZIP', defaultValue: '', description: 'Required, Path to oauth2 jwt plugin build zip')
    string(name: 'DestinyDockerBuildJob', defaultValue: '', description: 'Optional, Docker build job name on same jenkins to be triggered after build')
    string(name: 'docker_image_tag', defaultValue: 'latest', description: 'Optional, the docker tag parameter to pass to DestinyDockerBuildJob')
  }

  stages {
    
    stage('Cleanup') {
      steps {
        cleanWs()
      }
    }
    
    stage('Prepare') {
        steps {
          echo "DESTINY_BUILD_ARTIFACTS_ZIP_FILE is ${params.DESTINY_BUILD_ARTIFACTS_ZIP_FILE}"
          echo "DESTINY_XLIB_ARTIFACTS_ZIP_FILE is ${params.DESTINY_XLIB_ARTIFACTS_ZIP_FILE}"
          echo "OAUTH2JWTSECRET_PLUGIN_ZIP is ${params.OAUTH2JWTSECRET_PLUGIN_ZIP}"
          echo "workspace: ${env.WORKSPACE}"
        }
    }

    stage('UnpackDestinyArtifacts') {
      steps {
        parallel(
          "unzip_destiny_apps": {
            unzip zipFile: params.DESTINY_BUILD_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny", glob: "run/server/apps/*.war"
          },
          "unzip_destiny_certificates": {
            unzip zipFile: params.DESTINY_BUILD_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny", glob: "enrollment.cer"
            unzip zipFile: params.DESTINY_BUILD_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny", glob: "keymanagement.cer"
            unzip zipFile: params.DESTINY_BUILD_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny", glob: "policyAuthor.cer"
            unzip zipFile: params.DESTINY_BUILD_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny", glob: "temp_agent.cer"
          },
          "unzip_destiny_configuration": {
            unzip zipFile: params.DESTINY_BUILD_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny", glob: "run/server/configuration/*.xml"
            unzip zipFile: params.DESTINY_BUILD_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny", glob: "run/server/configuration/*.xsd"
            unzip zipFile: params.DESTINY_BUILD_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny", glob: "agentprofile.xml"
            unzip zipFile: params.DESTINY_BUILD_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny", glob: "commprofile.template.xml"
            unzip zipFile: params.DESTINY_BUILD_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny", glob: "mapping.xml"
            unzip zipFile: params.DESTINY_BUILD_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny", glob: "temp_agent-keystore.jks"
            unzip zipFile: params.DESTINY_BUILD_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny", glob: "run/server/certificates/temp_agent-keystore.jks"
          },
          "unzip_destiny_shared_lib": {
            unzip zipFile: params.DESTINY_BUILD_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny", glob: "common-version.jar"
            unzip zipFile: params.DESTINY_BUILD_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny", glob: "crypt.jar"
            unzip zipFile: params.DESTINY_BUILD_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny", glob: "server-axis-security.jar"
            unzip zipFile: params.DESTINY_BUILD_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny", glob: "server-base.jar"
            unzip zipFile: params.DESTINY_BUILD_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny", glob: "server-base-internal.jar"
            unzip zipFile: params.DESTINY_BUILD_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny", glob: "server-security.jar"
            unzip zipFile: params.DESTINY_BUILD_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny", glob: "run/server/license/license.jar"
            unzip zipFile: params.DESTINY_BUILD_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny", glob: "nxl-filehandler.jar"
          },
          "uznip_destiny_xlib": {
            unzip zipFile: params.DESTINY_XLIB_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny/xlib", glob: "jar/bcprov-jdk15on-151.jar"
            unzip zipFile: params.DESTINY_XLIB_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny/xlib", glob: "jar/c3p0-0.9.1.2.jar"
            unzip zipFile: params.DESTINY_XLIB_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny/xlib", glob: "jar/commons-logging-1.1.1.jar"
            unzip zipFile: params.DESTINY_XLIB_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny/xlib", glob: "jar/ojdbc6.jar"
            unzip zipFile: params.DESTINY_XLIB_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny/xlib", glob: "jar/postgresql-9.2-1002.jdbc4.jar"
            unzip zipFile: params.DESTINY_XLIB_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny/xlib", glob: "jar/sqljdbc4.jar"
          },
          "unzip_destiny_license": {
            unzip zipFile: params.DESTINY_BUILD_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny", glob: "license.dat"
          },
          "unzip_destiny_tools": {
            unzip zipFile: params.DESTINY_BUILD_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny", glob: "tools/common/**"
            unzip zipFile: params.DESTINY_BUILD_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny", glob: "tools/crypt/**"
            unzip zipFile: params.DESTINY_BUILD_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny", glob: "tools/dbInit/**"
            unzip zipFile: params.DESTINY_BUILD_ARTIFACTS_ZIP_FILE, dir: "${env.WORKSPACE}/destiny", glob: "seed_data/**"
          },
          "unzip_oauth2_jwt_plugin": {
            unzip zipFile: params.OAUTH2JWTSECRET_PLUGIN_ZIP, dir: "${env.WORKSPACE}/plugins/Oauth2JWTSecret-Plugin"
          }
        )
      }
    }
    
    stage('OrganizeArtifacts') {
      steps {
        parallel(
          "apps": {
            fileOperations([
              fileCopyOperation(
                excludes: '**/rest-api.war',
                flattenFiles: true,
                includes: 'destiny/run/server/apps/*.war',
                targetLocation: 'destiny_artifacts/apps'
              )
            ])
          },
          "certificates": {
            fileOperations([
              fileCopyOperation(
                flattenFiles: true,
                includes: 'destiny/*.cer',
                targetLocation: 'destiny_artifacts/certificates'
              )
            ])
          },
          "configuration": {
            fileOperations([
              fileCopyOperation(
                flattenFiles: true,
                includes: 'destiny/run/server/configuration/configuration.digester.rules.xml',
                targetLocation: 'destiny_artifacts/configuration/dms'
              ),
              fileCopyOperation(
                flattenFiles: true,
                includes: 'destiny/run/server/configuration/Configuration.xsd',
                targetLocation: 'destiny_artifacts/configuration/dms'
              ),
              fileCopyOperation(
                flattenFiles: true,
                includes: 'destiny/run/server/configuration/configuration-template.xml',
                targetLocation: 'destiny_artifacts/configuration/dms'
              ),
              fileCopyOperation(
                flattenFiles: true,
                includes: 'destiny/agentprofile.xml',
                targetLocation: 'destiny_artifacts/configuration/dpc/config'
              ),
              fileCopyOperation(
                flattenFiles: true,
                includes: 'destiny/commprofile.template.xml',
                targetLocation: 'destiny_artifacts/configuration/dpc/config'
              ),
              fileCopyOperation(
                flattenFiles: true,
                includes: 'destiny/mapping.xml',
                targetLocation: 'destiny_artifacts/configuration/dpc/config'
              ),
              fileCopyOperation(
                flattenFiles: true,
                includes: 'destiny/temp_agent-keystore.jks',
                targetLocation: 'destiny_artifacts/configuration/dpc/config/security'
              ),
              fileCopyOperation(
                flattenFiles: true,
                includes: 'destiny/run/server/configuration/dashboard.xml',
                targetLocation: 'destiny_artifacts/configuration/inquiryCenter'
              )
            ])
          },
          "plugins": {
            dir('plugins/Oauth2JWTSecret-Plugin') {
              fileOperations([
                fileCopyOperation(
                  includes: '**/**',
                  targetLocation: "${env.WORKSPACE}/destiny_artifacts/plugins/Oauth2JWTSecret-Plugin"
                )
              ])
            }
          },
          "shared/lib": {
            fileOperations([
              fileCopyOperation(
                flattenFiles: true,
                includes: 'destiny/*.jar',
                targetLocation: 'destiny_artifacts/shared/lib'
              ),
              fileCopyOperation(
                flattenFiles: true,
                includes: 'destiny/run/server/license/license.jar',
                targetLocation: 'destiny_artifacts/shared/lib'
              )
            ])
          },
          "shared/license": {
            fileOperations([
              fileCopyOperation(
                flattenFiles: true,
                includes: 'destiny/license.dat',
                targetLocation: 'destiny_artifacts/shared'
              )
            ])
          },
          "shared/xlib": {
            fileOperations([
              fileCopyOperation(
                flattenFiles: true,
                includes: 'destiny/xlib/jar/*.jar',
                targetLocation: 'destiny_artifacts/shared/xlib'
              )
            ])
          },
          "tools": {
            dir('destiny/tools') {
              fileOperations([
                fileCopyOperation(
                  includes: '**/**',
                  targetLocation: "${env.WORKSPACE}/destiny_artifacts/tools"
                )
              ])
            }
            dir('destiny/seed_data') {
              fileOperations([
                fileCopyOperation([
                  includes: '**/**',
                  targetLocation: "${env.WORKSPACE}/destiny_artifacts/tools/dbInit/pf/seed_data"
                ])
              ])
            }
          }
        )
      }
    }

    stage('PostCleanup') {
      steps {
        dir('destiny') {
          deleteDir()
        }
        dir('plugins') {
          deleteDir()
        }
      }
    }

    stage('TriggerDockerBuild') {
      when {
        // Only do this is DestinyDockerBuildJob is defined
        expression { "${params.DestinyDockerBuildJob}" != "" }
      }
      steps {
        build job: "${params.DestinyDockerBuildJob}", parameters: [
          string(name: 'destiny_artifacts', value: "${env.WORKSPACE}/destiny_artifacts"),
          string(name: 'docker_image_tag', value: params.docker_image_tag)
        ]
      }
    }
  }
}
