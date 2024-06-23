---
title: Maven Configuration in engine-spring/core-6
---
This document provides a detailed explanation of how Maven is used in the `engine-spring/core-6` module of the Camunda Platform.

<SwmSnippet path="/engine-spring/core-6/pom.xml" line="1">

---

## Project Information

The `pom.xml` file starts with the project information. The `modelVersion` is set to `4.0.0`, which is the standard for Maven 2 and 3. The `name` and `artifactId` specify the name and identifier of the project. The `parent` section indicates that this module is a child of the `camunda-database-settings` module.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <name>Camunda Platform - engine - Spring 6</name>
  <artifactId>camunda-engine-spring-6</artifactId>

  <parent>
    <groupId>org.camunda.bpm</groupId>
    <artifactId>camunda-database-settings</artifactId>
    <relativePath>../../database</relativePath>
    <version>7.22.0-SNAPSHOT</version>
  </parent>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-spring/core-6/pom.xml" line="14">

---

## Dependency Management

The `dependencyManagement` section is used to manage the versions of dependencies. This section defines the versions of `camunda-core-internal-dependencies`, `jakarta.jakartaee-bom`, and `spring-framework-bom` that will be used in this module.

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
        <groupId>jakarta.platform</groupId>
        <artifactId>jakarta.jakartaee-bom</artifactId>
        <version>${version.jakarta-ee-spec}</version>
        <type>pom</type>
        <scope>import</scope>
      </dependency>

      <dependency>
        <groupId>org.springframework</groupId>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-spring/core-6/pom.xml" line="44">

---

## Dependencies

The `dependencies` section lists all the dependencies required by this module. These include `camunda-engine`, `spring-context`, `spring-jdbc`, `spring-tx`, `spring-orm`, `spring-web`, and others. Some dependencies are marked as `provided`, meaning they are required for compilation and testing, but should not be packaged with the application as they are provided by the runtime environment.

```xml
  <dependencies>
    <dependency>
      <groupId>org.camunda.bpm</groupId>
      <artifactId>camunda-engine</artifactId>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <scope>provided</scope>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jdbc</artifactId>
      <scope>provided</scope>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-tx</artifactId>
      <scope>provided</scope>
    </dependency>
    <dependency>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-spring/core-6/pom.xml" line="171">

---

## Build Configuration

The `build` section contains the build configuration. It includes several plugins such as `maven-resources-plugin`, `maven-dependency-plugin`, `transformer-maven-plugin`, `maven-surefire-plugin`, `build-helper-maven-plugin`, `maven-source-plugin`, and `maven-enforcer-plugin`. These plugins are used to perform various build tasks such as resource copying, dependency management, source transformation, testing, source addition, and enforcing certain conditions.

```xml
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-resources-plugin</artifactId>
        <executions>
          <execution>
            <id>sources</id>
            <phase>generate-sources</phase>
            <goals>
              <goal>copy-resources</goal>
            </goals>
            <configuration>
              <outputDirectory>${project.build.directory}/generated-sources/java</outputDirectory>
               <resources>
                <resource>
                  <directory>${basedir}/../core/src/main/java</directory>
                  <filtering>false</filtering>
                </resource>
              </resources>
            </configuration>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
