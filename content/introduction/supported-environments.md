---

title: 'Supported Environments'
weight: 40

menu:
  main:
    identifier: "user-guide-introduction-supported-environments"
    parent: "user-guide-introduction"

---


Run CadenzaFlow in every Java-runnable environment. CadenzaFlow is supported with our QA infrastructure in the following environments.

{{< note title="Supported Environments" class="info" >}}
  Please note that the environments listed in this section depend on the version of CadenzaFlow. Please select the corresponding version of this documentation to see the environment that fits to your version of CadenzaFlow.
{{< /note >}}


# Container/Application Server for Runtime Components

## Application-Embedded Process Engine

* All Java application servers
* CadenzaFlow Spring Boot Starter: Embedded Tomcat
  * [Supported versions]({{< ref "/user-guide/spring-boot-integration/version-compatibility.md" >}})
  * [Deployment scenarios]({{< ref "/user-guide/spring-boot-integration/_index.md#supported-deployment-scenarios" >}})
* CadenzaFlow Engine Quarkus Extension
  * [Supported versions]({{< ref "/user-guide/quarkus-integration/version-compatibility.md" >}})
  * [Deployment scenarios]({{< ref "/user-guide/quarkus-integration/_index.md#supported-deployment-scenarios" >}})

## Container-Managed Process Engine and CadenzaFlow Webapps

* Apache Tomcat 10.1
* JBoss EAP 8.0
* WildFly Application Server 33.0 / 35.0 / 37.0
* Oracle WebLogic Server 14.1.2

# Databases

## Supported Database Products

* PostgreSQL 15 / 16 / 17 / 18
* Amazon Aurora PostgreSQL compatible with PostgreSQL 14 / 15 / 16
* Oracle 19c / 23ai
* H2 2.3 (not recommended for Cluster Mode - see Deployment Note)

## Database Clustering & Replication

Clustered or replicated databases are supported given the following conditions. The communication between CadenzaFlow and the database cluster has to match with the corresponding non-clustered / non-replicated configuration. It is especially important that the configuration of the database cluster guarantees the equivalent behavior of READ-COMMITTED isolation level.


# Web Browser

* Google Chrome latest
* Mozilla Firefox latest
* Microsoft Edge latest


# Java

* Java 11 / 17 / 21


# CadenzaFlow Modeler

* Windows 10 / 11
* macOS 13 / 14 / 15
* Ubuntu LTS (latest)

# Maintenance Policy

Check our [Enterprise Announcements page](/enterprise/announcement/) for confirmed changes to our supported environments in upcoming releases.

## Adding Environments

Whenever a new version of one of the following environments is released, we target support of that new version with the next minor release of CadenzaFlow. A new released environment has to be available three months before the next CadenzaFlow minor release to be considered.

* Java Language (LTS)
* Spring Boot
* Oracle Database (LTS)
* PostgreSQL

The exact release in which we support a new environment depends on factors such as the release date of the environment and the required implementation effort.

Version support for other environments is decided case by case, much of which is based on the demand in our user base.

## Removing Environments

Whenever a new version of one of the following environments is supported, we usually discontinue support of the oldest version with the same release.

  * n.a.

Note that we may decide to deviate from this policy on a case-by-case basis.
