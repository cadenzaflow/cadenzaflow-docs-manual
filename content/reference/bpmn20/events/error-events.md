---

title: 'Error Events'
weight: 50

menu:
  main:
    identifier: "bpmn-ref-events-error-events"
    parent: "bpmn-ref-events"
    pre: "Events catching / throwing errors."
---

Error events are events which are triggered by a defined error.

<div data-bpmn-diagram="../bpmn/event-error"></div>


# Business Errors vs. Technical Errors

A BPMN error is meant for business errors - which are different than technical exceptions. So, this is different than Java exceptions - which are, by default, handled in their own way.

You might also want to check out the basics of [Threading and Transactions]({{< ref "/user-guide/process-engine/transactions-in-processes.md#transaction-boundaries" >}}) in the [User Guide]({{< ref "/user-guide/_index.md" >}}) first.


# Defining an Error

An error event definition references an error element. The following is an example of an error end event, referencing an error declaration:

```xml
<definitions>
  <error id="myError" errorCode="ERROR-OCCURED" name="ERROR-OCCURED"/>
  <!-- ... -->
  <process>
    <!-- ... -->
    <endEvent id="myErrorEndEvent">
      <errorEventDefinition errorRef="myError" />
    </endEvent>
  </process>
</definitions>
```

You can trigger this error event either with a throwing error event within your process definition or from Delegation Code, see the
[Throwing BPMN Errors from Delegation Code]({{< ref "/user-guide/process-engine/delegation-code.md#throw-bpmn-errors-from-delegation-code" >}}) section of the [User Guide]({{< ref "/user-guide/_index.md" >}}) for more information.

Another possibility to define an error is setting of the type (class name) of any Java Exception as error code. Example:

```xml
<definitions>
  <error id="myException" errorCode="com.company.MyBusinessException" 
      name="myBusinessException"/>
  <!-- ... -->
  <process>
    <!-- ... -->
    <endEvent id="myErrorEndEvent">
      <errorEventDefinition errorRef="myException" />
    </endEvent>
  </process>
</definitions>
```

The exception type should only be used for business exceptions and not for technical exceptions in the process.

An error event handler references the same error element to declare that it catches the error.

It is also possible to define an error message with the <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#errormessage" >}}">`cadenzaflow:errorMessage`</a> extension for an error element to give further information about the error.
The referencing error event definition must specify <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#errormessagevariable" >}}">`cadenzaflow:errorMessageVariable`</a> to receive the error message. The error message can also contain <a href="{{< ref "/user-guide/process-engine/expression-language/unified-expression-language.md" >}}">expressions</a>.

```xml
<definitions>
  <error id="myError" errorCode="ERROR-OCCURED" name="ERROR-OCCURED" 
      cadenzaflow:errorMessage="Something went wrong: ${errorCause}" />
  <!-- ... -->
  <process>
    <!-- ... -->
    <endEvent id="myErrorEndEvent">
      <errorEventDefinition errorRef="myError" cadenzaflow:errorMessageVariable="err"/>
    </endEvent>
  </process>
</definitions>
```
When the error thrown by the error end event is catched a process variable with the name `err` will be created that holds the evaluated message.

For External Tasks, it is also possible to define error events by using a [cadenzaflow:errorEventDefinition]({{< ref "/reference/bpmn20/custom-extensions/extension-elements.md#erroreventdefinition" >}}) as shown in the following example. It additionally requires an expression that must evaluate to `true` in order for the BPMN error to be thrown. For further details on how to use those error events, consult the [External Tasks Guide]({{< ref "/user-guide/process-engine/external-tasks.md#error-event-definitions" >}}).

```xml
<serviceTask id="validateAddressTask"
  name="Validate Address"
  cadenzaflow:type="external"
  cadenzaflow:topic="AddressValidation" >
  <extensionElements>
    <cadenzaflow:errorEventDefinition id="addressErrorDefinition" 
      errorRef="addressError" 
      expression="${externalTask.getErrorDetails().contains('address error found')}" />
  </extensionElements>
</serviceTask>
```

# Error Start Event

An error start event can only be used to trigger an Event Sub-Process - it __cannot__ be used to start a process instance. The error start event is always interrupting.

<div data-bpmn-diagram="../bpmn/event-subprocess-alternative1"></div>

Three optional attributes can be added to the error start event: <code>errorRef</code>, <code>cadenzaflow:errorCodeVariable</code> and <code>cadenzaflow:errorMessageVariable</code>:
```xml
<definitions>
  <error id="myException" errorCode="com.company.MyBusinessException" name="myBusinessException"/>
  ...
  <process>
    ...
    <subProcess id="SubProcess_1" triggeredByEvent="true">>
      <startEvent id="myErrorStartEvent">
        <errorEventDefinition errorRef="myException" cadenzaflow:errorCodeVariable="myErrorVariable"
  		  cadenzaflow:errorMessageVariable="myErrorMessageVariable" />
      </startEvent>
    ...
    </subProcess>
  ...
  </process>
</definitions>
```
* If `errorRef` is omitted, the subprocess will start for every error event that occurs.
* The `cadenzaflow:errorCodeVariable` will contain the error code that was specified with the error. 
* The `cadenzaflow:errorMessageVariable` will contain the error message that was specified with the error.

