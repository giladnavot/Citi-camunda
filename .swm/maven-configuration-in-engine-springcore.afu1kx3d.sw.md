---
title: Maven Configuration in engine-spring/core
---
This document provides a detailed walkthrough of how Maven is used in the `engine-spring/core` directory of the project. It focuses on the configuration and dependencies defined in the `pom.xml` file.

<SwmSnippet path="/engine-spring/core/pom.xml" line="1">

---

# Project Information

The `pom.xml` file starts with the project information. It specifies the model version, the name of the project, and the artifact ID. It also defines the parent project, which is `camunda-database-settings` in this case.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <name>Camunda Platform - engine - Spring</name>
  <artifactId>camunda-engine-spring</artifactId>

  <parent>
    <groupId>org.camunda.bpm</groupId>
    <artifactId>camunda-database-settings</artifactId>
    <relativePath>../../database</relativePath>
    <version>7.22.0-SNAPSHOT</version>
  </parent>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-spring/core/pom.xml" line="14">

---

# Dependency Management

The `dependencyManagement` section is used to manage the versions of the dependencies. It includes `camunda-core-internal-dependencies` and `spring-framework-bom`.

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
        <groupId>org.springframework</groupId>
        <artifactId>spring-framework-bom</artifactId>
        <version>${version.spring.framework}</version>
        <type>pom</type>
        <scope>import</scope>
      </dependency>

    </dependencies>
  </dependencyManagement>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-spring/core/pom.xml" line="36">

---

# Dependencies

The `dependencies` section lists all the dependencies required for the project. It includes `camunda-engine`, `spring-context`, `spring-jdbc`, `spring-tx`, `spring-orm`, `spring-web`, and others. Some dependencies are marked as `provided`, meaning they are required for compiling the project code, but should not be included in the final package as they are provided by the runtime environment.

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

<SwmSnippet path="/engine-spring/core/pom.xml" line="163">

---

# Build Configuration

The `build` section defines the build plugins. It includes the `maven-surefire-plugin` for running tests and the `maven-jar-plugin` for creating the jar file.

```xml
  <build>
    <plugins>
      <plugin>
        <artifactId>maven-surefire-plugin</artifactId>
        <configuration>
          <redirectTestOutputToFile>true</redirectTestOutputToFile>
          <dependenciesToScan>
            <dependency>org.camunda.bpm:camunda-bpm-archunit</dependency>
          </dependenciesToScan>
        </configuration>
      </plugin>

      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-jar-plugin</artifactId>
        <executions>
          <!-- create test jar that is consumed by the compatibility tests -->
          <execution>
            <id>create-test-jar</id>
            <phase>package</phase>
            <goals>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-spring/core/pom.xml" line="199">

---

# Profiles

The `profiles` section defines build profiles. Here, a profile for Java 15 is defined, which adjusts the configuration of the `maven-surefire-plugin`.

```xml
  <profiles>
    <profile>
      <id>java15</id>
      <activation>
        <jdk>[15,)</jdk>
      </activation>
      <build>
        <pluginManagement>
          <plugins>
            <plugin>
              <groupId>org.apache.maven.plugins</groupId>
              <artifactId>maven-surefire-plugin</artifactId>
              <configuration>
                <!-- Nashorn is not part of the JDK anymore in Java 15+ -->
                <excludes>
                  <exclude>**/*NashornTest.java</exclude>
                </excludes>
              </configuration>
            </plugin>
          </plugins>
        </pluginManagement>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
