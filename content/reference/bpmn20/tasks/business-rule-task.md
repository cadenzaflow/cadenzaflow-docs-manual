---

title: 'Business Rule Task'
weight: 40

menu:
  main:
    identifier: "bpmn-ref-tasks-business-rule-task"
    parent: "bpmn-ref-tasks"
    pre: "Execute an automated business decision."

---

A Business Rule Task is used to synchronously execute one or more rules. It is also possible to call Java code or providing a work item for an external worker to complete asynchronously or invoking a logic which is implemented in form of webservices.

{{< bpmn-symbol type="business-rule-task" >}}


# Using CadenzaFlow DMN Engine

You can use the CadenzaFlow DMN engine integration to evaluate a DMN decision. You have
to specify the decision key to evaluate as the `cadenzaflow:decisionRef` attribute. Additionally, 
the `cadenzaflow:decisionRefBinding` specifies which version of the decision should be evaluated.
Valid values are:

* `deployment`, which evaluates the decision version which was deployed with the process
version,
* `latest` which will always evaluate the latest decision version,
* `version` which allows you to specify a specific version to execute with the `cadenzaflow:decisionRefVersion` attribute, and
* `versionTag` which allows you to specify a specific version tag to execute with the `cadenzaflow:decisionRefVersionTag` attribute.

```xml
<businessRuleTask id="businessRuleTask"
    cadenzaflow:decisionRef="myDecision"
    cadenzaflow:decisionRefBinding="version"
    cadenzaflow:decisionRefVersion="12" />
```

The `cadenzaflow:decisionRefBinding` attribute defaults to `latest`.

```xml
<businessRuleTask id="businessRuleTask"
    cadenzaflow:decisionRef="myDecision" />
```

The attributes `cadenzaflow:decisionRef`, `cadenzaflow:decisionRefVersion`, and `cadenzaflow:decisionRefVersionTag` can be specified as
an expression which will be evaluated on execution of the task.

```xml
<businessRuleTask id="businessRuleTask"
    cadenzaflow:decisionRef="${decisionKey}"
    cadenzaflow:decisionRefBinding="version"
    cadenzaflow:decisionRefVersion="${decisionVersion}" />
```

The output of the decision, also called decision result, is not saved as process variable automatically. It has to pass into a process variable by using a [predefined]({{< ref "/user-guide/process-engine/decisions/bpmn-cmmn.md#predefined-mapping-of-the-decision-result" >}}) or a [custom]({{< ref "/user-guide/process-engine/decisions/bpmn-cmmn.md#custom-mapping-into-process-variables" >}}) mapping of the decision result.

In case of a predefined mapping, the `cadenzaflow:mapDecisionResult` attribute references the mapper to use. The result of the mapping is saved in the variable which is specified by the `cadenzaflow:resultVariable` attribute. If no predefined mapper is set then the `resultList` mapper is used by default.

```xml
<businessRuleTask id="businessRuleTask"
    cadenzaflow:decisionRef="myDecision"
    cadenzaflow:mapDecisionResult="singleEntry"
    cadenzaflow:resultVariable="result" />
```

See the [User Guide]({{< ref "/user-guide/process-engine/decisions/bpmn-cmmn.md#the-decision-result" >}}) for details about the mapping.

{{< note title="Name of the Result Variable" class="warning" >}}
The result variable should not have the name `decisionResult`, as the decision result itself is saved in a variable with this name. Otherwise, an exception is thrown while saving the result variable.
{{< /note >}}

# DecisionRef Tenant Id

When the Business Rule Task resolves the decision definition to be evaluated it must take multi tenancy into account.

## Default Tenant Resolution
By default, the tenant id of the calling process definition is used to evaluate the decision definition.
That is, if the calling process definition has no tenant id, then the Business Rule Task evaluates a decision definition using the provided key, binding and without a tenant id (tenant id = null).
If the calling process definition has a tenant id, a decision definition with the provided key and the same tenant id is evaluated.

Note that the tenant id of the calling process instance is not taken into account in the default behavior.

## Explicit Tenant Resolution

In some situations it may be useful to override this default behavior and specify the tenant id explicitly.

The `cadenzaflow:decisionRefTenantId` attribute allows to explicitly specify a tenant id:

