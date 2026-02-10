---

title: 'Service Task'
weight: 10

menu:
  main:
    identifier: "bpmn-ref-tasks-service-task"
    parent: "bpmn-ref-tasks"
    pre: "Invoke or execute business logic."

---



A Service Task is used to invoke services. In CadenzaFlow this is done by calling Java code or providing a work item for an external worker to complete asynchronously or invoking a logic which is implemented in form of webservices.

{{< bpmn-symbol type="service-task" >}}

# Calling Java Code

There are four ways of declaring how to invoke Java logic:

* Specifying a class that implements a JavaDelegate or ActivityBehavior
* Evaluating an expression that resolves to a delegation object
* Invoking a method expression
* Evaluating a value expression

To specify a class that is called during process execution, the fully qualified classname needs to be provided by the `cadenzaflow:class` attribute.

```xml
<serviceTask id="javaService"
             name="My Java Service Task"
             cadenzaflow:class="org.cadenzaflow.bpm.MyJavaDelegate" />
```

Please refer to the [Java Delegate]({{< ref "/user-guide/process-engine/delegation-code.md#java-delegate" >}}) section of the [User Guide]({{< ref "/user-guide/_index.md" >}}) for details on how to implement a Java Delegate.

It is also possible to use an expression that resolves to an object. This object must follow the
same rules as objects that are created when the `cadenzaflow:class` attribute is used.

```xml
<serviceTask id="beanService"
             name="My Bean Service Task"
             cadenzaflow:delegateExpression="${myDelegateBean}" />
```

Or an expression which calls a method or resolves to a value.

```xml
<serviceTask id="expressionService"
             name="My Expression Service Task"
             cadenzaflow:expression="${myBean.doWork()}" />
```

For more information about expression language as delegation code, please see the corresponding
[section]({{< ref "/user-guide/process-engine/expression-language/unified-expression-language.md#delegation-code" >}})
of the [User Guide]({{< ref "/user-guide/_index.md" >}}).

It is also possible to invoke logic which is implemented in form of webservices. `cadenzaflow:connector` is an extension that allows calling REST/SOAP APIs directly from the workflow. For more information about using connectors, please see the corresponding [section]({{< ref "/user-guide/process-engine/connectors.md#use-connectors" >}}) of the [User Guide]({{< ref "/user-guide/_index.md" >}})

## Generic Java Delegates & Field Injection

You can easily write generic Java Delegate classes which can be configured later on via the BPMN 2.0 XML in the Service Task. Please refer to the [Field Injection]({{< ref "/user-guide/process-engine/delegation-code.md#field-injection" >}}) section of the [User Guide]({{< ref "/user-guide/_index.md" >}}) for details.


## Service Task Results

The return value of a service execution (for a Service Task exclusively using expressions) can be assigned to an already existing or to a new process variable by specifying the process variable name as a literal value for the `cadenzaflow:resultVariable` attribute of a Service Task definition. Any existing value for a specific process variable will be overwritten by the result value of the service execution. When not specifying a result variable name, the service execution result value is ignored.

```xml
<serviceTask id="aMethodExpressionServiceTask"
           cadenzaflow:expression="#{myService.doSomething()}"
           cadenzaflow:resultVariable="myVar" />
```

In the example above, the result of the service execution (the return value of the `doSomething()` method invocation on object `myService`) is set to the process variable named `myVar` after the service execution completes.

{{< note title="Result variables and multi-instance" class="warning" >}}
Note that when you use <code>cadenzaflow:resultVariable</code> in a multi-instance construct, for example in a multi-instance subprocess, the result variable is overwritten every time the task completes, which may appear as random behavior. See <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#resultvariable" >}}">cadenzaflow:resultVariable</a> for details.
{{< /note >}}

# External Tasks

