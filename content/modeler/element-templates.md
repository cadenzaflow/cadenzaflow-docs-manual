---

title: 'Use Element Templates to Extend the Modeler'
draft: true
weight: 28

menu:
  main:
    name: "Element Templates"
    identifier: "cadenzaflow-modeler-element-templates"
    parent: "cadenzaflow-modeler"
    pre: "Extend the modeler with custom elements."

---

{{< note class="info" title="Using Element Templates" >}}
Element Templates can be used with CadenzaFlow Modeler version 1.0 and higher. They are currently available in BPMN diagrams only.
{{< /note >}}



# Overview

Element templates are a way to extend the [CadenzaFlow Modeler](https://camunda.org/bpmn/tool/) with domain specific diagram elements such as service and user tasks.

{{< img src="img/overview.png" title="Custom fields in the CadenzaFlow Modeler" >}}

If applicable, element templates can be assigned to a diagram element via the properties panel.
Once applied, they configure the diagram element with pre-defined values for BPMN properties, input/output mappings as well as extension properties.

As seen in the _Mail Task_ example above the modeler allows properties of custom elements to be edited, too.


## Learn More

Refer to the following resources to learn more about element templates:

* [Element Template documentation](https://github.com/camunda/cadenzaflow-modeler/tree/master/docs/element-templates)
