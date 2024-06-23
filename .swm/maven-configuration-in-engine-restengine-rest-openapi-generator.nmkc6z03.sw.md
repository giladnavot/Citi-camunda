---
title: Maven Configuration in engine-rest/engine-rest-openapi-generator
---
This document provides a detailed explanation of how Maven is used in the `engine-rest/engine-rest-openapi-generator` directory of the project.

<SwmSnippet path="/engine-rest/engine-rest-openapi-generator/pom.xml" line="1">

---

# Maven Project Configuration

The `pom.xml` file defines the Maven project configuration. The `modelVersion` is set to `4.0.0`, which is the version of the Project Object Model (POM) that this project adheres to. The `artifactId` is `camunda-engine-rest-openapi-generator`, which is the unique identifier of this project artifact. The `name` is a human-readable name of the project. The `packaging` is set to `jar`, which means Maven will package the project as a JAR file.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <artifactId>camunda-engine-rest-openapi-generator</artifactId>
  <name>Camunda Platform - engine - REST - OpenAPI (JSON Generator)</name>
  <packaging>jar</packaging>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi-generator/pom.xml" line="7">

---

# Maven Parent Configuration

The `parent` element specifies the parent project from which this project inherits configuration. The `groupId` is `org.camunda.bpm`, the `artifactId` is `camunda-engine-rest-root`, and the `version` is `7.22.0-SNAPSHOT`. The `relativePath` is `../`, which is the location of the parent project relative to this project.

```xml
  <parent>
    <groupId>org.camunda.bpm</groupId>
    <artifactId>camunda-engine-rest-root</artifactId>
    <relativePath>../</relativePath>
    <version>7.22.0-SNAPSHOT</version>
  </parent>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi-generator/pom.xml" line="14">

---

# Maven Properties Configuration

The `properties` element defines project properties that can be referenced elsewhere in the POM. Here, the `version.json-schema-validator` property is defined with a value of `1.0.76`.

```xml
  <properties>
    <version.json-schema-validator>1.0.76</version.json-schema-validator>
  </properties>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi-generator/pom.xml" line="18">

---

# Maven Dependencies Configuration

The `dependencies` element lists all dependencies required by this project. Each `dependency` element specifies a dependency, with `groupId`, `artifactId`, and `version` elements defining the dependency coordinates. Dependencies include `freemarker` for template engine, `gson` for JSON formatting, `commons-io` for file management, and `json-schema-validator` for JSON schema validation.

```xml
  <dependencies>

    <dependency>
      <groupId>org.freemarker</groupId>
      <artifactId>freemarker</artifactId>
    </dependency>

    <!-- json formatting -->
    <dependency>
      <groupId>com.google.code.gson</groupId>
      <artifactId>gson</artifactId>
    </dependency>

    <!-- file management -->
    <dependency>
      <groupId>commons-io</groupId>
      <artifactId>commons-io</artifactId>
    </dependency>

    <!-- json schema validation -->
    <dependency>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
