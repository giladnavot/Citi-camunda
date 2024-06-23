---
title: Maven Usage in engine-plugins/connect-plugin
---
This document provides a detailed explanation of how Maven is used in the `engine-plugins/connect-plugin` directory of the project.

<SwmSnippet path="/engine-plugins/connect-plugin/pom.xml" line="1">

---

# Maven Project Configuration

The `pom.xml` file starts by defining the project as a Maven project. It specifies the parent artifact as `camunda-engine-plugins` and sets the model version to `4.0.0`. The artifact for this project is identified as `camunda-engine-plugin-connect`.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">

  <parent>
    <artifactId>camunda-engine-plugins</artifactId>
    <groupId>org.camunda.bpm</groupId>
    <version>7.22.0-SNAPSHOT</version>
  </parent>
  <modelVersion>4.0.0</modelVersion>

  <artifactId>camunda-engine-plugin-connect</artifactId>
  <name>Camunda Platform - engine plugins - connect</name>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-plugins/connect-plugin/pom.xml" line="14">

---

# Dependencies

The `pom.xml` file specifies the dependencies required for the project. These include `camunda-connect-core`, `camunda-connect-http-client`, `camunda-connect-soap-http-client`, and others. The scope of some dependencies is set to `test`, indicating that they are only required for testing.

```xml
  <dependencies>

    <dependency>
      <groupId>org.camunda.connect</groupId>
      <artifactId>camunda-connect-core</artifactId>
      <version>${project.version}</version>
    </dependency>

    <dependency>
      <groupId>org.camunda.connect</groupId>
      <artifactId>camunda-connect-http-client</artifactId>
      <version>${project.version}</version>
      <scope>test</scope>
    </dependency>

    <dependency>
      <groupId>org.camunda.connect</groupId>
      <artifactId>camunda-connect-soap-http-client</artifactId>
      <version>${project.version}</version>
      <scope>test</scope>
    </dependency>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-plugins/connect-plugin/pom.xml" line="68">

---

# Build Configuration

The build configuration is defined in the `build` section. It uses the `maven-surefire-plugin` for running tests and configures it to redirect test output to a file.

```xml
  <build>
    <plugins>
      <plugin>
        <artifactId>maven-surefire-plugin</artifactId>
        <configuration>
          <redirectTestOutputToFile>true</redirectTestOutputToFile>
        </configuration>
      </plugin>
    </plugins>
  </build>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
