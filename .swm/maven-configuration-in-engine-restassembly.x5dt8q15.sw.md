---
title: Maven Configuration in engine-rest/assembly
---
This document provides a detailed explanation of how Maven is used in the `engine-rest/assembly` directory of the project.

<SwmSnippet path="/engine-rest/assembly/pom.xml" line="1">

---

# Maven Project Configuration

The `pom.xml` file starts by defining the project and its model version. It specifies the artifactId and the packaging type. It also defines the parent project, which is `camunda-engine-rest-root`.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <artifactId>camunda-engine-rest</artifactId>
  <name>Camunda Platform - engine - REST - Assembly</name>
  <packaging>war</packaging>

  <parent>
    <groupId>org.camunda.bpm</groupId>
    <artifactId>camunda-engine-rest-root</artifactId>
    <relativePath>../</relativePath>
    <version>7.22.0-SNAPSHOT</version>
  </parent>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/assembly/pom.xml" line="14">

---

The properties section is used to control the generation of a bill of materials (BOM) for the license book. It includes compile and provided scope dependencies.

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

<SwmSnippet path="/engine-rest/assembly/pom.xml" line="23">

---

The dependencies section lists all the dependencies required for the project. It includes the core engine, sources, tests, and other necessary libraries.

```xml
  <dependencies>
    <dependency>
      <groupId>org.camunda.bpm</groupId>
      <artifactId>camunda-engine-rest-core</artifactId>
      <version>${project.version}</version>
    </dependency>

    <!-- dependencies only used for assemblies should be scope provided -->
    <dependency>
      <groupId>org.camunda.bpm</groupId>
      <artifactId>camunda-engine-rest-core</artifactId>
      <version>${project.version}</version>
      <classifier>sources</classifier>
      <scope>provided</scope>
    </dependency>

    <dependency>
      <groupId>org.camunda.bpm</groupId>
      <artifactId>camunda-engine-rest-core</artifactId>
      <version>${project.version}</version>
      <classifier>tests</classifier>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/assembly/pom.xml" line="69">

---

The build section defines the plugins used during the build process. The maven-assembly-plugin is used to create a binary distribution of the project. It is configured to package the project for different servers like wildfly, tomcat, was, wls, and also to package classes, sources, and tests.

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
