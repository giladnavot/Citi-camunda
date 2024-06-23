---
title: Maven Configuration in engine-rest/engine-rest-openapi
---
This document provides a detailed explanation of how Maven is used in the `engine-rest/engine-rest-openapi` directory of the project.

<SwmSnippet path="/engine-rest/engine-rest-openapi/pom.xml" line="1">

---

# Project Information

The `pom.xml` file starts by defining the project information. The `modelVersion` is set to `4.0.0`, which is the version of the POM model used. The `artifactId` is `camunda-engine-rest-openapi`, which is the unique identifier of this project. The `name` is `Camunda Platform - engine - REST - OpenAPI`, which is a human-readable name of the project. The `packaging` is set to `jar`, which means the project will be packaged as a JAR file.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <artifactId>camunda-engine-rest-openapi</artifactId>
  <name>Camunda Platform - engine - REST - OpenAPI</name>
  <packaging>jar</packaging>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/pom.xml" line="7">

---

# Parent Project

The `parent` tag is used to indicate that this project is a child of the parent project defined here. The `groupId` is `org.camunda.bpm`, the `artifactId` is `camunda-engine-rest-root`, and the `version` is `7.22.0-SNAPSHOT`. The `relativePath` is set to `../`, which is the directory of the parent POM relative to this project.

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

<SwmSnippet path="/engine-rest/engine-rest-openapi/pom.xml" line="14">

---

# Properties

The `properties` tag is used to define project-wide properties that can be referenced elsewhere in the POM. Here, properties related to the OpenAPI generator and its dependencies are defined.

```xml
  <properties>
    <generated-directory>${project.build.directory}/generated-sources/openapi-json</generated-directory>
    <generated-file>openapi.json</generated-file>

    <openapi.generator.version>4.2.3</openapi.generator.version>
    <!-- properties versions used by the openapi client -->
    <!-- update them during openapi.generator version update  -->
    <gson-fire-version>1.8.3</gson-fire-version>
    <swagger-core-version>1.5.22</swagger-core-version>
    <okhttp-version>3.14.2</okhttp-version>
    <gson-version>2.8.9</gson-version>
    <commons-lang3-version>3.9</commons-lang3-version>
    <maven-plugin-version>1.0.0</maven-plugin-version>
    <javax-annotation-version>1.0</javax-annotation-version>
    <junit-version>4.13.1</junit-version>
  </properties>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/pom.xml" line="31">

---

# Dependencies

The `dependencies` tag is used to list all the dependencies of the project. These dependencies include the OpenAPI generator, test dependencies, and dependencies required by the OpenAPI client.

```xml
  <dependencies>

    <dependency>
      <groupId>org.camunda.bpm</groupId>
      <artifactId>camunda-engine-rest-openapi-generator</artifactId>
      <scope>test</scope>
      <version>${project.version}</version>
    </dependency>

    <!-- test dependencies -->
    <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-jdk14</artifactId>
      <scope>test</scope>
    </dependency>
    <dependency>
      <groupId>com.github.tomakehurst</groupId>
      <artifactId>wiremock</artifactId>
      <version>${version.wiremock}</version>
      <scope>test</scope>
    </dependency>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/pom.xml" line="120">

---

# Build Configuration

The `build` tag is used to provide build-specific information. This includes the configuration of various plugins such as the `exec-maven-plugin`, `build-helper-maven-plugin`, and `openapi-generator-maven-plugin`.

```xml
  <build>
    <plugins>
      <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>exec-maven-plugin</artifactId>
        <executions>
          <execution>
            <id>generate-openapi-json</id>
            <phase>generate-resources</phase>
            <goals>
              <goal>java</goal>
            </goals>
            <configuration>
              <classpathScope>test</classpathScope>
              <mainClass>org.camunda.bpm.engine.rest.openapi.generator.impl.TemplateParser</mainClass>
              <arguments>
                <argument>${project.basedir}/src/main/templates</argument>
                <argument>main.ftl</argument>
                <argument>${generated-directory}/${generated-file}</argument>
                <argument>${project.build.directory}</argument>
              </arguments>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/pom.xml" line="222">

---

# Profiles

The `profiles` tag is used to provide specific configurations that can be activated under certain conditions. Here, a profile with the id `javadocs` is defined, which modifies the build configuration when generating JavaDocs.

```xml
  <profiles>
    <profile>
      <id>javadocs</id>
      <build>
        <plugins>
          <plugin>
            <groupId>org.openapitools</groupId>
            <artifactId>openapi-generator-maven-plugin</artifactId>
            <version>${openapi.generator.version}</version>
            <configuration>
              <skip>true</skip>
            </configuration>
          </plugin>
          
          <plugin>
            <artifactId>maven-compiler-plugin</artifactId>
            <executions>
              <execution>
                <id>default-testCompile</id>
                <goals>
                  <goal>testCompile</goal>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
