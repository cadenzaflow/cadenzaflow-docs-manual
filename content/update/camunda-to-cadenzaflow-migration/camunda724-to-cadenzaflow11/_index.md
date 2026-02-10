---

title: "Camunda 7.24 to CadenzaFlow 1.1"
weight: 1
layout: "single"

menu:
  main:
    name: "Camunda 7.24 to CadenzaFlow 1.1"
    identifier: "migration-guide-camunda-724-cadenzaflow-11"
    parent: "migration-guide-camunda-to-cadenzaflow"
    pre: "Migrate to Cadenza `1.1` from Camunda `7.24.x`."

---


This document guides you through the migration from Camunda to `7.24.x` to CadenzaFlow `1.1` and covers the following use cases:

1. For administrators and developers: [Database updates](#database-updates)
1. For administrators and developers: [Full distribution update](#full-distribution)
1. For administrators and developers: [Bootstrap NES and AngularJS NES by HeroDevs, Inc.](#bootstrap-nes-and-angularjs-nes-by-herodevs-inc)
1. For developers: [Set Variables Async API](#set-variables-async-api)
1. For developers: [GraalVM Upgrade](#graalvm-upgrade)
1. For developers: [Spring Framework Upgrade (changes required when using Java 11)](#spring-framework-upgrade-changes-required-when-using-java-11)
1. For developers: [Quarkus 3.20 Extension Update](#quarkus-3-20-extension-update)

This guide covers mandatory migration steps and optional considerations for the initial configuration of new functionality included in CadenzaFlow 1.1.

# Database updates

Since CadenzaFlow 1.1 is a stable fork of Camunda 7.24, two platforms are fully equivalent, and no updates are required.


# Full distribution

This section is applicable if you installed the
[Full Distribution]({{< ref "/introduction/downloading-cadenzaflow.md#full-distribution" >}})
with a **shared process engine**.

The following steps are required:

1. Update the CadenzaFlow libraries and applications inside the application server.
2. Migrate custom process applications.

Before starting, ensure you have downloaded the CadenzaFlow 1.1 distribution for the application server you use. This contains the SQL scripts and libraries required for the update. This guide assumes you have unpacked the distribution to a path named `$DISTRIBUTION_PATH`.

# Bootstrap NES and AngularJS NES by HeroDevs, Inc.

Since CadenzaFlow 1.1 is a stable fork of Camunda 7.24, two platforms are fully equivalent, and no updates are required.

# Set Variables Async API

Since CadenzaFlow 1.1 is a stable fork of Camunda 7.24, two platforms are fully equivalent, and no updates are required.

# GraalVM Upgrade

Since CadenzaFlow 1.1 is a stable fork of Camunda 7.24, two platforms are fully equivalent, and no updates are required.

# Spring Framework Upgrade (changes required when using Java 11)

Since CadenzaFlow 1.1 is a stable fork of Camunda 7.24, two platforms are fully equivalent, and no updates are required.

# Quarkus 3.20 Extension Update

Since CadenzaFlow 1.1 is a stable fork of Camunda 7.24, two platforms are fully equivalent, and no updates are required.