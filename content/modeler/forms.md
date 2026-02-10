---

title: 'Building Forms in CadenzaFlow Modeler'
weight: 25

menu:
  main:
    name: "Forms"
    identifier: "cadenzaflow-modeler-forms"
    parent: "cadenzaflow-modeler"
    pre: "How to build CadenzaFlow Forms using the CadenzaFlow Modeler."

---

# Overview

The CadenzaFlow Forms feature allows you to easily design and configure forms. Once configured, they can be [connected to a User Task or Start Event]({{< ref "/user-guide/task-forms/_index.md#cadenzaflow-forms" >}}) so to implement a task form in your application.

# Quickstart

## Create new Form

To start building a form, in the **File** menu click **Create new Form (CadenzaFlow Platform or Cloud)**.

{{< img src="forms/img/create-form.png" title="Create new CadenzaFlow Form file" >}}

## Build your From

Now you can start to build your CadenzaFlow Form. Add the desired elements from the palette on the left hand side by dragging and dropping them onto the canvas.

{{< img src="forms/img/build-form.png" title="Drag and drop elements to build a CadenzaFlow Form" >}}

In the properties panel on the right hand side, you can view and edit attributes that apply to the currently selected form element. Please refer to the [CadenzaFlow Forms Reference]({{< ref "/reference/forms/cadenzaflow-forms/_index.md#configuration" >}}) to explore all configuration options for form elements.

{{< img src="forms/img/form-properties-panel.png" title="CadenzaFlow Form Properties Panel" >}}

## Save your Form

To save your state of work, click the **File > Save File As...** button in the top-level menu. Then select a location on your file system to store the form as `.form` file. You can load that file again by clicking **File > Open File...**.

## Connect your Form to a BPMN diagram

You can connect your CadenzaFlow Form to a User Task or Start Event, so to implement a task form in your application. Refer to the [User Task Forms guide]({{< ref "/user-guide/task-forms/_index.md#cadenzaflow-forms" >}}) to learn how.
