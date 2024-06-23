---
title: Maven Configuration in engine-dmn/engine
---
This document provides a detailed explanation of how Maven is used in the <SwmPath>[engine-dmn/engine/](/engine-dmn/engine/)</SwmPath> directory of the project. It will cover the configuration and dependencies defined in the <SwmPath>[pom.xml](/pom.xml)</SwmPath> file, and how they are used in the project.

<SwmSnippet path="/engine-dmn/engine/pom.xml" line="1">

---

# Project Configuration

The <SwmPath>[pom.xml](/pom.xml)</SwmPath> file starts with the project configuration. It specifies the model version and the parent artifact details. The parent artifact is <SwmToken path="/engine-dmn/engine/pom.xml" pos="7:4:10" line-data="    &lt;artifactId&gt;camunda-engine-dmn-root&lt;/artifactId&gt;">`camunda-engine-dmn-root`</SwmToken> with version <SwmToken path="/engine-dmn/engine/pom.xml" pos="8:4:10" line-data="    &lt;version&gt;7.22.0-SNAPSHOT&lt;/version&gt;">`7.22.0-SNAPSHOT`</SwmToken>.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <parent>
    <groupId>org.camunda.bpm.dmn</groupId>
    <artifactId>camunda-engine-dmn-root</artifactId>
    <version>7.22.0-SNAPSHOT</version>
  </parent>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/engine/pom.xml" line="11">

---

# Artifact Details

The artifact details for this project are defined here. The artifact ID is <SwmToken path="/engine-dmn/engine/pom.xml" pos="11:4:8" line-data="  &lt;artifactId&gt;camunda-engine-dmn&lt;/artifactId&gt;">`camunda-engine-dmn`</SwmToken> and the name is <SwmToken path="/engine-dmn/engine/pom.xml" pos="12:4:10" line-data="  &lt;name&gt;camunda DMN - engine&lt;/name&gt;">`camunda DMN - engine`</SwmToken>. Additional properties are also defined for the artifact.

```xml
  <artifactId>camunda-engine-dmn</artifactId>
  <name>camunda DMN - engine</name>
  <properties>
    <camunda.artifact>org.camunda.bpm.dmn.engine</camunda.artifact>
    <camunda.osgi.import.additional>
      org.junit.*;resolution:=optional
    </camunda.osgi.import.additional>
  </properties>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/engine/pom.xml" line="19">

---

# Dependencies

This section defines the dependencies for the project. It includes dependencies for <SwmToken path="/engine-dmn/engine/pom.xml" pos="22:4:8" line-data="      &lt;artifactId&gt;camunda-commons-utils&lt;/artifactId&gt;">`camunda-commons-utils`</SwmToken>, <SwmToken path="/engine-dmn/engine/pom.xml" pos="28:4:10" line-data="      &lt;artifactId&gt;camunda-commons-typed-values&lt;/artifactId&gt;">`camunda-commons-typed-values`</SwmToken>, <SwmToken path="/engine-dmn/engine/pom.xml" pos="34:4:8" line-data="      &lt;artifactId&gt;camunda-dmn-model&lt;/artifactId&gt;">`camunda-dmn-model`</SwmToken>, <SwmToken path="/engine-dmn/engine/pom.xml" pos="39:4:10" line-data="      &lt;artifactId&gt;camunda-engine-feel-api&lt;/artifactId&gt;">`camunda-engine-feel-api`</SwmToken>, <SwmToken path="/engine-dmn/engine/pom.xml" pos="44:4:10" line-data="      &lt;artifactId&gt;camunda-engine-feel-juel&lt;/artifactId&gt;">`camunda-engine-feel-juel`</SwmToken>, <SwmToken path="/engine-dmn/engine/pom.xml" pos="49:4:10" line-data="      &lt;artifactId&gt;camunda-engine-feel-scala&lt;/artifactId&gt;">`camunda-engine-feel-scala`</SwmToken>, <SwmToken path="/engine-dmn/engine/pom.xml" pos="54:4:6" line-data="      &lt;artifactId&gt;feel-engine&lt;/artifactId&gt;">`feel-engine`</SwmToken>, <SwmToken path="/engine-dmn/engine/pom.xml" pos="60:4:6" line-data="      &lt;artifactId&gt;camunda-juel&lt;/artifactId&gt;">`camunda-juel`</SwmToken>, and several others. The scope of some dependencies is set to `test`, meaning they are only required for testing.

```xml
  <dependencies>
    <dependency>
      <groupId>org.camunda.commons</groupId>
      <artifactId>camunda-commons-utils</artifactId>
      <version>${project.version}</version>
    </dependency>

    <dependency>
      <groupId>org.camunda.commons</groupId>
      <artifactId>camunda-commons-typed-values</artifactId>
      <version>${project.version}</version>
    </dependency>

    <dependency>
      <groupId>org.camunda.bpm.model</groupId>
      <artifactId>camunda-dmn-model</artifactId>
    </dependency>

    <dependency>
      <groupId>org.camunda.bpm.dmn</groupId>
      <artifactId>camunda-engine-feel-api</artifactId>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/engine/pom.xml" line="120">

