---

title: 'JNDI Bindings for CadenzaFlow Services'
weight: 20

menu:
  main:
    identifier: "user-guide-runtime-container-integration-jndi"
    parent: "user-guide-runtime-container-integration"

---

The CadenzaFlow Services (i.e., Process Engine Service and Process Application Service) are provided via JNDI Bindings with the following JNDI names:

* Process Engine Service: `java:global/cadenzaflow-bpm-platform/process-engine/ProcessEngineService!org.cadenzaflow.bpm.ProcessEngineService`
* Process Application Service: `java:global/cadenzaflow-bpm-platform/process-engine/ProcessApplicationService!org.cadenzaflow.bpm.ProcessApplicationService`

On JBoss EAP and WildFly, you are able to get any of these CadenzaFlow Services through a JNDI lookup. 
However, on Apache Tomcat you have to do quite a bit more to be able to do a lookup to get one of these CadenzaFlow Services.
