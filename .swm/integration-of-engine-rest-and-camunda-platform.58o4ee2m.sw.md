---
title: Integration of engine-rest and Camunda Platform
---
This document will cover how the `engine-rest` component ties in with the Camunda Platform. We'll cover:

1. The role of `engine-rest` in the Camunda Platform
2. How `engine-rest` is implemented and used in the codebase
3. The interaction of `engine-rest` with other components.

# Role of `engine-rest` in the Camunda Platform

`engine-rest` is a crucial component of the Camunda Platform. It provides a REST API that allows external applications to interact with the Camunda process engine. This includes starting process instances, completing tasks, and querying for data.

<SwmSnippet path="/engine-rest/engine-rest/src/main/java/org/camunda/bpm/engine/rest/MigrationRestService.java" line="17">

---

# Implementation of `engine-rest`

The `engine-rest` component is implemented in various Java classes under the `org.camunda.bpm.engine.rest` package. For instance, `MigrationRestService` is one of the classes that provide REST endpoints for process migration.

```java
package org.camunda.bpm.engine.rest;

import javax.ws.rs.Consumes;
```

---

</SwmSnippet>

<SwmSnippet path="/spring-boot-starter/starter-rest/src/main/java/org/camunda/bpm/spring/boot/starter/rest/CamundaJerseyResourceConfig.java" line="26">

---

# Interaction of `engine-rest` with other components

`engine-rest` interacts with other components of the Camunda Platform. For example, in the Spring Boot Starter, the `CamundaJerseyResourceConfig` class configures the REST resources provided by `engine-rest`.

```java
@ApplicationPath("/engine-rest")
public class CamundaJerseyResourceConfig extends ResourceConfig implements InitializingBean {

  private static final Logger log = org.slf4j.LoggerFactory.getLogger(CamundaJerseyResourceConfig.class);

  @Override
  public void afterPropertiesSet() throws Exception {
    registerCamundaRestResources();
    registerAdditionalResources();
  }

  protected void registerCamundaRestResources() {
    log.info("Configuring camunda rest api.");

    this.registerClasses(CamundaRestResources.getResourceClasses());
    this.registerClasses(CamundaRestResources.getConfigurationClasses());
    this.register(JacksonFeature.class);

    log.info("Finished configuring camunda rest api.");
  }

```

---

</SwmSnippet>

<SwmSnippet path="/clients/java/client/src/it/java/org/camunda/bpm/client/util/PropertyUtil.java" line="27">

---

The `engine-rest` component is also used in the Java client for integration tests. The `CAMUNDA_ENGINE_REST` constant is used to specify the base URL of the `engine-rest` API.

```java
  public static final String DEFAULT_PROPERTIES_PATH = "integration-rules.properties";
  public static final String CAMUNDA_ENGINE_REST = "camunda.engine.rest";
  public static final String CAMUNDA_ENGINE_NAME = "camunda.engine.name";
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="follow-up"><sup>Powered by [Swimm](/)</sup></SwmMeta>
