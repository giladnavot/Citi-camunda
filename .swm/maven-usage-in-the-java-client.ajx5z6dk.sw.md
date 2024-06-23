---
title: Maven Usage in the Java Client
---
This document provides a detailed walkthrough of how Maven is used in the `clients/java` directory of the project.

<SwmSnippet path="/clients/java/pom.xml" line="1">

---

# Root Maven Configuration

This is the root Maven configuration file for the Java client. It defines the project model version, the artifact ID, and the packaging type. It also specifies the parent project and the modules that make up this project. The `dependencyManagement` section is used to manage dependency versions. The `scm` section is used to connect to the source control management system.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">

  <modelVersion>4.0.0</modelVersion>
  <name>Camunda Platform - Java External Task Client - ROOT</name>

  <artifactId>camunda-external-task-client-root</artifactId>
  <inceptionYear>2018</inceptionYear>

  <packaging>pom</packaging>

  <parent>
    <groupId>org.camunda.bpm</groupId>
    <artifactId>camunda-database-settings</artifactId>
    <relativePath>../../database</relativePath>
    <version>7.22.0-SNAPSHOT</version>
  </parent>

  <modules>
    <module>qa</module>
    <module>client</module>
```

---

</SwmSnippet>

<SwmSnippet path="/clients/java/qa/pom.xml" line="1">

---

# QA Maven Configuration

This is the Maven configuration file for the QA module. It defines the group ID, the artifact ID, and the packaging type. It also specifies the parent project and the modules that make up this project.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">

  <modelVersion>4.0.0</modelVersion>
  <name>Camunda Platform - Java External Task Client - QA</name>

  <groupId>org.camunda.bpm.qa</groupId>
  <artifactId>camunda-external-task-client-qa</artifactId>

  <packaging>pom</packaging>

  <parent>
    <groupId>org.camunda.bpm</groupId>
    <artifactId>camunda-external-task-client-root</artifactId>
    <version>7.22.0-SNAPSHOT</version>
  </parent>

  <modules>
    <module>engine-variable-test</module>
  </modules>

```

---

</SwmSnippet>

<SwmSnippet path="/clients/java/client/src/it/java/org/camunda/bpm/client/client/ClientIT.java" line="513">

---

# ClientIT Class

This is a test class that uses the `ExternalTaskClient` class. The `shouldPerformAutoFetching` method tests the auto-fetching functionality of the client. It creates a client, checks if it's active, and then stops it.

```java
  }

  @Test
  public void shouldPerformAutoFetching() {
    ExternalTaskClient client = null;

    try {
      // given
      ExternalTaskClientBuilder clientBuilder = ExternalTaskClient.create()
        .baseUrl(BASE_URL);

      // when
      client = clientBuilder.build();

      // then
      assertThat(client.isActive()).isTrue();
    } finally {
      if (client != null) {
        client.stop();
      }
    }
```

---

</SwmSnippet>

<SwmSnippet path="/clients/java/client/src/main/java/org/camunda/bpm/client/ExternalTaskClient.java" line="34">

---

# ExternalTaskClient Class

This class provides a static `create` method to create a new instance of `ExternalTaskClientBuilder`. This builder can be used to configure and build an `ExternalTaskClient`.

```java
  static ExternalTaskClientBuilder create() {
    return new ExternalTaskClientBuilderImpl();
  }
```

---

</SwmSnippet>

<SwmSnippet path="/clients/java/client/src/main/java/org/camunda/bpm/client/ExternalTaskClientBuilder.java" line="34">

---

# ExternalTaskClientBuilder Class

This class provides a `baseUrl` method to set the base URL of the Camunda BPM Platform REST API. This information is mandatory for the client to function properly.

```java
  /**
   * Base url of the Camunda BPM Platform REST API. This information is mandatory.
   *
   * @param baseUrl of the Camunda BPM Platform REST API
   * @return the builder
   */
  ExternalTaskClientBuilder baseUrl(String baseUrl);
```

---

</SwmSnippet>

<SwmSnippet path="/clients/java/client/src/main/java/org/camunda/bpm/client/ExternalTaskClientBuilder.java" line="193">

---

# ExternalTaskClientBuilder Class

This class provides a `build` method to bootstrap the Camunda client. It throws an `ExternalTaskClientException` if any of the required configurations are missing or invalid.

```java
  /**
   * Bootstraps the Camunda client
   *
   * @throws ExternalTaskClientException
   * <ul>
   *   <li> if base url is null or string is empty
   *   <li> if hostname cannot be retrieved
   *   <li> if maximum amount of tasks is not greater than zero
   *   <li> if maximum asynchronous response timeout is not greater than zero
   *   <li> if lock duration is not greater than zero
   * </ul>
   * @return the builder
   */
  ExternalTaskClient build();
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