---

# Build Configuration

The build configuration is defined here. It includes the configuration for the <SwmToken path="/engine-dmn/engine/pom.xml" pos="123:4:8" line-data="        &lt;artifactId&gt;maven-surefire-plugin&lt;/artifactId&gt;">`maven-surefire-plugin`</SwmToken> and the <SwmToken path="/engine-dmn/engine/pom.xml" pos="132:4:8" line-data="        &lt;artifactId&gt;maven-bundle-plugin&lt;/artifactId&gt;">`maven-bundle-plugin`</SwmToken>. The <SwmToken path="/engine-dmn/engine/pom.xml" pos="132:4:8" line-data="        &lt;artifactId&gt;maven-bundle-plugin&lt;/artifactId&gt;">`maven-bundle-plugin`</SwmToken> is used to create a bundle manifest during the <SwmToken path="/engine-dmn/engine/pom.xml" pos="136:4:6" line-data="            &lt;phase&gt;process-classes&lt;/phase&gt;">`process-classes`</SwmToken> phase.

```xml
  <build>
    <plugins>
      <plugin>
        <artifactId>maven-surefire-plugin</artifactId>
        <configuration>
          <dependenciesToScan>
            <dependency>org.camunda.bpm:camunda-bpm-archunit</dependency>
          </dependenciesToScan>
        </configuration>
      </plugin>
      <plugin>
        <groupId>org.apache.felix</groupId>
        <artifactId>maven-bundle-plugin</artifactId>
        <executions>
          <execution>
            <id>bundle-manifest</id>
            <phase>process-classes</phase>
            <goals>
              <goal>manifest</goal>
            </goals>
          </execution>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/engine/pom.xml" line="146">

---

# Profiles

A Maven profile <SwmToken path="/engine-dmn/engine/pom.xml" pos="149:4:8" line-data="      &lt;id&gt;check-api-compatibility&lt;/id&gt;">`check-api-compatibility`</SwmToken> is defined here. This profile is activated by default and uses the <SwmToken path="/engine-dmn/engine/pom.xml" pos="157:4:8" line-data="            &lt;artifactId&gt;clirr-maven-plugin&lt;/artifactId&gt;">`clirr-maven-plugin`</SwmToken> to check for API differences between the latest minor release.

```xml
  <profiles>
    <!-- check for api differences between latest minor release -->
    <profile>
      <id>check-api-compatibility</id>
      <activation>
        <activeByDefault>true</activeByDefault>
      </activation>
      <build>
        <plugins>
          <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>clirr-maven-plugin</artifactId>
            <configuration>
              <comparisonVersion>${camunda.version.old}</comparisonVersion>
              <logResults>true</logResults>
              <excludes>
                <exclude>org/camunda/bpm/dmn/engine/impl/**</exclude>
              </excludes>
            </configuration>
            <executions>
              <execution>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda"><sup>Powered by [Swimm](https://app.swimm.io/)</sup></SwmMeta>
