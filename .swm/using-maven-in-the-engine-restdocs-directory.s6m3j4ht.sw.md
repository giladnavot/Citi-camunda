---
title: Using Maven in the engine-rest/docs Directory
---
This document provides a detailed explanation of how Maven is used in the `engine-rest/docs` directory of the project.

<SwmSnippet path="/engine-rest/docs/pom.xml" line="1">

---

# Maven Project Configuration

The `pom.xml` file defines the Maven project configuration. It specifies the parent project, the model version, the artifact ID, the name, and the packaging type of the project.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">

  <parent>
    <artifactId>camunda-engine-rest-root</artifactId>
    <groupId>org.camunda.bpm</groupId>
    <version>7.22.0-SNAPSHOT</version>
  </parent>
  <modelVersion>4.0.0</modelVersion>

  <artifactId>docs</artifactId>
  <name>Camunda Platform - engine - REST - Docs</name>
  <packaging>pom</packaging>

```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/docs/pom.xml" line="14">

---

The `properties` section is used to define project-wide properties. Here, the `skip-third-party-bom` property is set to `true`.

```xml
  <properties>
    <skip-third-party-bom>true</skip-third-party-bom>
  </properties>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/docs/pom.xml" line="18">

---

The `dependencies` section is used to define the dependencies of the project. Here, the project depends on `camunda-engine-rest-openapi`.

```xml
  <dependencies>
    <dependency>
      <groupId>org.camunda.bpm</groupId>
      <artifactId>camunda-engine-rest-openapi</artifactId>
      <version>${project.version}</version>
    </dependency>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/docs/pom.xml" line="26">

---

# Maven Build Configuration

The `build` section is used to configure the build process. Here, the `maven-dependency-plugin` is used to unpack the `camunda-engine-rest-openapi` artifact during the `generate-resources` phase.

```xml
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-dependency-plugin</artifactId>
        <executions>
          <execution>
            <id>unpack</id>
            <phase>generate-resources</phase>
            <goals>
              <goal>unpack</goal>
            </goals>
            <configuration>
              <artifactItems>
                <artifactItem>
                  <groupId>org.camunda.bpm</groupId>
                  <artifactId>camunda-engine-rest-openapi</artifactId>
                  <version>${project.version}</version>
                  <type>jar</type>
                </artifactItem>
              </artifactItems>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/docs/pom.xml" line="51">

---

The `frontend-maven-plugin` is used to install Node.js and npm, run `npm install`, and execute the `npm run build` command during the `generate-resources` phase.

```xml
      <plugin>
        <groupId>com.github.eirslett</groupId>
        <artifactId>frontend-maven-plugin</artifactId>
        <configuration>
          <outputdir>${project.build.directory}</outputdir>
        </configuration>
        <executions>
          <execution>
            <id>install node and npm</id>
            <goals>
              <goal>install-node-and-npm</goal>
            </goals>
          </execution>
          <execution>
            <id>npm install</id>
            <goals>
              <goal>npm</goal>
            </goals>
            <phase>generate-resources</phase>
            <configuration>
              <arguments>ci</arguments>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/docs/build.js" line="1">

---

# Node.js Build Script

The `build.js` script is a Node.js script that generates the documentation. It uses the `redoc` library to load the OpenAPI specification from `docs/target/dependency/openapi.json`, create a store, and render the documentation as a static HTML page.

```javascript
#!/usr/bin/env node

const {createElement} = require("react");
const {renderToString} = require("react-dom/server");

const {ServerStyleSheet} = require("styled-components");
const {dirname, join} = require("path");

const {
    readFileSync,
    writeFileSync
} = require("fs");

const {Redoc, createStore, loadAndBundleSpec} = require("redoc");

const SPEC_PATH = "docs/target/dependency/openapi.json";

async function generateDocs() {
    const spec = await loadAndBundleSpec(SPEC_PATH);
    const store = await createStore(spec, null, {});

```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/docs/package.json" line="1">

---

# Node.js Project Configuration

The `package.json` file defines the Node.js project configuration. It specifies the name, version, scripts, and dependencies of the project. The `build` script is set to run the `build.js` script.

```json
{
  "name": "docs",
  "version": "7.22.0-SNAPSHOT",
  "private": true,
  "scripts": {
    "build": "node build"
  },
  "dependencies": {
    "redoc": "2.1.1"
  }
}
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
