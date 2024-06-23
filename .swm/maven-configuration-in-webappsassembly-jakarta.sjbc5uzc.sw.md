---
title: Maven Configuration in webapps/assembly-jakarta
---
This document provides a detailed explanation of how Maven is used in the `webapps/assembly-jakarta` directory of the project. It will cover the configuration files and their respective steps.

<SwmSnippet path="/webapps/assembly-jakarta/pom.xml" line="1">

---

# Maven Project Configuration

The `pom.xml` file starts by defining the model version and the parent project. It then specifies the artifactId, packaging type, and name of the current project. It also sets up several properties, including the paths for `jakarta.webapp` and `jakarta.runtime`, and versions for various dependencies.

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

  <artifactId>camunda-webapp-jakarta</artifactId>
  <packaging>war</packaging>
  <name>Camunda Platform - Webapp - Assembly Jakarta</name>

  <properties>
    <jakarta.webapp>${project.build.directory}/generated-resources/jakarta-webapp</jakarta.webapp>
    <jakarta.runtime>${project.build.directory}/generated-resources/jakarta-runtime</jakarta.runtime>

    <version.resteasy>6.2.3.Final</version.resteasy>
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/assembly-jakarta/pom.xml" line="35">

---

# Dependency Management

The `dependencyManagement` section is used to manage the versions of various dependencies. It ensures that all dependencies or their transitive dependencies use the same version, which helps avoid potential conflicts.

```xml
  <dependencyManagement>
    <dependencies>
      <dependency>
        <groupId>org.camunda.bpm</groupId>
        <artifactId>camunda-engine-rest-core-jakarta</artifactId>
        <version>${project.version}</version>
      </dependency>
      <dependency>
        <groupId>org.camunda.bpm</groupId>
        <artifactId>camunda-engine-rest-jakarta</artifactId>
        <version>${project.version}</version>
      </dependency>
      <dependency>
        <groupId>jakarta.platform</groupId>
        <artifactId>jakarta.jakartaee-bom</artifactId>
        <version>${version.jakarta-ee-spec}</version>
        <type>pom</type>
        <scope>import</scope>
      </dependency>
      <dependency>
        <groupId>com.fasterxml.jackson</groupId>
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/assembly-jakarta/pom.xml" line="64">

---

# Dependencies

The `dependencies` section lists all the dependencies required by the project. These dependencies will be included in the classpath during both compile-time and runtime.

```xml
  <dependencies>

    <dependency>
      <groupId>com.fasterxml.jackson.jakarta.rs</groupId>
      <artifactId>jackson-jakarta-rs-json-provider</artifactId>
      <exclusions>
        <exclusion>
          <groupId>jakarta.activation</groupId>
          <artifactId>jakarta.activation-api</artifactId>
        </exclusion>
        <exclusion>
          <groupId>jakarta.xml.bind</groupId>
          <artifactId>jakarta.xml.bind-api</artifactId>
        </exclusion>
      </exclusions>
    </dependency>

    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-databind</artifactId>
    </dependency>
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/assembly-jakarta/pom.xml" line="126">

---

# Build Configuration

The `build` section defines how the project should be built. It specifies the final name of the project, and lists the plugins to be used during the build process. Each plugin has its own configuration and executions.

```xml
  <build>
    <finalName>camunda-webapp-jakarta</finalName>

    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-resources-plugin</artifactId>
        <executions>
          <execution>
            <id>copy-resources-assembly</id>
            <phase>prepare-package</phase>
            <goals>
              <goal>copy-resources</goal>
            </goals>
            <configuration>
              <outputDirectory>${basedir}/target/webapp</outputDirectory>
              <resources>
                <resource>
                  <directory>${basedir}/../frontend/target/webapp</directory>
                  <filtering>false</filtering>
                </resource>
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/assembly-jakarta/pom.xml" line="446">

---

# Profiles

The `profiles` section is used to provide different configurations for different environments. Each profile has an id and can specify its own dependencies, properties, and build configurations.

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
