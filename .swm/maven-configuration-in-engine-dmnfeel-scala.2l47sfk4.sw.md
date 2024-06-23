---
title: Maven Configuration in engine-dmn/feel-scala
---
This document provides a detailed walkthrough of how Maven is used in the `engine-dmn/feel-scala` directory of the project.

<SwmSnippet path="/engine-dmn/feel-scala/pom.xml" line="1">

---

# Project Configuration

The project is defined with the model version 4.0.0. It is a child of the `camunda-engine-dmn-root` artifact from the `org.camunda.bpm.dmn` group. The artifact id for this project is `camunda-engine-feel-scala` and it is named `camunda DMN - engine FEEL - SCALA`. The property `camunda.artifact` is set to `org.camunda.bpm.dmn.feel.impl.scala`.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <parent>
    <groupId>org.camunda.bpm.dmn</groupId>
    <artifactId>camunda-engine-dmn-root</artifactId>
    <version>7.22.0-SNAPSHOT</version>
  </parent>

  <artifactId>camunda-engine-feel-scala</artifactId>
  <name>camunda DMN - engine FEEL - SCALA</name>
  <properties>
    <camunda.artifact>org.camunda.bpm.dmn.feel.impl.scala</camunda.artifact>
  </properties>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-scala/pom.xml" line="15">

---

# Dependencies

The project has several dependencies. The `feel-engine` from `org.camunda.feel` is included with the `scala-shaded` classifier. It also depends on `camunda-engine-feel-api` from `org.camunda.bpm.dmn`. For testing, it uses `logback-classic` from `ch.qos.logback`, `junit` from `junit`, `mockito-core` from `org.mockito`, and `assertj-core` from `org.assertj`.

```xml
  <dependencies>

    <dependency>
      <groupId>org.camunda.feel</groupId>
      <artifactId>feel-engine</artifactId>
      <classifier>scala-shaded</classifier>
    </dependency>

    <dependency>
      <groupId>org.camunda.bpm.dmn</groupId>
      <artifactId>camunda-engine-feel-api</artifactId>
    </dependency>

    <dependency>
      <groupId>ch.qos.logback</groupId>
      <artifactId>logback-classic</artifactId>
      <scope>test</scope>
    </dependency>

    <dependency>
      <groupId>junit</groupId>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-scala/pom.xml" line="53">

---

# Build Configuration

The build configuration uses the `maven-bundle-plugin` from `org.apache.felix`. It has two executions. The first execution is during the `generate-sources` phase and it runs the `cleanVersions` goal. The second execution is during the `process-classes` phase and it runs the `manifest` goal.

```xml
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.felix</groupId>
        <artifactId>maven-bundle-plugin</artifactId>
        <executions>
          <execution>
            <phase>generate-sources</phase>
            <goals>
              <goal>cleanVersions</goal>
            </goals>
          </execution>
          <execution>
            <id>bundle-manifest</id>
            <phase>process-classes</phase>
            <goals>
              <goal>manifest</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
