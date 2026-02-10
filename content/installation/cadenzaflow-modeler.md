---

title: "Install the CadenzaFlow Modeler"
weight: 01

menu:
  main:
    name: "CadenzaFlow Modeler"
    identifier: "installation-guide-modeler"
    parent: "installation-guide"
    pre: "Install the CadenzaFlow Modeler for BPMN 2.0, DMN 1.3 and CadenzaFlow Forms"

---

This page explains how to install the CadenzaFlow Modeler for modeling BPMN 2.0 diagrams, DMN 1.3 decision tables and CadenzaFlow Forms.

# Requirements

## Operation Systems

Officially supported on the following operating systems:

* Windows 7 / 10
* Mac OS X 10.11 and later
* Ubuntu LTS (latest)

Reported to work on these operating systems, too:

* Ubuntu 12.04 and later
* Fedora 21
* Debian 8

{{< meta-comment "this is based on our testing environment and the Electron documentation (https://electronjs.org/docs/tutorial/support)" >}}


## Matching CadenzaFlow Process Engine Version

For executing BPMN Diagrams created using CadenzaFlow Modeler, Process Engine version 1.0.0 and above is required.

For evaluating DMN 1.3 Decisions created using CadenzaFlow Modeler, Process Engine version 1.0.0 and above is required.

For displaying CadenzaFlow Forms created using CadenzaFlow Modeler, Process Engine version 1.0.0 and above is required.

Note that you do not need to install the Process Engine if you do not want to execute the BPMN Diagrams or evaluate DMN Decisions.

# Download

Get the latest release from the [CadenzaFlow Modeler download page](https://cadenzaflow.com/download/).

# Install

Unpack the modeler into a location of your choice.

# Run the Application

Run the application via the executable `CadenzaFlow Modeler.exe` (Windows), `CadenzaFlow Modeler.app` (Mac) or `cadenzaflow-modeler` (Linux).

# Wire File Associations

On Windows and Linux you must carry out additional steps to register the modeler as the default editor for BPMN, DMN and CadenzaFlow Form files.

### Windows

To make the modeler the default editor for `.bpmn`, `.dmn` and `.form` files execute `support/register_fileassoc.bat`.

### Linux

To create a [desktop file](https://specifications.freedesktop.org/desktop-entry-spec/latest/) and make the modeler the default editor for `.bpmn`, `.dmn` and `.form` files execute `support/xdg_register.sh`.
