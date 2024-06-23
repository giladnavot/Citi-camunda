---
title: Maven Configuration in Camunda Platform Engine
---
This document provides a detailed explanation of how Maven is used in the Camunda Platform engine. It will cover the configuration file `pom.xml` and how it is used to manage dependencies, plugins, and properties for the project.

<SwmSnippet path="/engine/pom.xml" line="1">

---

# Project Metadata

The project metadata defines the basic information about the project such as the model version, project name, and artifact ID. It also specifies the parent project, which in this case is `camunda-database-settings`.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">

  <modelVersion>4.0.0</modelVersion>

  <name>Camunda Platform - engine</name>
  <artifactId>camunda-engine</artifactId>

  <parent>
    <groupId>org.camunda.bpm</groupId>
    <artifactId>camunda-database-settings</artifactId>
    <relativePath>../database</relativePath>
    <version>7.22.0-SNAPSHOT</version>
  </parent>
```

---

</SwmSnippet>

<SwmSnippet path="/engine/pom.xml" line="15">

---

# Dependency Management

The dependency management section is used to manage the versions of various dependencies in a central place. Dependencies such as `camunda-core-internal-dependencies`, `spring-framework-bom`, and `jakarta.jakartaee-bom` are defined here.

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

      <dependency>
        <groupId>jakarta.platform</groupId>
```

---

</SwmSnippet>

<SwmSnippet path="/engine/pom.xml" line="45">

---

# Dependencies

The dependencies section lists all the dependencies needed for the project. These include both internal dependencies like `camunda-bpmn-model`, `camunda-cmmn-model`, and `camunda-juel`, as well as external dependencies like `spring-beans`, `mybatis`, and `joda-time`.

```xml
  <dependencies>

    <!-- camunda dependencies -->

    <dependency>
      <groupId>org.camunda.bpm.model</groupId>
      <artifactId>camunda-bpmn-model</artifactId>
    </dependency>

    <dependency>
      <groupId>org.camunda.bpm.model</groupId>
      <artifactId>camunda-cmmn-model</artifactId>
    </dependency>

    <dependency>
      <groupId>org.camunda.bpm.juel</groupId>
      <artifactId>camunda-juel</artifactId>
    </dependency>

    <dependency>
      <groupId>org.camunda.bpm.dmn</groupId>
```

---

</SwmSnippet>

<SwmSnippet path="/engine/pom.xml" line="348">

---

# Properties

The properties section is used to define project-wide properties that can be referenced elsewhere in the pom file. It includes properties like `test.includes`, `history.level`, `mail.server.port`, and `jdbcBatchProcessing`.

```xml
  <properties>
    <test.includes />
    <!-- without a special test profile we don't want to exclude anything, this expressions should never match -->
    <test.excludes>$.</test.excludes>
    <history.level>full</history.level>
    <mail.server.port>5025</mail.server.port>
    <authorizationCheckRevokes>auto</authorizationCheckRevokes>
    <jdbcBatchProcessing>true</jdbcBatchProcessing>

    <!-- We shade artifacts into the jar, so we need to generate a dependency BOM
    for the license book -->
    <skip-third-party-bom>false</skip-third-party-bom>

    <camunda.artifact>
      org.camunda.bpm
    </camunda.artifact>
    <camunda.osgi.export.pkg>
      !${camunda.artifact}.engine.variable.*,
      ${camunda.artifact},
      ${camunda.artifact}.application.*,
      ${camunda.artifact}.container.*,
```

---

</SwmSnippet>

<SwmSnippet path="/engine/pom.xml" line="392">

---

# Build Configuration

The build section defines project-specific build settings. It includes configurations for resources, test resources, and plugins like `maven-surefire-plugin`, `maven-bundle-plugin`, `maven-jar-plugin`, and `maven-shade-plugin`.

```xml
  <build>
    <!-- filter test configurations to inject properties -->
    <resources>
      <resource>
        <directory>src/main/resources</directory>
      </resource>
      <resource>
        <directory>src/main/resources</directory>
        <filtering>true</filtering>
        <includes>
          <include>org/camunda/bpm/engine/product-info.properties</include>
        </includes>
      </resource>
    </resources>
    <testResources>
      <testResource>
        <directory>src/test/resources</directory>
      </testResource>
      <testResource>
        <directory>src/test/resources</directory>
        <filtering>true</filtering>
```

---

</SwmSnippet>

<SwmSnippet path="/engine/pom.xml" line="576">

---

# Profiles

The profiles section is used to provide different build settings for different environments. It includes profiles for `distro`, `database`, `cfghistoryaudit`, `cfghistoryactivity`, `cfghistorynone`, `cfgJdbcBatchProcessingOff`, and various database profiles.

```xml
  <profiles>
    <profile>
      <id>distro</id>
      <build>
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
        </plugins>
      </build>
    </profile>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
