---
title: Maven Usage in engine-plugins
---
This document provides a detailed explanation of how Maven is used in the `engine-plugins` directory of the Citi-camunda project. It will cover the configuration and usage of Maven in this context, with a focus on the `pom.xml` file.

<SwmSnippet path="/engine-plugins/pom.xml" line="4">

---

# Parent Project Configuration

The `parent` tag is used to indicate the parent project from which this project inherits. The `groupId`, `artifactId`, and `version` tags specify the parent project's coordinates. The `relativePath` tag is used to locate the parent project's POM file.

```xml
  <parent>
    <groupId>org.camunda.bpm</groupId>
    <artifactId>camunda-database-settings</artifactId>
    <relativePath>../database</relativePath>
    <version>7.22.0-SNAPSHOT</version>
  </parent>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-plugins/pom.xml" line="11">

---

# Project Artifact Configuration

The `artifactId` tag is used to uniquely identify the project artifact. The `packaging` tag specifies the type of artifact to be generated. The `name` tag provides a human-readable name for the project.

```xml
  <artifactId>camunda-engine-plugins</artifactId>
  <packaging>pom</packaging>

  <name>Camunda Platform - engine plugins</name>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-plugins/pom.xml" line="16">

---

# Modules Configuration

The `modules` tag is used to specify the modules that make up this project. Each `module` tag represents a child project.

```xml
  <modules>
    <module>identity-ldap</module>
    <module>connect-plugin</module>
    <module>spin-plugin</module>
  </modules>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-plugins/pom.xml" line="22">

---

# Dependency Management

The `dependencyManagement` tag is used to manage the versions of dependencies. The `dependencies` tag within it contains `dependency` tags that specify the `groupId`, `artifactId`, `version`, `scope`, and `type` of each dependency.

```xml
  <dependencyManagement>
    <dependencies>
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
        <version>${version.xml.jaxb-impl}</version>
      </dependency>
    </dependencies>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-plugins/pom.xml" line="39">

---

# Dependencies Configuration

The `dependencies` tag is used to specify the dependencies required by this project. Each `dependency` tag represents a dependency and specifies its `groupId`, `artifactId`, `scope`, and `version`.

```xml
  <dependencies>
    <dependency>
      <groupId>org.camunda.bpm</groupId>
      <artifactId>camunda-engine</artifactId>
      <scope>provided</scope>
    </dependency>

    <dependency>
      <groupId>com.h2database</groupId>
      <artifactId>h2</artifactId>
      <scope>test</scope>
    </dependency>

    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <scope>test</scope>
    </dependency>

    <dependency>
      <groupId>org.assertj</groupId>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
