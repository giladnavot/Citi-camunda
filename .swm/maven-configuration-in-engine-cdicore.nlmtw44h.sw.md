---
title: Maven Configuration in engine-cdi/core
---
This document provides a detailed explanation of how Maven is used in the `engine-cdi/core` directory of the project.

<SwmSnippet path="/engine-cdi/core/pom.xml" line="1">

---

# Maven Project Configuration

The `pom.xml` file starts by defining the model version, the name of the project, the artifact ID, and the packaging type. It also specifies the parent project, which is `camunda-database-settings`.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <name>Camunda Platform - engine - Cdi</name>
  <artifactId>camunda-engine-cdi</artifactId>
  <packaging>jar</packaging>

  <parent>
    <groupId>org.camunda.bpm</groupId>
    <artifactId>camunda-database-settings</artifactId>
    <relativePath>../../database</relativePath>
    <version>7.22.0-SNAPSHOT</version>
  </parent>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-cdi/core/pom.xml" line="16">

---

Next, the properties for the project are defined. These include versions for Arquillian container, Arquillian JUnit, Weld, and Java EE specifications.

```xml
  <properties>
    <arquillian.container.version>2.1.0.Final</arquillian.container.version>
    <arquillian.junit.version>1.6.0.Final</arquillian.junit.version>
    <weld.version>3.1.9.Final</weld.version>
    <javaee.spec>jboss-javaee-8.0</javaee.spec>
    <javaee.spec.version>1.0.4.Final</javaee.spec.version>
  </properties>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-cdi/core/pom.xml" line="24">

---

The `dependencyManagement` section is used to manage the versions of dependencies. In this case, it manages the versions for `camunda-core-internal-dependencies` and `weld-core-bom`.

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
        <groupId>org.jboss.weld</groupId>
        <artifactId>weld-core-bom</artifactId>
        <version>${weld.version}</version>
        <type>pom</type>
        <scope>import</scope>
      </dependency>
    </dependencies>
  </dependencyManagement>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-cdi/core/pom.xml" line="43">

---

The `dependencies` section lists all the dependencies required for the project. These include `camunda-engine`, `javaee-spec`, `arquillian-weld-embedded`, `weld-core-impl`, `weld-web`, `weld-api`, `arquillian-junit-container`, `junit`, `assertj-core`, `h2`, `logback-classic`, `jcl-over-slf4j`, `jul-to-slf4j`, and `camunda-bpm-archunit`.

```xml
  <dependencies>
    <dependency>
      <groupId>org.camunda.bpm</groupId>
      <artifactId>camunda-engine</artifactId>
      <scope>provided</scope>
      <exclusions>
        <exclusion>
          <artifactId>livetribe-jsr223</artifactId>
          <groupId>org.livetribe</groupId>
        </exclusion>
      </exclusions>
    </dependency>
    <dependency>
      <groupId>org.jboss.spec</groupId>
      <artifactId>${javaee.spec}</artifactId>
      <version>${javaee.spec.version}</version>
      <type>pom</type>
      <scope>provided</scope>
    </dependency>

    <dependency>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-cdi/core/pom.xml" line="128">

---

The `build` section defines how the project should be built. It specifies the resources to be included in the build and the plugins to be used, such as `maven-source-plugin` and `maven-surefire-plugin`.

```xml
  <build>
    <resources>
      <resource>
        <directory>src/main/resources</directory>
      </resource>
    </resources>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-source-plugin</artifactId>
        <executions>
          <execution>
            <id>attach-sources</id>
            <phase>package</phase>
            <goals>
              <goal>jar-no-fork</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
      <plugin>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
