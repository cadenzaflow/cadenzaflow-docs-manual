---

title: 'CadenzaFlow License Keys'
weight: 220

menu:
  main:
    identifier: "user-guide-license"
    parent: "user-guide"

---

Some CadenzaFlow features (e.g. enterprise plugins) require a license key. The license will be provided as a string by 
the CadenzaFlow support team. The license mechanism has no impact on the engine or other runtime components. The following 
section explains the various methods by which a CadenzaFlow license can be added to the Process Engine.


# Deployment Scenarios and the License Key

A CadenzaFlow license key should be applied per database.

In a clustered scenario, where multiple engines on multiple nodes access a single database, the 
license only needs to be activated once. When activated, a license is valid until the expiration 
date or until you have deleted your database. The license key is valid for an unlimited amount of 
engines.

In a multi tenancy scenario, the license check will be performed for each engine with an own 
database. Thus, you will be prompted to enter the license key separately for each engine.


# License Key Pickup Methods

## Through the Admin Webapp UI

Any environment setup that uses the enterprise CadenzaFlow Admin webapp, can use the provided License key page to
enter a valid license key. Please see the dedicated [Admin webapp]({{< ref "/webapps/admin/system-management.md#cadenzaflow-license-key" >}}) 
docs section for more details.

## Through the Java API

This method can be used in any environment setup. The license key can be set via the 
Java API by calling:

```
managementService.setLicenseKey(String licenseKey);
```

The managementService also offers methods to get and delete the license key from the database.
The license key is stored in the `ACT_GE_BYTEARRAY` table. A reference to the license entry can 
be found in the `ACT_GE_PROPERTY` table (`cadenzaflow-license-key-id`).

## Through the Home Directory

Another possibility is to put a file with the license key on the path `${user.home}/.cadenzaflow/license.txt`. 
This is another method that can be applied in any environment setup. The license key will be 
automatically loaded in the database table unless a valid license key is already present.

## With the CadenzaFlow Spring Boot Starter & CadenzaFlow Run

CadenzaFlow Run, and other Spring Boot applications that use the CadenzaFlow Spring Boot Starter, can be provided with license  keys in two additional ways:

* provide a URL to a license file via a custom [Spring Property]({{< ref "/user-guide/spring-boot-integration/configuration.md#license-file" >}}).
* provide the license key in a file called `cadenzaflow-license.txt` which is on the classpath of the application.

**Note:** For these two properties to be available, the CadenzaFlow Run EE edition must be used, or the Spring Boot 
application must use the **`cadenzaflow-bpm-spring-boot-starter-webapp-ee`** module.

```xml
<dependency>
  <groupId>org.cadenzaflow.bpm.springboot</groupId>
  <artifactId>cadenzaflow-bpm-spring-boot-starter-webapp-ee</artifactId>
</dependency>
```



# License content

This section defines what is a valid license key that will be accepted by the Process Engine. This description is 
valid for all [License pickup methods](#license-key-pickup-methods).

A valid license key content should include the following:

1. The header section:
    ```
    --------------- BEGIN CadenzaFlow BPM LICENSE KEY ---------------
    ``` 
1. The encrypted license key.

1. The unencrypted customer, expiry date and product data.

1. The footer section:
    ```
    ---------------  END CadenzaFlow BPM LICENSE KEY  ---------------
    ```

Note that omitting one of these sections will result in an error, and you will have to re-enter your
license key in the correct format.