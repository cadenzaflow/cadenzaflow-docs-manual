---

title: "Patch Level Update"
weight: 20

menu:
  main:
    name: "Patch Level Update"
    identifier: "migration-guide-patch"
    parent: "migration-guide"
    pre: "Guides you through a patch level update (Example: CadenzaFlow `1.0.0` to `1.1.0`)."

---

This guide explains how to perform a patch level update. The *patch level* is the version number "after the second dot". Example: update from CadenzaFlow `1.0.0` to `1.1.0`.

{{< enterprise >}}
Please note that Patch Level Updates are only provided to enterprise customers, they are not available in the community edition.
{{< /enterprise >}}

# Database Patches

Between patch levels, the structure of the database schema is not changed. The database structure of all patch releases is backward compatible with the corresponding minor version. Our [database schema update guide]({{< ref "/installation/database-schema.md#patch-level-update" >}}) provides details on the update procedure as well as available database patches.

# Full Distribution

This section is applicable if you installed the [Full Distribution]({{< ref "/introduction/downloading-cadenzaflow.md#full-distribution" >}}) with a **shared process engine**. In this case you need to update the libraries and applications installed inside the application server.

Please note that the following procedure may differ for cluster scenarios. Contact our [support team](https://app.cadenzaflow.com/jira/browse/SUPPORT) if you need further assistance.

* Shut down the server
* Exchange CadenzaFlow libraries, tools and webapps (EAR, RAR, Subsystem, Shared Libs) - essentially, follow the [installation guide]({{< ref "/installation/full/_index.md" >}}) for your server.
* Restart the server

# Application With Embedded Process Engine

In case you use an embedded process engine inside your Java Application, you need to

1. update the Process Engine library in your dependency management (Apache Maven, Gradle ...),
2. re-package the application,
3. deploy the new version of the application.


# Applying Multiple Patches at Once

It is possible to apply multiple patches in one go (e.g., updating from `1.0.0` to `1.1.2`).


# Special Considerations

This section describes noteworthy changes between individual patch levels.

{{< note title="No special consideration" class="warning" >}}
If a patch-level update (for example, **1.0.0 → 1.1.0**) is marked as *“No special consideration”*, this means:  

- No additional patch-level warnings or instructions apply.  
- Replacing the back-end engine with the new version is sufficient.  
{{< /note >}}

## 1.0.0 to 1.1.0 

[Patch 1.0.0 to 1.1.0]({{< ref "/update/cadenzaflow-patch/patch-100-to-101/_index.md" >}})
