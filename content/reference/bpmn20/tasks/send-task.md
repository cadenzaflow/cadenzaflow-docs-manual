---

title: 'Send Task'
weight: 20

menu:
  main:
    identifier: "bpmn-ref-tasks-send-task"
    parent: "bpmn-ref-tasks"
    pre: "Send a message."

---

A Send Task is used to send a message. In CadenzaFlow this is done by calling Java code.

The Send Task has the same behavior as a Service Task.

{{< bpmn-symbol type="send-task" >}}

```xml
<sendTask id="sendTask" cadenzaflow:class="org.cadenzaflow.bpm.MySendTaskDelegate" />
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
</table>