In contrast to calling Java code, where the process engine synchronously invokes Java logic, it is possible to implement a Service Task outside of the process engine's boundaries in the form of an external task. When a Service Task is declared external, the process engine offers a work item to workers that independently poll the engine for work to do. This decouples the implementation of tasks from the process engine and allows to cross system and technology boundaries. See the [user guide on external tasks]({{< ref "/user-guide/process-engine/external-tasks.md" >}}) for details on the concept and the relevant API.

To declare a Service Task to be handled externally, the attribute `cadenzaflow:type` can be set to `external` and the attribute `cadenzaflow:topic` specifies the external task's topic. For example, the following XML snippet defines an external Service Task with topic `ShipmentProcessing`:

```xml
<serviceTask id="anExternalServiceTask"
           cadenzaflow:type="external"
           cadenzaflow:topic="ShipmentProcessing" />
```

# CadenzaFlow Extensions

<table class="table table-striped">
  <tr>
    <th>Attributes</th>
    <td>
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#asyncbefore" >}}">cadenzaflow:asyncBefore</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#asyncafter" >}}">cadenzaflow:asyncAfter</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#class" >}}">cadenzaflow:class</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#delegateexpression" >}}">cadenzaflow:delegateExpression</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#exclusive" >}}">cadenzaflow:exclusive</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#expression" >}}">cadenzaflow:expression</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#jobpriority" >}}">cadenzaflow:jobPriority</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#resultvariable" >}}">cadenzaflow:resultVariable</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#topic" >}}">cadenzaflow:topic</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#type" >}}">cadenzaflow:type</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#taskpriority" >}}">cadenzaflow:taskPriority</a>
    </td>
  </tr>
  <tr>
    <th>Extension Elements</th>
    <td>
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-elements.md#erroreventdefinition" >}}">cadenzaflow:errorEventDefinition</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-elements.md#failedjobretrytimecycle" >}}">cadenzaflow:failedJobRetryTimeCycle</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-elements.md#field" >}}">cadenzaflow:field</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-elements.md#connector" >}}">cadenzaflow:connector</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-elements.md#inputoutput" >}}">cadenzaflow:inputOutput</a>
    </td>
  </tr>
  <tr>
    <th>Constraints</th>
    <td>
      One of the attributes <code>cadenzaflow:class</code>, <code>cadenzaflow:delegateExpression</code>,
      <code>cadenzaflow:type</code> or <code>cadenzaflow:expression</code> is mandatory
    </td>
  </tr>
  <tr>
    <td></td>
    <td>
      The attribute <code>cadenzaflow:resultVariable</code> can only be used in combination with the
      <code>cadenzaflow:expression</code> attribute
    </td>
  </tr>
  <tr>
    <td></td>
    <td>
      The <code>cadenzaflow:exclusive</code> attribute is only evaluated if the attribute
      <code>cadenzaflow:asyncBefore</code> or <code>cadenzaflow:asyncAfter</code> is set to <code>true</code>
    </td>
  </tr>
  <tr>
    <td></td>
    <td>
      The attribute <code>cadenzaflow:topic</code> can only be used when the <code>cadenzaflow:type</code> attribute is set to <code>external</code>.
    </td>
  </tr>
  <tr>
    <td></td>
    <td>
      The attribute <code>cadenzaflow:taskPriority</code> can only be used when the <code>cadenzaflow:type</code> attribute is set to <code>external</code>.
    </td>
  </tr>
  <tr>
    <td></td>
    <td>
      The element <code>cadenzaflow:errorEventDefinition</code> can only be used as a child of <code>serviceTask</code> when the <code>cadenzaflow:type</code> attribute is set to <code>external</code>.
    </td>
  </tr>
</table>


# Additional Resources

* [Tasks](http://cadenzaflow.org/bpmn/reference.html#activities-task) in the [BPMN Modeling Reference](http://cadenzaflow.org/bpmn/reference.html) section
* [How to call a Webservice from BPMN](http://www.bpm-guide.de/2010/12/09/how-to-call-a-webservice-from-bpmn/). Please note that this article is outdated. However, it is still valid regarding how you would call a Web Service using the process engine.