`cadenzaflow:errorCodeVariable` and `cadenzaflow:errorMessageVariable` can be retrieved like any other process variable, but only if the attribute was set.


# Error End Event

When process execution arrives at an error end event, the current path of execution is ended and an error is thrown. This error can be caught by a matching intermediate error boundary event. In case no matching error boundary event is found, the execution semantics defaults to the none end event semantics.

## CadenzaFlow Extensions

### Error Event Definition

<table class="table table-striped">
  <tr>
    <th>Attributes</th>
    <td>
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#asyncbefore" >}}">cadenzaflow:asyncBefore</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#asyncafter" >}}">cadenzaflow:asyncAfter</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#errorcodevariable" >}}">cadenzaflow:errorCodeVariable</a>,
	  <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#errormessagevariable" >}}">cadenzaflow:errorMessageVariable</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#exclusive" >}}">cadenzaflow:exclusive</a>,
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#jobpriority" >}}">cadenzaflow:jobPriority</a>
    </td>
  </tr>
  <tr>
    <th>Extension Elements</th>
    <td>
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-elements.md#inputoutput" >}}">cadenzaflow:inputOutput</a>
    </td>
  </tr>
  <tr>
    <th>Constraints</th>
    <td>&ndash;</td>
  </tr>
</table>

### Error Definition

<table class="table table-striped">
  <tr>
    <th>Attributes</th>
    <td>
      <a href="{{< ref "/reference/bpmn20/custom-extensions/extension-attributes.md#errormessage" >}}">cadenzaflow:errorMessage</a>
    </td>
  </tr>
  <tr>
    <th>Extension Elements</th>
    <td>&ndash;</td>
  </tr>
  <tr>
    <th>Constraints</th>
    <td>&ndash;</td>
  </tr>
</table>


# Error Boundary Event

An intermediate catching error event on the boundary of an activity, or error boundary event for short, catches errors that are thrown within the scope of the activity on which it is defined.

Defining a error boundary event makes most sense on an embedded subprocess, or a call activity, as a subprocess creates a scope for all activities inside the subprocess. Errors are thrown by error end events. Such an error will propagate its parent scopes upwards until a scope is found on which a error boundary event is defined that matches the error event definition.

When an error event is caught, the activity on which the boundary event is defined is destroyed, also destroying all current executions therein (e.g., concurrent activities, nested subprocesses, etc.). Process execution continues following the outgoing sequence flow of the boundary event.

<div data-bpmn-diagram="../bpmn/event-subprocess-alternative2"></div>

A error boundary event is defined as a typical boundary event. As with the other error events, the errorRef references an error defined outside of the process element:

```xml
<definitions>
  <error id="myError" errorCode="ERROR-OCCURED" name="name of error"/>
  <!-- ... -->
  <process>
    <!-- ... -->
    <subProcess id="mySubProcess">
      <!-- ... -->
    </subProcess>
    <boundaryEvent id="catchError" attachedToRef="mySubProcess">
      <errorEventDefinition errorRef="myError" cadenzaflow:errorCodeVariable="myErrorVariable"
	    cadenzaflow:errorMessageVariable="myErrorMessageVariable" />
    </boundaryEvent>
  </process>
</definitions>
```

The errorCode is used to match the errors that are caught:

*   If errorRef is omitted, the error boundary event will catch any error event, regardless of the errorCode of the error.
*   In case an errorRef is provided and it references an existing error, the boundary event will only catch errors with the defined error code.
*   If the errorCodeVariable is set, the error code can be retrieved using this variable.
*   If the errorMessageVariable is set, the error message can be retrieved using this variable.


# Unhandled BPMN Error

It can happen that no catching boundary event was defined for an error event. The default behaviour in this case is to log information and end the current execution.
This behaviour can be changed with <code>enableExceptionsAfterUnhandledBpmnError</code> property set to <code>true</code> 
(via the process engine configuration or the deployment descriptor) and Process Engine Exception will be thrown if unhandled BPMN Error occurs.


# Catch and Re-Throw Pattern

An error can be handled by the error start event in the event sub process and the same error can be thrown from the event sub process to handle the error on the higher level scope (in the example  below, the error thrown from the Event Subprocess is handled by the error boundary event in the Subprocess). 

<div data-bpmn-diagram="../bpmn/catchandthrowpattern"></div>

## Additional Resources

*   [Error Events](http://cadenzaflow.org/bpmn/reference.html#events-error) in the [BPMN 2.0 Modeling Reference](http://cadenzaflow.org/bpmn/reference.html)
*   [Incidents]({{< ref "/user-guide/process-engine/incidents.md" >}}) in the [User Guide]({{< ref "/user-guide/_index.md" >}})
