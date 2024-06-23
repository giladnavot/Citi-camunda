---
title: Maven Configuration in engine-rest
---
This document provides a detailed explanation of how Maven is used in the `engine-rest` module of the Camunda Platform. It will go through the configuration steps in the `engine-rest/pom.xml` file step by step.

<SwmSnippet path="/engine-rest/pom.xml" line="1">

---

# Project Information

The `pom.xml` file starts by defining the project and its parent. The parent project is `camunda-database-settings` which is located in the `database` directory. The artifactId for this project is `camunda-engine-rest-root`. The packaging type is `pom` and the name is `Camunda Platform - engine - REST - Root`.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <parent>
    <groupId>org.camunda.bpm</groupId>
    <artifactId>camunda-database-settings</artifactId>
    <relativePath>../database</relativePath>
    <version>7.22.0-SNAPSHOT</version>
  </parent>

  <artifactId>camunda-engine-rest-root</artifactId>

  <packaging>pom</packaging>
  <name>Camunda Platform - engine - REST - Root</name>

  <properties>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/pom.xml" line="16">

---

# Properties

The properties section defines versions for various dependencies that will be used in the project. These include `rest-assured`, `groovy`, `apache.httpcore`, and `commons-codec`.

```xml
  <properties>
    <version.rest-assured>4.5.0</version.rest-assured>
    <!-- override groovy version with the one used by rest-assured -->
    <version.groovy>3.0.9</version.groovy>
    <version.apache.httpcore>4.4.5</version.apache.httpcore>
    <version.commons-codec>1.15</version.commons-codec>
  </properties>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/pom.xml" line="24">

---

# Dependency Management

The `dependencyManagement` section is used to manage the versions of various dependencies in a central place. This includes dependencies like `groovy-bom`, `camunda-core-internal-dependencies`, `jaxb-impl`, `rest-assured`, `jackson-bom`, `httpcore`, and `commons-codec`.

```xml
  <dependencyManagement>
    <dependencies>
      <!-- explicitly declare groovy dependencies, so it prevents our groovy version
            from overriding the groovy version from rest-assured -->
      <dependency>
        <groupId>org.codehaus.groovy</groupId>
        <artifactId>groovy-bom</artifactId>
        <version>${version.groovy}</version>
        <scope>import</scope>
        <type>pom</type>
      </dependency>
      <dependency>
        <groupId>org.camunda.bpm</groupId>
        <artifactId>camunda-core-internal-dependencies</artifactId>
        <version>${project.version}</version>
        <scope>import</scope>
        <type>pom</type>
      </dependency>
      <dependency>
        <groupId>com.sun.xml.bind</groupId>
        <artifactId>jaxb-impl</artifactId>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/pom.xml" line="72">

---

# Modules

The `modules` section lists all the modules that make up this project. These include `engine-rest`, `engine-rest-jakarta`, `engine-rest-openapi`, `engine-rest-openapi-generator`, `assembly`, `assembly-jakarta`, and `docs`.

```xml
  <modules>
    <module>engine-rest</module>
    <module>engine-rest-jakarta</module>
    <module>engine-rest-openapi</module>
    <module>engine-rest-openapi-generator</module>
    <module>assembly</module>
    <module>assembly-jakarta</module>
    <module>docs</module>
  </modules>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
