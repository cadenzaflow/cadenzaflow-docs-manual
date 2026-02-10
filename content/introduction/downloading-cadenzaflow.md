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
