---
title: Maven Configuration in engine-cdi/jakarta
---
This document provides a detailed explanation of how Maven is used in the `engine-cdi/jakarta` directory of the project.

<SwmSnippet path="/engine-cdi/jakarta/pom.xml" line="1">

---

# Maven Project Configuration

The `pom.xml` file starts with the project configuration. It specifies the model version, the name, artifactId, and packaging type of the project. It also defines the parent project from which it inherits default configuration.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <name>Camunda Platform - engine - Cdi - Jakarta</name>
  <artifactId>camunda-engine-cdi-jakarta</artifactId>
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

<SwmSnippet path="/engine-cdi/jakarta/pom.xml" line="16">

---

# Properties Configuration

The properties section defines versions of various dependencies such as `arquillian.container.version`, `arquillian.junit.version`, and `weld.version`.

```xml
  <properties>
    <arquillian.container.version>3.0.2.Final</arquillian.container.version>
    <arquillian.junit.version>1.7.0.Alpha14</arquillian.junit.version>
    <weld.version>5.0.1.Final</weld.version>
  </properties>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-cdi/jakarta/pom.xml" line="22">

---

# Dependency Management

The `dependencyManagement` section is used to manage the versions of dependencies. It includes dependencies like `camunda-core-internal-dependencies`, `weld-core-bom`, and `jakarta.jakartaee-bom`.

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
      <dependency>
        <groupId>jakarta.platform</groupId>
        <artifactId>jakarta.jakartaee-bom</artifactId>
        <version>${version.jakarta-ee-spec}</version>
        <type>pom</type>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-cdi/jakarta/pom.xml" line="48">

---

# Dependencies Configuration

The `dependencies` section is where the dependencies required for the project are defined. It includes dependencies like `camunda-engine`, `jakarta.enterprise.concurrent-api`, `jakarta.enterprise.cdi-api`, and others.

```xml
  <dependencies>
    <dependency>
      <groupId>org.camunda.bpm</groupId>
      <artifactId>camunda-engine</artifactId>
      <exclusions>
        <exclusion>
          <artifactId>livetribe-jsr223</artifactId>
          <groupId>org.livetribe</groupId>
        </exclusion>
      </exclusions>
    </dependency>

    <dependency>
      <groupId>jakarta.enterprise.concurrent</groupId>
      <artifactId>jakarta.enterprise.concurrent-api</artifactId>
      <scope>provided</scope>
    </dependency>
    <dependency>
      <groupId>jakarta.enterprise</groupId>
      <artifactId>jakarta.enterprise.cdi-api</artifactId>
      <scope>provided</scope>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-cdi/jakarta/pom.xml" line="150">

---

# Build Configuration

The `build` section defines the build plugins and their configurations. It includes plugins like `maven-resources-plugin`, `transformer-maven-plugin`, `build-helper-maven-plugin`, `maven-source-plugin`, and `maven-jar-plugin`.

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
              <outputDirectory>${project.build.directory}/generated-sources/jakarta</outputDirectory>
               <resources>
                <resource>
                  <directory>${basedir}/../core/src/main/java</directory>
                  <filtering>false</filtering>
                  <!-- exclude manual overrides -->
                  <excludes>**/CdiEventListener.java,**/CdiJtaProcessEngineConfiguration.java</excludes>
                </resource>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
