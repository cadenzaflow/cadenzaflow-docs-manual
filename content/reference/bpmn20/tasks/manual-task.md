---

title: 'Manual Task'
weight: 70

menu:
  main:
    identifier: "bpmn-ref-tasks-manual-task"
    parent: "bpmn-ref-tasks"
    pre: "A task which is performed externally."

---

A Manual Task defines a task that is external to the BPM engine. It is used to model work that is done by somebody who the engine does not need to know of and that has no known system or UI interface. For the engine, a manual task is handled as a pass-through activity, automatically continuing the process when the process execution arrives at it.

{{< bpmn-symbol type="manual-task" >}}

```xml
<manualTask id="myManualTask" name="Manual Task" />
```


# CadenzaFlow Extensions

<table class="table table-striped">
  <tr>
    <th>Attributes</th>
    <td>
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#asyncbefore" >}}">cadenzaflow:asyncBefore</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#asyncafter" >}}">cadenzaflow:asyncAfter</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#exclusive" >}}">cadenzaflow:exclusive</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#jobpriority" >}}">cadenzaflow:jobPriority</a>
    </td>
  </tr>
  <tr>
    <th>Extension Elements</th>
    <td>
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-elements.md#failedjobretrytimecycle" >}}">cadenzaflow:failedJobRetryTimeCycle</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-elements.md#inputoutput" >}}">cadenzaflow:inputOutput</a>
    </td>
  </tr>
  <tr>
    <th>Constraints</th>
    <td>
      The <code>cadenzaflow:exclusive</code> attribute is only evaluated if the attribute
      <code>cadenzaflow:asyncBefore</code> or <code>cadenzaflow:asyncAfter</code> is set to <code>true</code>
    </td>
  </tr>
</table>
