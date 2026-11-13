---

title: 'Download'
weight: 10

menu:
  main:
    identifier: "user-guide-introduction-downloading-cadenzaflow"
    parent: "user-guide-introduction"

---


# Prerequisites

Before downloading CadenzaFlow, make sure you have a JRE (Java Runtime Environment), or better, a JDK
(Java Development Kit) installed. Please check the supported [Java versions]({{< ref "/introduction/supported-environments.md#java" >}}).

[Download JDK][get-jdk]


# Download the Runtime

CadenzaFlow is a flexible framework which can be used in different contexts. See [Architecture Overview]({{< ref "/introduction/architecture.md" >}}) for more details. Based on how you want
to use CadenzaFlow, you can choose a different distribution.

CadenzaFlow provides separate runtime downloads for community users and enterprise subscription
customers. Please refer to [download page][download-page] to download.

It is also possible to run CadenzaFlow with [Spring Boot][run-with-spring-boot] and [Docker][run-with-docker].

## Full Distribution

Download the full distribution if you want to use a [shared process engine][shared-engine] or if you
want to get to know CadenzaFlow quickly, without any additional setup or installation steps required.

The full distribution bundles

* Process Engine configured as [shared process engine][shared-engine],
* Runtime Web Applications (Tasklist, Cockpit, Admin),
* Rest Api,
* Container / Application Server itself.

{{< note title="Server/Container" class="info" >}}
  If you download the full distribution for an open-source application
  server/container, the container itself is included. For example, if you download the Tomcat
  distribution, Tomcat itself is included and the CadenzaFlow binaries (process engine and
  web apps) are pre-installed in the container.
{{< /note >}}



See the [Installation Guide][installation-guide-full] for additional details.


# Maven Artifacts

The libraries of CadenzaFlow are published to Maven Central: the process engine, the Spring Boot
starters, the External Task Client, the BOM and the other modules you put into your own
application. A Maven or Gradle build finds them without any extra setup.

Since 1.3.0, some artifacts are published only to the CadenzaFlow Nexus
(`https://nexus.cadenzaflow.com/repository/cadenzaflow-nexus`):

* the distributions (CadenzaFlow Run, Tomcat) and the WAR files for application servers
  (`cadenzaflow-webapp`, `cadenzaflow-engine-rest`, `cadenzaflow-engine-rest-jakarta`),
* the Java EE integration (`cadenzaflow-engine-cdi`, `cadenzaflow-engine-cdi-jakarta`,
  `cadenzaflow-ejb-client`, `cadenzaflow-ejb-client-jakarta`),
* the OpenAPI description of the REST API (`cadenzaflow-engine-rest-openapi`),
* the javax and Spring 5 variants `cadenzaflow-engine-rest-core`, `cadenzaflow-engine-spring` and
  `cadenzaflow-spin-dataformat-xml-dom`. Maven Central has their Jakarta and Spring 6 / 7 variants:
  `cadenzaflow-engine-rest-core-jakarta`, `cadenzaflow-engine-spring-6`, `cadenzaflow-engine-spring-7`
  and `cadenzaflow-spin-dataformat-xml-dom-jakarta`,
* the shaded jars `cadenzaflow-spin-dataformat-all` and `cadenzaflow-connect-connectors-all`,
* the `test-sources` jars.

The POMs of CadenzaFlow declare no repositories. If you need one of these artifacts, add the
CadenzaFlow Nexus to your build. In Maven:

```xml
<repositories>
  <repository>
    <id>cadenzaflow-nexus</id>
    <url>https://nexus.cadenzaflow.com/repository/cadenzaflow-nexus</url>
  </repository>
</repositories>
```

In Gradle:

```groovy
repositories {
  mavenCentral()
  maven { url 'https://nexus.cadenzaflow.com/repository/cadenzaflow-nexus' }
}
```

If your organization resolves all artifacts through its own repository manager, add the
CadenzaFlow Nexus there.


# Download CadenzaFlow Modeler

CadenzaFlow Modeler is a modeling Tool for BPMN 2.0 and DMN 1.3. CadenzaFlow Modeler can be downloaded
from the [community download page][community-download-page].



[get-jdk]: https://www.oracle.com/technetwork/java/javase/downloads/index.html
[download-page]: https://cadenzaflow.com/download
[community-download-page]: https://cadenzaflow.com/download
[enterprise-download-page]: https://cadenzaflow.com/download
[shared-engine]: {{< ref "/introduction/architecture.md#shared-container-managed-process-engine" >}}
[installation-guide-full]: {{< ref "/installation/_index.md" >}}
[run-with-spring-boot]: {{< ref "/user-guide/spring-boot-integration/_index.md" >}}
[run-with-docker]: {{< ref "/installation/docker.md" >}}
