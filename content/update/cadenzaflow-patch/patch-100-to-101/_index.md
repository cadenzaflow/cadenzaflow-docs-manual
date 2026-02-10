---

title: "Update from CadenzaFlow 1.0.0 to 1.0.1"
weight: 1
layout: "single"

menu:
  main:
    name: "Update from CadenzaFlow 1.0.0 to 1.0.1"
    identifier: "cadenzaflow-patch-100-101"
    parent: "migration-guide-patch"
    pre: "Update from CadenzaFlow 1.0.0 to 1.0.1"

---


# cadenzaflow-bpm-spring-boot-starter-webapp updated

With cadenzaflow-bpm-spring-boot-starter-webapp version=1.0.1, webjar-classpath default value has been corrected as: "/META-INF/resources/webjars/cadenzaflow"

For applications that start CadenzaFlow as an embedded server and still have dependency to version=1.0.0, please
 * Update the dependency version to 1.0.1
 * Or introduce the following fix/patch/override to your application.yaml

```
camunda:
  bpm:
    webapp:
      webjar-classpath: /META-INF/resources/webjars/cadenzaflow
```