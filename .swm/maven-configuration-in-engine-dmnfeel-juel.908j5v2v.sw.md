---
title: Maven Configuration in engine-dmn/feel-juel
---
This document provides a detailed walkthrough of how Maven is used in the `engine-dmn/feel-juel` module of the project.

<SwmSnippet path="/engine-dmn/feel-juel/pom.xml" line="1">

---

# Project Definition

The project is defined using the Maven POM (Project Object Model) version 4.0.0.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-juel/pom.xml" line="5">

---

# Parent Project

The parent project is defined as `camunda-engine-dmn-root` with version `7.22.0-SNAPSHOT`. This means that this module inherits the dependencies and plugins defined in the parent project.

```xml
  <parent>
    <groupId>org.camunda.bpm.dmn</groupId>
    <artifactId>camunda-engine-dmn-root</artifactId>
    <version>7.22.0-SNAPSHOT</version>
  </parent>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-juel/pom.xml" line="11">

---

# Artifact Information

The artifact produced by this module is `camunda-engine-feel-juel`. The `camunda.artifact` property is set to `org.camunda.bpm.dmn.feel.impl.juel`.

```xml
  <artifactId>camunda-engine-feel-juel</artifactId>
  <name>camunda DMN - engine FEEL - JUEL</name>

  <properties>
    <camunda.artifact>org.camunda.bpm.dmn.feel.impl.juel</camunda.artifact>
  </properties>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-juel/pom.xml" line="17">

---

# Dependencies

The module has several dependencies including `camunda-engine-feel-api`, `camunda-commons-logging`, `camunda-commons-typed-values`, `camunda-juel`, `junit`, and `assertj-core`. The versions for `camunda-commons-logging` and `camunda-commons-typed-values` are derived from the project version.

```xml
  <dependencies>
    <dependency>
      <groupId>org.camunda.bpm.dmn</groupId>
      <artifactId>camunda-engine-feel-api</artifactId>
    </dependency>

    <dependency>
      <groupId>org.camunda.commons</groupId>
      <artifactId>camunda-commons-logging</artifactId>
      <version>${project.version}</version>
    </dependency>

    <dependency>
      <groupId>org.camunda.commons</groupId>
      <artifactId>camunda-commons-typed-values</artifactId>
      <version>${project.version}</version>
    </dependency>

    <dependency>
      <groupId>org.camunda.bpm.juel</groupId>
      <artifactId>camunda-juel</artifactId>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-juel/pom.xml" line="54">

---

# Build Configuration

The build configuration includes the `maven-bundle-plugin` which is used to generate OSGi bundle metadata. The `cleanVersions` goal is executed during the `generate-sources` phase and the `manifest` goal is executed during the `process-classes` phase.

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

<SwmSnippet path="/engine-dmn/feel-juel/pom.xml" line="78">

---

# Profiles

A profile named `check-api-compatibility` is defined which is active by default. This profile uses the `clirr-maven-plugin` to check for API differences between the current and the previous version. The `check-no-fork` goal is executed during the `verify` phase.

```xml
  <profiles>
    <!-- check for api differences between latest minor release -->
    <profile>
      <id>check-api-compatibility</id>
      <activation>
        <activeByDefault>true</activeByDefault>
      </activation>
      <build>
        <plugins>
          <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>clirr-maven-plugin</artifactId>
            <configuration>
              <comparisonVersion>${camunda.version.old}</comparisonVersion>
              <logResults>true</logResults>
              <excludes>
                <exclude>org/camunda/bpm/dmn/feel/impl/**</exclude>
                <!-- exclude shaded dependencies -->
                <exclude>camundafeel/**</exclude>
              </excludes>
            </configuration>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
