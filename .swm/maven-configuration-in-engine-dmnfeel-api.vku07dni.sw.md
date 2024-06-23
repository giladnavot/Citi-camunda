---
title: Maven Configuration in engine-dmn/feel-api
---
This document provides a detailed explanation of how Maven is used in the `engine-dmn/feel-api` module of the project.

<SwmSnippet path="/engine-dmn/feel-api/pom.xml" line="5">

---

# Parent Project Configuration

The `parent` tag is used to indicate the parent project from which this module inherits properties. Here, the parent project is `camunda-engine-dmn-root` with version `7.22.0-SNAPSHOT`.

```xml
  <parent>
    <groupId>org.camunda.bpm.dmn</groupId>
    <artifactId>camunda-engine-dmn-root</artifactId>
    <version>7.22.0-SNAPSHOT</version>
  </parent>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-api/pom.xml" line="11">

---

# Artifact Configuration

The `artifactId` is set to `camunda-engine-feel-api`, which is the name of the jar without version. The `properties` tag is used to define project-specific properties that can be referenced elsewhere in the pom.

```xml
  <artifactId>camunda-engine-feel-api</artifactId>
  <name>camunda DMN - engine FEEL - API</name>
  <properties>
    <camunda.artifact>org.camunda.bpm.dmn.feel.impl</camunda.artifact>
  </properties>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-api/pom.xml" line="16">

---

# Dependencies Configuration

The `dependencies` tag is used to list all the dependencies required by the project. Here, the project depends on `camunda-commons-typed-values` with the same version as the project.

```xml
  <dependencies>
    <dependency>
      <groupId>org.camunda.commons</groupId>
      <artifactId>camunda-commons-typed-values</artifactId>
      <version>${project.version}</version>
    </dependency>
  </dependencies>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-api/pom.xml" line="24">

---

# Build Configuration

The `build` tag is used to provide build-specific information. The `plugins` tag within the build tag is used to list the plugins used during the build process. Here, the `maven-bundle-plugin` is used with two executions: `generate-sources` and `process-classes`.

```xml
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.felix</groupId>
        <artifactId>maven-bundle-plugin</artifactId>
        <executions>
          <execution>
            <phase>generate-sources</phase>
            <goals>
              <goal>cleanVersions</goal>
            </goals>
          </execution>
          <execution>
            <id>bundle-manifest</id>
            <phase>process-classes</phase>
            <goals>
              <goal>manifest</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-api/pom.xml" line="48">

---

# Profile Configuration

The `profiles` tag is used to provide specific settings under certain situations. Here, a profile `check-api-compatibility` is defined which is active by default. It uses the `clirr-maven-plugin` to check for API differences between the latest minor release.

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
                <exclude>org/camunda/bpm/dmn/feel/impl/**</exclude>
              </excludes>
            </configuration>
            <executions>
              <execution>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
