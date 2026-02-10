---

title: "Quarkus Version Compatibility"
weight: 10

menu:
  main:
    name: "Version Compatibility"
    identifier: "user-guide-quarkus-version-compatibility"
    parent: "user-guide-quarkus-integration"

---

Each version of the CadenzaFlow Engine Quarkus Extension is bound to a specific version of CadenzaFlow and Quarkus. 
Only these default combinations are recommended (and supported) by CadenzaFlow.

<table class="table table-striped">
  <tr>
    <th>CadenzaFlow version</th>
    <th>Quarkus version</th>
  </tr>
  <tr>
    <td>1.0.x</td>
    <td>3.20.x</td>
  </tr>
</table>

In case a certain Quarkus version has a bug, you can override the existing Quarkus version by adding the following
inside your `pom.xml`. Note that this new CadenzaFlow/Quarkus version combination should also be supported by CadenzaFlow.

```xml
<dependencyManagement>
  <dependencies>
    ...
    <dependency>
      <groupId>io.quarkus.platform</groupId>
      <artifactId>quarkus-bom</artifactId>
      <version>${quarkus.framework.version}</version><!-- set correct version here -->
      <type>pom</type>
      <scope>import</scope>
    </dependency>
    ...
  </dependencies>
</dependencyManagement>
```
