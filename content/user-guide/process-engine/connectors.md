---

title: 'Connectors'
weight: 100

menu:
  main:
    identifier: "user-guide-process-engine-connectors"
    parent: "user-guide-process-engine"

---


With the dependency [cadenzaflow-connect](https://github.com/cadenzaflow/cadenzaflow-bpm-platform/tree/master/connect), the process engine supports simple
connectors. Currently the following connector implementations exist:

<table class="table">
  <tr>
    <th>Connector</th>
    <th>ID</th>
  </tr>
  <tr>
    <td>REST HTTP</td>
    <td>http-connector</td>
  </tr>
  <tr>
    <td>SOAP HTTP</td>
    <td>soap-http-connector</td>
  </tr>
</table>

It is also possible to implement your own custom connector in cadenzaflow. For more information about extending connectors please visit the [Connector reference]({{< ref "/reference/connect/extending-connect.md" >}}). 


# Configure CadenzaFlow Connect

As CadenzaFlow Connect is available only partially when using the process engine (check the list below). With a pre-built distribution, CadenzaFlow Connect is already preconfigured.

The following `connect` artifacts exist:

* `cadenzaflow-connect-core`: a jar that contains only the core Connect classes. The artifact already is available as dependency to the process engine. In addition to `cadenzaflow-connect-core`, single connector implementations like `cadenzaflow-connect-http-client` and `cadenzaflow-connect-soap-http-client` exist. These dependencies should be used when the default connectors have to be reconfigured or when custom connector implementations are used.
* `cadenzaflow-connect-connectors-all`: a single jar without dependencies that contains the HTTP and SOAP connectors.
* `cadenzaflow-engine-plugin-connect`: a process engine plugin to add Connect to CadenzaFlow.


# Maven Coordinates

{{< note title="" class="info" >}}
  Please import the [CadenzaFlow BOM](/get-started/apache-maven/) to ensure correct versions for every CadenzaFlow project.
{{< /note >}}


## cadenzaflow-connect-core

`cadenzaflow-connect-core` contains the core classes of Connect. Additionally, the HTTP and SOAP connectors can be added with the dependencies `cadenzaflow-connect-http-client` and `cadenzaflow-connect-soap-http-client`. These artifacts will transitively pull in their dependencies, like Apache HTTP client. For integration with the engine, the artifact `cadenzaflow-engine-plugin-connect` is needed. Given that the BOM is imported, the Maven coordinates are as follows:

```xml
<dependency>
  <groupId>org.cadenzaflow.connect</groupId>
  <artifactId>cadenzaflow-connect-core</artifactId>
</dependency>
```

```xml
<dependency>
  <groupId>org.cadenzaflow.connect</groupId>
  <artifactId>cadenzaflow-connect-http-client</artifactId>
</dependency>
```

```xml
<dependency>
  <groupId>org.cadenzaflow.connect</groupId>
  <artifactId>cadenzaflow-connect-soap-http-client</artifactId>
</dependency>
```

```xml
<dependency>
  <groupId>org.cadenzaflow.bpm</groupId>
  <artifactId>cadenzaflow-engine-plugin-connect</artifactId>
</dependency>
```


## cadenzaflow-connect-connectors-all

This artifact contains the HTTP and SOAP connectors as well as their dependencies. To avoid conflicts with other versions of these dependencies, the dependencies are relocated to different packages. `cadenzaflow-connect-connectors-all` has the following Maven coordinates:

```xml
<dependency>
  <groupId>org.cadenzaflow.connect</groupId>
  <artifactId>cadenzaflow-connect-connectors-all</artifactId>
</dependency>
```


## Configure the Process Engine Plugin

`cadenzaflow-engine-plugin-connect` contains a class called `org.cadenzaflow.connect.plugin.impl.ConnectProcessEnginePlugin` that can be registered with a process engine using the [plugin mechanism]({{< ref "/user-guide/process-engine/process-engine-plugins.md" >}}). For example, a `bpm-platform.xml` file with the plugin enabled would look as follows:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<bpm-platform xmlns="http://www.cadenzaflow.org/schema/1.0/BpmPlatform"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://www.cadenzaflow.org/schema/1.0/BpmPlatform http://www.cadenzaflow.org/schema/1.0/BpmPlatform ">
  ...
  <process-engine name="default">
    ...
    <plugins>
      <plugin>
        <class>org.cadenzaflow.connect.plugin.impl.ConnectProcessEnginePlugin</class>
      </plugin>
    </plugins>
    ...
  </process-engine>
</bpm-platform>
```

{{< note title="" class="info" >}}
  When using a pre-built distribution of CadenzaFlow, the plugin is already pre-configured.
{{< /note >}}


# Use Connectors

To use a connector, you have to add the CadenzaFlow extension element [connector]({{< ref "/reference/bpmn20/custom-extensions/extension-elements.md#cadenzaflow-connector" >}}). The connector is configured by a unique [connectorId]({{< ref "/reference/bpmn20/custom-extensions/extension-elements.md#cadenzaflow-connectorid" >}}), which specifies the used connector implementation. The ids of the currently supported connectors can be found at the beginning of this section. Additionally, an [input/output mapping]({{< ref "/user-guide/process-engine/variables.md#input-output-variable-mapping" >}}) is used to configure the connector. The required input parameters and the available output parameters depend on the connector implementation. Additional input parameters can also be provided to be used within the connector.

As an example, a shortened configuration of the CadenzaFlow SOAP connector implementation is shown. A complete [example](https://github.com/cadenzaflow/cadenzaflow-bpm-examples/tree/master/servicetask/soap-service) can be found in the [CadenzaFlow examples repository](https://github.com/cadenzaflow/cadenzaflow-bpm-examples) on GitHub.

```xml
<serviceTask id="soapRequest" name="Simple SOAP Request">
  <extensionElements>
    <cadenzaflow:connector>
      <cadenzaflow:connectorId>soap-http-connector</cadenzaflow:connectorId>
      <cadenzaflow:inputOutput>
        <cadenzaflow:inputParameter name="url">
          http://example.com/webservice
        </cadenzaflow:inputParameter>
        <cadenzaflow:inputParameter name="payload">
          <![CDATA[
            <soap:Envelope ...>
              ... // the request envelope
            </soap:Envelope>
          ]]>
        </cadenzaflow:inputParameter>
        <cadenzaflow:outputParameter name="result">
          <![CDATA[
            ... // process response body
          ]]>
        </cadenzaflow:outputParameter>
      </cadenzaflow:inputOutput>
    </cadenzaflow:connector>
  </extensionElements>
</serviceTask>
```

A full [example](https://github.com/cadenzaflow/cadenzaflow-bpm-examples/tree/master/servicetask/rest-service) of the REST connector can also be found in the [CadenzaFlow examples repository](https://github.com/cadenzaflow/cadenzaflow-bpm-examples) on GitHub.
