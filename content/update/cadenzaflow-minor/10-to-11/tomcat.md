---

title: "Update a Tomcat Installation from CadenzaFlow 1.0 to 1.1"

menu:
  main:
    name: "Tomcat"
    identifier: "migration-guide-cadenzaflow-10-11-tomcat"
    parent: "migration-guide-cadenzaflow-10-11"

---

The following steps describe how to update the CadenzaFlow artifacts on a Tomcat server in a shared process engine setting.

Throughout the procedure, refer to the [update guide][update-guide]. If not already done, download the
[CadenzaFlow 1.1 Tomcat distribution][tomcat-distribution].

The update procedure takes the following steps:

1. Update the CadenzaFlow core libraries.
2. Update optional CadenzaFlow libraries.
3. Update web applications.

In each of the following steps, the identifier `$*_VERSION` refers to the current versions and the new versions of the artifacts.

# 1. Update the CadenzaFlow core libraries

Replace the following libraries in the folder `$TOMCAT_HOME/lib/` with the new versions from the folder `$TOMCAT_DISTRIBUTION/lib/`:

* `cadenzaflow-engine-$PLATFORM_VERSION.jar`
* `cadenzaflow-bpmn-model-$PLATFORM_VERSION.jar`
* `cadenzaflow-cmmn-model-$PLATFORM_VERSION.jar`
* `cadenzaflow-dmn-model-$PLATFORM_VERSION.jar`
* `cadenzaflow-xml-model-$PLATFORM_VERSION.jar`
* `cadenzaflow-engine-dmn-$PLATFORM_VERSION.jar`
* `cadenzaflow-engine-feel-api-$PLATFORM_VERSION.jar`
* `cadenzaflow-engine-feel-juel-$PLATFORM_VERSION.jar`
* `cadenzaflow-engine-feel-scala-$PLATFORM_VERSION.jar`
* `cadenzaflow-juel-$PLATFORM_VERSION.jar`
* `cadenzaflow-commons-logging-$PLATFORM_VERSION.jar`
* `cadenzaflow-commons-typed-values-$PLATFORM_VERSION.jar`
* `cadenzaflow-commons-utils-$PLATFORM_VERSION.jar`
* `cadenzaflow-connect-connectors-all-$PLATFORM_VERSION.jar`
* `cadenzaflow-connect-core-$PLATFORM_VERSION.jar`
* `cadenzaflow-template-engines-freemarker-$PLATFORM_VERSION.jar`
* `feel-engine-$FEEL_ENGINE_VERSION-scala-shaded.jar`
* `freemarker-$FREEMARKER_VERSION.jar`
* `mybatis-$MYBATIS_VERSION.jar`

# 2. Update optional CadenzaFlow 1.1 libraries

In addition to the core libraries, there may be optional artifacts in `$TOMCAT_HOME/lib/` for LDAP integration, CadenzaFlow Connect, CadenzaFlow Spin, and scripting. If you use any of these extensions, the following update steps apply:

## LDAP integration

Copy the following library from `$TOMCAT_DISTRIBUTION/lib` to the folder `$TOMCAT_HOME/lib/`, if present:

* `cadenzaflow-identity-ldap-$PLATFORM_VERSION.jar`

## CadenzaFlow Connect plugin

Copy the following libraries from `$TOMCAT_DISTRIBUTION/lib` to the folder `$TOMCAT_HOME/lib/`, if present:

* `cadenzaflow-engine-plugin-connect-$PLATFORM_VERSION.jar`

## CadenzaFlow Spin

Copy the following libraries from `$TOMCAT_DISTRIBUTION/lib` to the folder `$TOMCAT_HOME/lib/`, if present:

* `cadenzaflow-spin-dataformat-all-$PLATFORM_VERSION.jar`
* `cadenzaflow-spin-core-$PLATFORM_VERSION.jar`
* `cadenzaflow-engine-plugin-spin-$PLATFORM_VERSION.jar`

## GraalVM JavaScript

Copy the following libraries from `$TOMCAT_DISTRIBUTION/lib` to the folder `$TOMCAT_HOME/lib/`, if present:

