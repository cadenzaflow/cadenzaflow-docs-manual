---

title: 'Public API'
weight: 80

menu:
  main:
    identifier: "user-guide-introduction-public-api"
    parent: "user-guide-introduction"

---


CadenzaFlow provides a public API. This section covers the definition of the public API and backwards compatibility for version updates.


# Definition of Public API

The CadenzaFlow public API is limited to the following items:

Java API: 

All non-implementation Java packages (package name does not contain `impl`) of the following modules.

* `cadenzaflow-engine`
* `cadenzaflow-engine-spring`
* `cadenzaflow-engine-cdi`
* `cadenzaflow-engine-dmn`
* `cadenzaflow-bpmn-model`
* `cadenzaflow-cmmn-model`
* `cadenzaflow-dmn-model`
* `cadenzaflow-spin-core`
* `cadenzaflow-connect-core`
* `cadenzaflow-commons-typed-values`

HTTP API (REST API):

* `cadenzaflow-engine-rest`: HTTP interface (set of HTTP requests accepted by the REST API as documented in [REST API reference]({{< ref "/reference/rest/_index.md" >}}). Java classes are not part of the public API.


# Backwards Compatibility for Public API

The CadenzaFlow versioning scheme follows the MAJOR.MINOR.PATCH pattern put forward by [Semantic Versioning](http://semver.org/). CadenzaFlow will maintain public API backwards compatibility for MINOR version updates. Example: Update from version `1.0.x` to `1.1.x` will not break the public API.
