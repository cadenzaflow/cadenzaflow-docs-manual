---

title: 'Extension Attributes'
weight: 60

menu:
  main:
    identifier: "user-guide-dmn-model-api-extension-attributes"
    parent: "user-guide-dmn-model-api"

---


[Custom extensions]({{< ref "/reference/dmn/custom-extensions/_index.md" >}}) are a standardized way to extend the DMN model.
The [CadenzaFlow extension attributes]({{< ref "/reference/dmn/custom-extensions/cadenzaflow-attributes.md" >}}) are fully implemented in the DMN model API.

Every DMN `Decision` element can have the attributes `historyTimeToLive` and `versionTag`.
To access the extension attributes, you have to call the `Decision#getCadenzaflowHistoryTimeToLiveString()` and 
`Decision#getVersionTag()` methods. 

```java
String historyTimeToLive = decision.getCadenzaflowHistoryTimeToLiveString();
String versionTag = decision.getVersionTag();
```
To set attributes, use `Decision#setCadenzaflowHistoryTimeToLiveString()` and `Decision#setVersionTag()`
```java
decision.setCadenzaflowHistoryTimeToLiveString("1000");
decision.setVersionTag("1.0.0");
```

Every `Input` element can have an `inputVariable` attribute.
This attribute specifies the variable name which can be used to access the result of the input expression in an input entry expression.
It can be set and fetched similarly, calling `Input#setCadenzaflowInputVariable()` and `Input#getCadenzaflowInputVariable()`:

```java
input.setCadenzaflowInputVariable("cadenzaflowInput");
String cadenzaflowInput = input.getCadenzaflowInputVariable();
```
