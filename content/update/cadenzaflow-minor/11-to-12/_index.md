---

title: "Update from CadenzaFlow 1.1 to 1.2"
weight: 1
layout: "single"

menu:
  main:
    name: "Update from CadenzaFlow 1.1 to 1.2"
    identifier: "migration-guide-cadenzaflow-11-12"
    parent: "migration-guide-cadenzaflow-minor"
    pre: "Update from CadenzaFlow 1.1 to 1.2"

---


This document guides you through the update from CadenzaFlow `1.1.0` to `1.2.0` and covers the following use cases:

1. For administrators and developers: [Database updates](#database-updates)
1. For administrators and developers: [Full distribution update](#full-distribution)
1. For developers: [Brand rename: Java packages and Maven coordinates](#brand-rename-java-packages-and-maven-coordinates)
1. For administrators and developers: [Dependency upgrades](#dependency-upgrades)
1. For administrators: [Trivy Security Scan Pipeline](#trivy-security-scan-pipeline)


This guide covers mandatory migration steps and optional considerations for the initial configuration of new functionality included in CadenzaFlow 1.2.0.

# Database updates

Every CadenzaFlow installation requires a database schema update. Check our [database schema update guide]({{< ref "/installation/database-schema.md#update" >}})
for further instructions.

The 1.1 to 1.2 upgrade scripts only record the new version in `ACT_GE_SCHEMA_LOG`; no tables, columns, or constraints change.

# Full distribution

This section is applicable if you installed the
[Full Distribution]({{< ref "/introduction/downloading-cadenzaflow.md#full-distribution" >}})
with a **shared process engine**.

The following steps are required:

1. Update the CadenzaFlow libraries and applications inside the application server.
2. Migrate custom process applications. Most projects need only the **Brand rename** changes described below; library upgrades are transparent.

Before starting, ensure you have downloaded the CadenzaFlow 1.2.0 distribution for the application server you use. This contains the SQL scripts and libraries required for the update. This guide assumes you have unpacked the distribution to a path named `$DISTRIBUTION_PATH`.

# Brand rename: Java packages and Maven coordinates

{{< note title="Breaking change" class="warning" >}}
CadenzaFlow 1.2.0 completes the rename from the Camunda namespace to the CadenzaFlow namespace. Process applications, custom plugins, and any project that depends on CadenzaFlow artifacts must update both their Java imports and their Maven/Gradle coordinates.
{{< /note >}}

## Rename rule

Across every published artifact and every shipped package, the prefix changes consistently:

- Java packages: `org.camunda.*` → `org.cadenzaflow.*`
- Maven `groupId`: `org.camunda.bpm.*` → `org.cadenzaflow.bpm.*`
- Maven `artifactId`: `camunda-*` → `cadenzaflow-*`

No public class names, method signatures, or REST endpoints have changed. Only the namespace path is different.

## Migration steps

1. **Update Java imports**: in your IDE, perform a project-wide find-and-replace of `org.camunda.` with `org.cadenzaflow.`.
2. **Update dependency coordinates** in `pom.xml`, `build.gradle`, or any BOM you import.
3. **Rebuild and redeploy**. BPMN, DMN, and CMMN models do not need to change.

### Example

**Before (CadenzaFlow 1.1.0):**
```xml
<dependency>
  <groupId>org.camunda.bpm.springboot</groupId>
  <artifactId>camunda-bpm-spring-boot-starter-rest</artifactId>
  <version>1.1.0</version>
</dependency>
```

```java
import org.camunda.bpm.engine.RuntimeService;
import org.camunda.bpm.engine.delegate.JavaDelegate;
```

**After (CadenzaFlow 1.2.0):**
```xml
<dependency>
  <groupId>org.cadenzaflow.bpm.springboot</groupId>
  <artifactId>cadenzaflow-bpm-spring-boot-starter-rest</artifactId>
  <version>1.2.0</version>
</dependency>
```

```java
import org.cadenzaflow.bpm.engine.RuntimeService;
import org.cadenzaflow.bpm.engine.delegate.JavaDelegate;
```

The same coordinate update applies to Gradle build files and BOM imports — replace `org.camunda.bpm` with `org.cadenzaflow.bpm` and `camunda-*` with `cadenzaflow-*` consistently.

# Dependency upgrades

CadenzaFlow 1.2.0 ships with patched runtime and frontend dependencies, primarily addressing CVE advisories raised in early 2026. No API changes are introduced.

| Library | 1.1.0 | 1.2.0 |
|---|---|---|
| Spring Framework | `6.2.16` | `6.2.18` |
| Spring Boot | `3.5.11` | `3.5.14` |
| Tomcat (embedded) | `10.1.52` | `10.1.54` |
| Jackson core / databind | `2.19.4` | `2.21.3` |
| Jackson annotations | `2.19.4` | `2.21` |
| dompurify (webapps) | `3.3.2` | `3.4.1` |
| lodash (webapps) | `4.17.23` | `4.18.1` |

{{< note title="Jackson annotations version" class="info" >}}
From Jackson 2.20 onwards the `jackson-annotations` module is published without a patch number (`2.20`, `2.21`). The CadenzaFlow parent POM tracks it through a separate `version.jackson.annotations` property. If you pin Jackson versions yourself, mirror this split: `2.21.3` for `jackson-core` and `jackson-databind`, `2.21` for `jackson-annotations`.
{{< /note >}}

For standard usage no action is required — the 1.2.0 distribution brings every upgraded library in transitively. If your project pins these libraries independently of CadenzaFlow, align your declared versions with the table above to avoid resolution conflicts.

# Trivy Security Scan Pipeline

CadenzaFlow 1.2.0 introduces a Trivy-based security scan running on every push and pull request in the upstream repository. The scan publishes results to GitHub's Security tab and surfaces both library and container-image vulnerabilities.

This change affects the upstream CadenzaFlow repository only; it does not add a new requirement for consumer projects.
