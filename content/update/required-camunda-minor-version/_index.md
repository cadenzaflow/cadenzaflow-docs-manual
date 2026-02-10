---

title: "Required Camunda Minor Version Updates"
weight: 10

menu:
  main:
    name: "Required Camunda Minor Version"
    identifier: "required-camunda-minor-version"
    parent: "migration-guide"
    pre: "Required Camunda Minor Version for Upgrade to CadenzaFlow"

---



This section provides the required/prerequisite **procedures to upgrade Camunda** to the required 7.23 or 7.24 base Camunda release.

{{< note title="!!! important - Transition Prerequisites" class="danger" >}}
- The **minimum Camunda release** required to begin a transition to CadenzaFlow is **Camunda 7.23 or 7.24**.  
- If your current version is earlier than 7.23/7.24, please follow the official [Camunda Update & Migration documentation](https://docs.camunda.org/manual/latest/update/) to upgrade before continuing.  
  - Starting with **Camunda 7.16.0**, Liquibase can be used to install the database schema and track required changes, providing operational convenience.  
  - For versions **earlier than 7.16**, you must apply database patches manually, as described in the same Camunda documentation.  
{{< /note >}}

