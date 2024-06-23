---
title: Maven Configuration in Java Client
---
This document provides a detailed explanation of how Maven is used in the `clients/java/client` directory of the project. It focuses on the configuration and dependencies defined in the `pom.xml` file.

<SwmSnippet path="/clients/java/client/pom.xml" line="1">

---

# Project Information

The `pom.xml` file starts by defining the project information. The `modelVersion` is set to `4.0.0`, which is the latest model version of Maven. The `name` of the project is `Camunda Platform - Java External Task Client - CLIENT`. The `artifactId` is `camunda-external-task-client`, which is the identifier of the project artifact. The `packaging` type is set to `jar`, meaning the project will be packaged as a JAR file. The `parent` section defines the parent project from which this project inherits.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">

  <modelVersion>4.0.0</modelVersion>
  <name>Camunda Platform - Java External Task Client - CLIENT</name>

  <artifactId>camunda-external-task-client</artifactId>

  <packaging>jar</packaging>

  <parent>
    <groupId>org.camunda.bpm</groupId>
    <artifactId>camunda-external-task-client-root</artifactId>
    <version>7.22.0-SNAPSHOT</version>
  </parent>
```

---

</SwmSnippet>

<SwmSnippet path="/clients/java/client/pom.xml" line="16">

---

# Properties

The `properties` section defines project-wide properties that can be referenced elsewhere in the `pom.xml`. These properties include versions of dependencies, runtime configurations, and port numbers.

```xml
  <properties>
    <version.httpclient>5.3</version.httpclient>
    <engine.runtime>${project.build.directory}/camunda-tomcat</engine.runtime>
    <tomcat.runtime>${engine.runtime}/server/apache-tomcat-${version.tomcat}</tomcat.runtime>
    <http.port>${tomcat.connector.http.port}</http.port>

    <tomcat.connector.http.port>48080</tomcat.connector.http.port>
    <tomcat.connector.http.redirectPort>48443</tomcat.connector.http.redirectPort>
    <tomcat.connector.ajp.port>48009</tomcat.connector.ajp.port>
    <tomcat.connector.ajp.redirectPort>48443</tomcat.connector.ajp.redirectPort>
    <tomcat.server.port>48005</tomcat.server.port>

    <cargo.timeout>240000</cargo.timeout>
    <cargo.deploy.timeout>60000</cargo.deploy.timeout>
  </properties>
```

---

</SwmSnippet>

<SwmSnippet path="/clients/java/client/pom.xml" line="32">

---

# Dependency Management

The `dependencyManagement` section is used to manage the versions of dependencies. Dependencies defined here are not directly included in the project, but their versions are managed centrally. This is useful when multiple sub-modules or dependencies use a common dependency, and you want to ensure a consistent version across all of them.

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
        <groupId>com.fasterxml.jackson</groupId>
        <artifactId>jackson-bom</artifactId>
        <version>${version.jackson}</version>
        <scope>import</scope>
        <type>pom</type>
      </dependency>
    </dependencies>
  </dependencyManagement>
```

---

</SwmSnippet>

<SwmSnippet path="/clients/java/client/pom.xml" line="51">

---

# Dependencies

The `dependencies` section lists all the dependencies required by the project. These dependencies are divided into two categories: mandatory dependencies and test dependencies. Mandatory dependencies are required for the project to function, while test dependencies are only required during the testing phase.

```xml
  <dependencies>

    <!-- mandatory dependencies -->
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
      <groupId>org.apache.httpcomponents.client5</groupId>
      <artifactId>httpclient5</artifactId>
      <version>${version.httpclient}</version>
    </dependency>

```

---

</SwmSnippet>

<SwmSnippet path="/clients/java/client/pom.xml" line="170">

---

# Build Configuration

The `build` section defines how the project should be built. It includes the configuration of plugins, test resources, and other build settings. The plugins used include `build-helper-maven-plugin`, `maven-surefire-plugin`, `maven-dependency-plugin`, `maven-failsafe-plugin`, and `cargo-maven3-plugin`. These plugins help with adding test sources, running tests, managing dependencies, and deploying the application.

```xml
  <build>
    <plugins>

      <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>build-helper-maven-plugin</artifactId>
        <executions>
          <execution>
            <id>add-it-source</id>
            <phase>generate-test-sources</phase>
            <goals>
              <goal>add-test-source</goal>
            </goals>
            <configuration>
              <sources>
                <source>src/it/java</source>
              </sources>
            </configuration>
          </execution>
        </executions>
      </plugin>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
