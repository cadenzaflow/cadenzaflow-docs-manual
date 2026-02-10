---

title: 'XLTS It Is'
weight: 20

menu:
  main:
    identifier: "xlts-itis"
    parent: "user-guide-introduction-third-party-libraries"
    pre: "XLTS It Is"

---

# XLTS It Is


[**XLTS** is a fork of AngularJS](https://xlts.dev/angularjs) that’s maintained by xlts.dev. By switching out the current AngularJS dependencies with XLTS, we can ensure that people using the web apps can continue to do so for years to come. Unlike AngularJS, which has an open source MIT license, XLTS has a proprietary license, meaning the source code is not freely available. 

There are several effects from implementing this approach, and it’s important to know the things that will be completely unaffected as well as what will change for some people:

1. First and foremost, CadenzaFlow Platform Community Edition and Enterprise Edition users shouldn’t be concerned about unsupported frameworks like AngularJS existing in their stack. By adding XLTS to the web apps, we can guarantee all of the people using the CadenzaFlow web apps will be supported for years to come.
2. The end-users of the CadenzaFlow web apps will feel no effect of this change at all. By continuing support for the existing framework, anyone currently using Cockpit, Tasklist, or Admin can expect a flawless transition.
3. The core component of CadenzaFlow Platform 1.x and CadenzaFlow Engine will go completely unaffected. Thanks to the decoupling of front-end components, the engine won’t even know there’s been a change.
4. If you’re redistributing CadenzaFlow yourself, you’re not affected. You can still wrap up the web apps as you did before without any changes. 
5. The new XLTS libraries are licensed under a proprietary license [the XLTS license] and thus CadenzaFlow users need to be aware of the terms of the XLTS license. The most important thing is the new libraries are bundled with the CadenzaFlow web applications, and the XLTS license will not permit the disassembly of these libraries into source code. CadenzaFlow source code is still available via [GitHub](https://github.com/cadenzaflow/cadenzaflow-bpm-platform/tree/master/webapps) – no changes there. If you build from that source code, it’ll compile with the original, out-of-support, AngularJS components; not the new XLTS components. Details of this will be added to our documentation.
6. This approach gives CadenzaFlow more flexibility in prototyping other possible solutions if we decide to move forward with a different solution to the AngularJS problem.