```xml
<businessRuleTask id="businessRuleTask" decisionRef="myDecision"
  cadenzaflow:decisionRefTenantId="TENANT_1">
</businessRuleTask>
```

If the tenant id is not known at design time, an expression can be used as well:

```xml
<businessRuleTask id="businessRuleTask" decisionRef="myDecision"
  cadenzaflow:decisionRefTenantId="${ myBean.calculateTenantId(variable) }">
</businessRuleTask>
```

An expression also allows using the tenant id of the calling process instance instead of the calling process definition:

```xml
<businessRuleTask id="businessRuleTask" decisionRef="myDecision"
  cadenzaflow:decisionRefTenantId="${ execution.tenantId }">
</businessRuleTask>
```

# Using a Custom Rule Engine

You can integrate with other rule engines. To do so, you have to plug in your
implementation of the rule task the same way as in a Service Task.

```xml
<businessRuleTask id="businessRuleTask"
    cadenzaflow:delegateExpression="${MyRuleServiceDelegate}" />
```


# Using Delegate Code

Alternatively, a Business Rule Task can be implemented using Java Delegation just as a Service Task. For more
information on this please see the [Service Tasks]({{< relref "service-task.md" >}}) documentation.


# Implementing as an External Task

In addition to the above, a Business Rule Task can be implemented via the [External Task]({{< ref "/user-guide/process-engine/external-tasks.md" >}}) mechanism where an external system polls the process engine for work to do. See the section on [Service Tasks]({{< relref "service-task.md#external-tasks" >}}) for more information about how to configure an external task.


# CadenzaFlow Extensions

<table class="table table-striped">
  <tr>
    <th>Attributes</th>
    <td>
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#asyncbefore" >}}">cadenzaflow:asyncBefore</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#asyncafter" >}}">cadenzaflow:asyncAfter</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#class" >}}">cadenzaflow:class</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#decisionref" >}}">cadenzaflow:decisionRef</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#decisionrefbinding" >}}">cadenzaflow:decisionRefBinding</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#decisionreftenantid" >}}">cadenzaflow:decisionRefTenantId</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#decisionrefversion" >}}">cadenzaflow:decisionRefVersion</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#decisionrefversiontag" >}}">cadenzaflow:decisionRefVersionTag</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#delegateexpression" >}}">cadenzaflow:delegateExpression</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#exclusive" >}}">cadenzaflow:exclusive</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#expression" >}}">cadenzaflow:expression</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#jobpriority" >}}">cadenzaflow:jobPriority</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#mapdecisionresult" >}}">cadenzaflow:mapDecisionResult</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#resultvariable" >}}">cadenzaflow:resultVariable</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#topic" >}}">cadenzaflow:topic</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#type" >}}">cadenzaflow:type</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#taskpriority" >}}">cadenzaflow:taskPriority</a>
    </td>
  </tr>
  <tr>
    <th>Extension Elements</th>
    <td>
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-elements.md#failedjobretrytimecycle" >}}">cadenzaflow:failedJobRetryTimeCycle</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-elements.md#field" >}}">cadenzaflow:field</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-elements.md#connector" >}}">cadenzaflow:connector</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-elements.md#inputoutput" >}}">cadenzaflow:inputOutput</a>
    </td>
  </tr>
  <tr>
    <th>Constraints</th>
    <td>
      One of the attributes <code>cadenzaflow:class</code>, <code>cadenzaflow:delegateExpression</code>, <code>cadenzaflow:decisionRef</code>,
      <code>cadenzaflow:type</code> or <code>cadenzaflow:expression</code> is mandatory
    </td>
  </tr>
  <tr>
    <td></td>
    <td>
      The attribute <code>cadenzaflow:resultVariable</code> can only be used in combination with the
      <code>cadenzaflow:decisionRef</code> or <code>cadenzaflow:expression</code> attribute
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
</table>


# Additional Resources

* [Decisions]({{< ref "/user-guide/process-engine/decisions/_index.md" >}})
* [Service Tasks]({{< ref "/reference/bpmn20/tasks/service-task.md" >}})
* [Demo using Drools on the Business Rule Task](https://github.com/cadenzaflow/cadenzaflow-consulting/tree/master/one-time-examples/order-confirmation-rules)
