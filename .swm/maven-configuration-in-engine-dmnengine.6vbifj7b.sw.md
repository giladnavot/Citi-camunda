---
title: Maven Configuration in engine-dmn/engine
---
This document provides a detailed explanation of how Maven is used in the `engine-dmn/engine` directory of the project. It will cover the configuration and dependencies defined in the `pom.xml` file, and how they are used in the project.

<SwmSnippet path="/engine-dmn/engine/pom.xml" line="1">

---

# Project Configuration

The `pom.xml` file starts with the project configuration. It specifies the model version and the parent artifact details. The parent artifact is `camunda-engine-dmn-root` with version `7.22.0-SNAPSHOT`.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <parent>
    <groupId>org.camunda.bpm.dmn</groupId>
    <artifactId>camunda-engine-dmn-root</artifactId>
    <version>7.22.0-SNAPSHOT</version>
  </parent>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/engine/pom.xml" line="11">

---

# Artifact Details

The artifact details for this project are defined here. The artifact ID is `camunda-engine-dmn` and the name is `camunda DMN - engine`. Additional properties are also defined for the artifact.

```xml
  <artifactId>camunda-engine-dmn</artifactId>
  <name>camunda DMN - engine</name>
  <properties>
    <camunda.artifact>org.camunda.bpm.dmn.engine</camunda.artifact>
    <camunda.osgi.import.additional>
      org.junit.*;resolution:=optional
    </camunda.osgi.import.additional>
  </properties>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/engine/pom.xml" line="19">

---

# Dependencies

This section defines the dependencies for the project. It includes dependencies for `camunda-commons-utils`, `camunda-commons-typed-values`, `camunda-dmn-model`, `camunda-engine-feel-api`, `camunda-engine-feel-juel`, `camunda-engine-feel-scala`, `feel-engine`, `camunda-juel`, and several others. The scope of some dependencies is set to `test`, meaning they are only required for testing.

```xml
  <dependencies>
    <dependency>
      <groupId>org.camunda.commons</groupId>
      <artifactId>camunda-commons-utils</artifactId>
      <version>${project.version}</version>
    </dependency>

    <dependency>
      <groupId>org.camunda.commons</groupId>
      <artifactId>camunda-commons-typed-values</artifactId>
      <version>${project.version}</version>
    </dependency>

    <dependency>
      <groupId>org.camunda.bpm.model</groupId>
      <artifactId>camunda-dmn-model</artifactId>
    </dependency>

    <dependency>
      <groupId>org.camunda.bpm.dmn</groupId>
      <artifactId>camunda-engine-feel-api</artifactId>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/engine/pom.xml" line="120">

---

# Build Configuration

The build configuration is defined here. It includes the configuration for the `maven-surefire-plugin` and the `maven-bundle-plugin`. The `maven-bundle-plugin` is used to create a bundle manifest during the `process-classes` phase.

```xml
  <build>
    <plugins>
      <plugin>
        <artifactId>maven-surefire-plugin</artifactId>
        <configuration>
          <dependenciesToScan>
            <dependency>org.camunda.bpm:camunda-bpm-archunit</dependency>
          </dependenciesToScan>
        </configuration>
      </plugin>
      <plugin>
        <groupId>org.apache.felix</groupId>
        <artifactId>maven-bundle-plugin</artifactId>
        <executions>
          <execution>
            <id>bundle-manifest</id>
            <phase>process-classes</phase>
            <goals>
              <goal>manifest</goal>
            </goals>
          </execution>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/engine/pom.xml" line="146">

---

# Profiles

A Maven profile `check-api-compatibility` is defined here. This profile is activated by default and uses the `clirr-maven-plugin` to check for API differences between the latest minor release.

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
                <exclude>org/camunda/bpm/dmn/engine/impl/**</exclude>
              </excludes>
            </configuration>
            <executions>
              <execution>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
