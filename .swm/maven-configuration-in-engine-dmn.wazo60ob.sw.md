---
title: Maven Configuration in engine-dmn
---
This document provides a detailed explanation of how Maven is used in the `engine-dmn` module of the project. It will cover the configuration and usage of Maven in the `pom.xml` files located in the `engine-dmn` directory.

<SwmSnippet path="/engine-dmn/pom.xml" line="4">

---

# Parent Project Configuration

The `pom.xml` file starts by defining the parent project. This is done using the `<parent>` tag. The parent project is `camunda-database-settings` with the version `7.22.0-SNAPSHOT`. The relative path to the parent project is `../database`.

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

<SwmSnippet path="/engine-dmn/pom.xml" line="11">

---

# Project Information

The `groupId`, `artifactId`, `name`, `inceptionYear`, and `packaging` for the project are defined. The `groupId` is `org.camunda.bpm.dmn`, the `artifactId` is `camunda-engine-dmn-root`, the `name` is `camunda DMN - engine - root`, the `inceptionYear` is `2015`, and the `packaging` is `pom`.

```xml
  <groupId>org.camunda.bpm.dmn</groupId>
  <artifactId>camunda-engine-dmn-root</artifactId>
  <name>camunda DMN - engine - root</name>
  <inceptionYear>2015</inceptionYear>
  <packaging>pom</packaging>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/pom.xml" line="17">

---

# Properties

The `properties` section defines the version of `juel` to be used, which is `2.2.7`.

```xml
  <properties>
    <version.juel>2.2.7</version.juel>
  </properties>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/pom.xml" line="21">

---

# Dependency Management

The `dependencyManagement` section is used to manage the versions of dependencies. In this case, it imports the `pom` file of `camunda-core-internal-dependencies` with the version as `${project.version}`.

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
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/pom.xml" line="34">

---

# Modules

The `modules` section lists the modules that make up this project. The modules are `bom`, `engine`, `feel-api`, `feel-juel`, and `feel-scala`.

```xml
  <modules>
    <module>bom</module>
    <module>engine</module>
    <module>feel-api</module>
    <module>feel-juel</module>
    <module>feel-scala</module>
  </modules>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/pom.xml" line="42">

---

# Build Configuration

The `build` section defines how the project should be built. The `maven-surefire-plugin` is configured to redirect test output to a file. The `maven-bundle-plugin` is also added to the build plugins.

```xml
  <build>
    <pluginManagement>
      <plugins>
        <plugin>
          <groupId>org.apache.maven.plugins</groupId>
          <artifactId>maven-surefire-plugin</artifactId>
          <configuration>
            <redirectTestOutputToFile>true</redirectTestOutputToFile>
          </configuration>
        </plugin>
      </plugins>
    </pluginManagement>

    <plugins>
      <plugin>
        <groupId>org.apache.felix</groupId>
        <artifactId>maven-bundle-plugin</artifactId>
      </plugin>
    </plugins>
  </build>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
