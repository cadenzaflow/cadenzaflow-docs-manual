---

title: "Camunda to CadenzaFlow Migration"
weight: 10

menu:
  main:
    name: "Camunda to CadenzaFlow Migration"
    identifier: "migration-guide-camunda-to-cadenzaflow"
    parent: "migration-guide"
    pre: "Guides you through Camunda to CadenzaFlow migration"

---

This section provides the required **migration procedures to CadenzaFlow 1.0.x** from Camunda 7.23/7.24.
{{< note title="!!! important - Transition Prerequisites" class="danger" >}}
- The **minimum Camunda release** required to begin a transition to CadenzaFlow is **Camunda 7.23 or 7.24**.  
- If your current version is earlier than 7.23/7.24, please follow the official [Camunda Update & Migration documentation](https://docs.camunda.org/manual/latest/update/) to upgrade before continuing.  
  - Starting with **Camunda 7.16.0**, Liquibase can be used to install the database schema and track required changes, providing operational convenience.  
  - For versions **earlier than 7.16**, you must apply database patches manually, as described in the same Camunda documentation.  
{{< /note >}}

These documents guide you through the process of updating your existing application or server installation from Camunda 7.23/7.24 to CadenzaFlow.

{{< note title="Do I need to apply every minor version if I missed a few?" class="warning" >}}
Database update scripts are are NOT cumulative. Consult our [database schema update guide]({{< ref "/installation/database-schema.md#update" >}}) for details on how to account for that. Application library updates are cumulative and don't necessarily require sequential minor version updates. You can just apply your target minor application libraries. You should, however, check the migration guide of EVERY intermediate minor version to understand all noteworthy changes in behavior.
{{< /note >}}

There is a dedicated update guide for each version:

