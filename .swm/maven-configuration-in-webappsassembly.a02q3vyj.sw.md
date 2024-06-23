---
title: Maven Configuration in webapps/assembly
---
This document provides a detailed walkthrough of how Maven is used in the `webapps/assembly` directory of the project. It focuses on the configuration files and explains each step in the configuration process.

<SwmSnippet path="/webapps/assembly/pom.xml" line="1">

---

# Maven Project Configuration

The `pom.xml` file starts with the declaration of the project model version, parent artifact details, and the artifact details of the current project. The `packaging` type is set to `war` indicating that the output should be a web application archive.

```xml
<?xml version="1.0"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">

  <modelVersion>4.0.0</modelVersion>

  <parent>
    <groupId>org.camunda.bpm.webapp</groupId>
    <artifactId>camunda-webapp-root</artifactId>
    <version>7.22.0-SNAPSHOT</version>
    <relativePath>../</relativePath>
  </parent>

  <artifactId>camunda-webapp</artifactId>
  <packaging>war</packaging>
  <name>Camunda Platform - Webapp - Assembly</name>
  <inceptionYear>2014</inceptionYear>
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/assembly/pom.xml" line="18">

---

The `properties` section defines some properties that are used throughout the POM. It includes the paths for resources and properties override, and a flag for skipping third-party bom generation.

```xml
  <properties>
    <java.resources.override>src/main/runtime/default/resources</java.resources.override>
    <properties.override>src/main/runtime/default/config.properties</properties.override>

    <!-- generate a bom of compile time dependencies for the license book.
    Note: Every compile time dependency will end up in the license book. Please
    declare only dependencies that are actually needed -->
    <skip-third-party-bom>false</skip-third-party-bom>
  </properties>
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/assembly/pom.xml" line="28">

---

The `dependencyManagement` section is used to manage the versions of dependencies. Here, it specifies the versions for `camunda-engine-rest-core`, `camunda-engine-rest`, and `activation` dependencies.

```xml
  <dependencyManagement>
    <dependencies>
      <dependency>
        <groupId>org.camunda.bpm</groupId>
        <artifactId>camunda-engine-rest-core</artifactId>
        <version>${project.version}</version>
      </dependency>
      <dependency>
        <groupId>org.camunda.bpm</groupId>
        <artifactId>camunda-engine-rest</artifactId>
        <version>${project.version}</version>
      </dependency>
      <dependency>
        <groupId>javax.activation</groupId>
        <artifactId>activation</artifactId>
        <version>1.1</version>
      </dependency>
    </dependencies>
  </dependencyManagement>
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/assembly/pom.xml" line="48">

---

The `dependencies` section declares all the dependencies required for the project. It includes dependencies for JEE specifications, REST API, and testing.

```xml
  <dependencies>

    <!-- jee spec -->
    <dependency>
      <groupId>org.jboss.spec</groupId>
      <artifactId>jboss-javaee-6.0</artifactId>
      <type>pom</type>
      <scope>provided</scope>
      <exclusions>
        <exclusion>
          <groupId>org.jboss.spec.javax.ws.rs</groupId>
          <artifactId>jboss-jaxrs-api_1.1_spec</artifactId>
        </exclusion>
      </exclusions>
    </dependency>

    <dependency>
      <groupId>org.jboss.spec.javax.ws.rs</groupId>
      <artifactId>jboss-jaxrs-api_2.1_spec</artifactId>
      <scope>provided</scope>
    </dependency>
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/assembly/pom.xml" line="99">

---

The `build` section defines how the project should be built. It specifies the final name of the project, resources, test resources, and plugins to be used during the build process.

```xml
  <build>
    <finalName>camunda-webapp</finalName>
    <resources>
      <resource>
        <directory>src/main/resources</directory>
      </resource>
      <resource>
        <directory>${java.resources.override}</directory>
        <filtering>true</filtering>
      </resource>
    </resources>

    <testResources>
      <testResource>
        <directory>src/test/resources</directory>
        <filtering>true</filtering>
      </testResource>
    </testResources>

    <plugins>
      <plugin>
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/assembly/pom.xml" line="189">

---

The `profiles` section defines different build profiles for various purposes such as sonatype-oss-release, os, develop, h2, dev-e2e, database QA profiles, and license-header-check.

```xml
  <profiles>
    <profile>
      <id>sonatype-oss-release</id>
      <properties>
        <!-- skip building the frontend-sources zip artifact
        when releasing the community edition (alpha/minor releases) -->
        <skip-zip-frontend-sources>true</skip-zip-frontend-sources>
      </properties>
    </profile>

    <profile>
      <id>os</id>
      <activation>
        <os>
          <family>Windows</family>
        </os>
      </activation>
      <properties>
        <exec.shell>cmd</exec.shell>
        <exec.arg>/c</exec.arg>
      </properties>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="general-build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