* `graal-sdk-$GRAAL_VERSION.jar`
* `icu4j-$ICU4J_VERSION.jar`
* `js-$GRAAL_VERSION.jar`
* `js-scriptengine-$GRAAL_VERSION.jar`
* `regex-$GRAAL_VERSION.jar`
* `truffle-api-$GRAAL_VERSION.jar`

## Groovy

Copy these libraries from `$TOMCAT_DISTRIBUTION/lib` to the folder `$TOMCAT_HOME/lib/`, if present:

* `groovy-$GROOVY_VERSION.jar`
* `groovy-jsr223-$GROOVY_VERSION.jar`
* `groovy-json-$GROOVY_VERSION.jar`
* `groovy-xml-$GROOVY_VERSION.jar`
* `groovy-templates-$GROOVY_VERSION.jar`

# 3. Update web applications

## Update REST API

The following steps are required to update the CadenzaFlow REST API on a Tomcat instance:

1. Undeploy an existing web application with a name like `cadenzaflow-engine-rest`.
2. Download the REST API web application archive from our [Artifact Repository][artifact-repository-restapi] Alternatively, switch to the private repository for the enterprise version (credentials from license required). 
2. Download the CadenzaFlow web application archive from our [Artifact Repository][artifact-repository-webapp]. Alternatively, switch to the private repository for the enterprise version (credentials from license required). Choose accordingly:
    * For [Tomcat 10](https://nexus.cadenzaflow.com/service/rest/repository/browse/cadenzaflow-nexus/org/cadenzaflow/bpm/webapp/cadenzaflow-webapp-tomcat-jakarta/), the name of the artifact is `$PLATFORM_VERSION/cadenzaflow-webapp-tomcat-jakarta-$PLATFORM_VERSION.war`.
    * For [Tomcat 9](https://nexus.cadenzaflow.com/service/rest/repository/browse/cadenzaflow-nexus/org/cadenzaflow/bpm/webapp/cadenzaflow-webapp-tomcat/), the name of the artifact is `$PLATFORM_VERSION/cadenzaflow-webapp-tomcat-$PLATFORM_VERSION.war`.

3. Deploy the web application archive to your Tomcat instance.

## Update Cockpit, Tasklist, and Admin

The following steps are required to update the CadenzaFlow web applications Cockpit, Tasklist, and Admin on a Tomcat instance:

1. Undeploy an existing web application with a name like `cadenzaflow-webapp`.
2. Download the CadenzaFlow web application archive from our [Artifact Repository][artifact-repository-webapp]. Alternatively, switch to the private repository for the enterprise version (credentials from license required). Choose accordingly:
    * For [Tomcat 10](https://nexus.cadenzaflow.com/service/rest/repository/browse/cadenzaflow-nexus/org/cadenzaflow/bpm/webapp/cadenzaflow-webapp-tomcat-jakarta/), the name of the artifact is `$PLATFORM_VERSION/cadenzaflow-webapp-tomcat-jakarta-$PLATFORM_VERSION.war`.
    * For [Tomcat 9](https://nexus.cadenzaflow.com/service/rest/repository/browse/cadenzaflow-nexus/org/cadenzaflow/bpm/webapp/cadenzaflow-webapp-tomcat/), the name of the artifact is `$PLATFORM_VERSION/cadenzaflow-webapp-tomcat-$PLATFORM_VERSION.war`.
3. Deploy the web application archive to your Tomcat instance.

[update-guide]: {{< ref "/update/cadenzaflow-minor/10-to-11/_index.md" >}}
[artifact-repository-restapi]: https://nexus.cadenzaflow.com:443/repository/cadenzaflow-nexus/org/cadenzaflow/bpm/cadenzaflow-engine-rest/1.0.1/cadenzaflow-engine-rest-1.0.1-tomcat.war
[artifact-repository-webapp]: https://nexus.cadenzaflow.com:443/repository/cadenzaflow-nexus/org/cadenzaflow/bpm/webapp/cadenzaflow-webapp-tomcat/1.0.1/cadenzaflow-webapp-tomcat-1.0.1.war
[tomcat-distribution]: https://downloads.cadenzaflow.com/release/communityEdition/cadenzaflow-bpm/tomcat/1.1/

