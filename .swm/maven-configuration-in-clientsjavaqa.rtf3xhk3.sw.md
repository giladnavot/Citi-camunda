---
title: Maven Configuration in clients/java/qa
---
This document provides a detailed walkthrough of how Maven is used in the `clients/java/qa` directory of the project.

<SwmSnippet path="/clients/java/qa/pom.xml" line="1">

---

# Maven Project Configuration

The `pom.xml` file is the main configuration file for a Maven project. It defines the project structure, dependencies, build plugins, and other project-specific configurations. In this case, the project is defined with a model version of 4.0.0, a name, a group ID, an artifact ID, and a packaging type of `pom`. The parent project is specified with a group ID, artifact ID, and version. The `modules` section lists all the modules that are part of this project, in this case, `engine-variable-test`.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">

  <modelVersion>4.0.0</modelVersion>
  <name>Camunda Platform - Java External Task Client - QA</name>

  <groupId>org.camunda.bpm.qa</groupId>
  <artifactId>camunda-external-task-client-qa</artifactId>

  <packaging>pom</packaging>

  <parent>
    <groupId>org.camunda.bpm</groupId>
    <artifactId>camunda-external-task-client-root</artifactId>
    <version>7.22.0-SNAPSHOT</version>
  </parent>

  <modules>
    <module>engine-variable-test</module>
  </modules>

```

---

</SwmSnippet>

<SwmSnippet path="/clients/java/qa/engine-variable-test/pom.xml" line="1">

---

# Module Configuration

This `pom.xml` file is for the `engine-variable-test` module. It specifies the model version, name, artifact ID, and packaging type. It also defines the parent project. The `dependencies` section lists all the dependencies required for this module. The `build` section specifies the build plugins used, in this case, the `maven-war-plugin`.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">

  <modelVersion>4.0.0</modelVersion>
  <name>Camunda Platform - Java External Task Client - QA VARIABLE TEST</name>

  <artifactId>engine-variable-test</artifactId>

  <packaging>war</packaging>

  <parent>
    <groupId>org.camunda.bpm.qa</groupId>
    <artifactId>camunda-external-task-client-qa</artifactId>
    <version>7.22.0-SNAPSHOT</version>
  </parent>

  <dependencies>
    <dependency>
      <groupId>org.camunda.bpm</groupId>
      <artifactId>camunda-engine</artifactId>
      <scope>provided</scope>
```

---

</SwmSnippet>

<SwmSnippet path="/clients/java/qa/engine-variable-test/src/main/resources/META-INF/processes.xml" line="1">

---

# Process Definition

The `processes.xml` file is used to define process applications. It specifies the process engine and properties for the process archive. In this case, the process engine is `another-engine` and the property `isScanForProcessDefinitions` is set to `true`.

```xml
<?xml version="1.0" encoding="UTF-8" ?>

<process-application
  xmlns="http://www.camunda.org/schema/1.0/ProcessApplication"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

  <process-archive>
    <process-engine>another-engine</process-engine>
    <properties>
      <property name="isScanForProcessDefinitions">true</property>
    </properties>
  </process-archive>

</process-application>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
