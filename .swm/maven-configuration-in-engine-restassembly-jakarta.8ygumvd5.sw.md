---
title: Maven Configuration in engine-rest/assembly-jakarta
---
This document provides a detailed walkthrough of how Maven is used in the `engine-rest/assembly-jakarta` directory of the project.

<SwmSnippet path="/engine-rest/assembly-jakarta/pom.xml" line="1">

---

# Project Information

The `pom.xml` file starts by defining the model version, artifact ID, name, and packaging type. It also specifies the parent project, which is `camunda-engine-rest-root`.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <artifactId>camunda-engine-rest-jakarta</artifactId>
  <name>Camunda Platform - engine - REST - Assembly Jakarta</name>
  <packaging>war</packaging>

  <parent>
    <groupId>org.camunda.bpm</groupId>
    <artifactId>camunda-engine-rest-root</artifactId>
    <version>7.22.0-SNAPSHOT</version>
  </parent>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/assembly-jakarta/pom.xml" line="14">

---

# Properties

The properties section defines whether to skip the third-party bom and the scopes for the third-party bom.

```xml
  <properties>
    <!-- generate a bom of dependencies for the license book.
    We include compile and provided scope dependencies;
    all the dependencies that we include in only one of the
    runtime-specific-WARs are in provided scope -->
    <skip-third-party-bom>false</skip-third-party-bom>
    <third-party-bom-scopes>compile|provided</third-party-bom-scopes>
  </properties>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/assembly-jakarta/pom.xml" line="23">

---

# Dependency Management

The `dependencyManagement` section is used to manage the versions of dependencies. In this case, it imports the `jakarta.jakartaee-bom` dependency.

```xml
  <dependencyManagement>
    <dependencies>
      <dependency>
        <groupId>jakarta.platform</groupId>
        <artifactId>jakarta.jakartaee-bom</artifactId>
        <version>${version.jakarta-ee-spec}</version>
        <scope>import</scope>
        <type>pom</type>
      </dependency>
    </dependencies>
  </dependencyManagement>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/assembly-jakarta/pom.xml" line="35">

---

# Dependencies

The `dependencies` section lists all the dependencies required for the project. It includes the `camunda-engine-rest-core-jakarta` and `jakarta.ws.rs-api` dependencies.

```xml
  <dependencies>
    <dependency>
      <groupId>org.camunda.bpm</groupId>
      <artifactId>camunda-engine-rest-core-jakarta</artifactId>
      <version>${project.version}</version>
    </dependency>

    <!-- dependencies only used for assemblies should be scope provided -->
    <dependency>
      <groupId>org.camunda.bpm</groupId>
      <artifactId>camunda-engine-rest-core-jakarta</artifactId>
      <version>${project.version}</version>
      <classifier>sources</classifier>
      <scope>provided</scope>
    </dependency>
    <dependency>
      <groupId>org.camunda.bpm</groupId>
      <artifactId>camunda-engine-rest-core-jakarta</artifactId>
      <version>${project.version}</version>
      <classifier>tests</classifier>
      <scope>provided</scope>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/assembly-jakarta/pom.xml" line="65">

---

# Build Configuration

The `build` section defines how the project should be built. It specifies the use of the `maven-assembly-plugin` and its configurations for different executions such as `wildfly`, `classes`, `sources`, and `tests`.

```xml
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-assembly-plugin</artifactId>
        <executions>
          <execution>
            <id>wildfly</id>
            <phase>package</phase>
            <goals>
              <goal>single</goal>
            </goals>
            <configuration>
              <archive>
                <manifestEntries>
                  <!-- module dependencies for deployment on wildfly  -->
                  <Dependencies>org.camunda.bpm.camunda-engine,org.camunda.bpm.dmn.camunda-engine-dmn,org.camunda.commons.camunda-commons-logging,org.camunda.spin.camunda-spin-core,org.camunda.bpm.juel.camunda-juel services,org.graalvm.js.js-scriptengine services</Dependencies>
                </manifestEntries>
              </archive>
              <descriptors>
                <descriptor>assembly-war-wildfly.xml</descriptor>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
