---
title: Maven Usage in engine-dmn/bom
---
This document provides a detailed walkthrough of how Maven is used in the `engine-dmn/bom` directory of the project.

<SwmSnippet path="/engine-dmn/bom/pom.xml" line="1">

---

# Project Configuration

The `pom.xml` file starts with the project configuration. It specifies the model version, parent artifact, and the artifact details for this project. The `artifactId` is `camunda-engine-dmn-bom` and it uses `pom` packaging.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <parent>
    <groupId>org.camunda.bpm</groupId>
    <artifactId>camunda-root</artifactId>
    <version>7.22.0-SNAPSHOT</version>
    <relativePath>../../</relativePath>
  </parent>

  <groupId>org.camunda.bpm.dmn</groupId>
  <artifactId>camunda-engine-dmn-bom</artifactId>
  <version>7.22.0-SNAPSHOT</version>
  <name>camunda DMN - engine - bom</name>
  <packaging>pom</packaging>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/bom/pom.xml" line="18">

---

# Dependency Management

The `dependencyManagement` section is used to manage the versions of various dependencies. It includes dependencies like `camunda-engine-dmn`, `camunda-engine-feel-api`, `camunda-engine-feel-juel`, and `camunda-engine-feel-scala`. All these dependencies are managed at a single place, and they all use the same version, which is the `${project.version}`.

```xml
  <dependencyManagement>
    <dependencies>

      <dependency>
        <groupId>org.camunda.bpm.dmn</groupId>
        <artifactId>camunda-engine-dmn</artifactId>
        <version>${project.version}</version>
      </dependency>

      <dependency>
        <groupId>org.camunda.bpm.dmn</groupId>
        <artifactId>camunda-engine-feel-api</artifactId>
        <version>${project.version}</version>
      </dependency>

      <dependency>
        <groupId>org.camunda.bpm.dmn</groupId>
        <artifactId>camunda-engine-feel-juel</artifactId>
        <version>${project.version}</version>
      </dependency>

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
