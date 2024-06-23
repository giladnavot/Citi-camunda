---
title: Maven Configuration in engine-spring
---
This document provides a detailed walkthrough of how Maven is used in the `engine-spring` module of the project. It will cover the configuration and usage of Maven in the `pom.xml` files located in the `engine-spring` directory.

<SwmSnippet path="/engine-spring/pom.xml" line="4">

---

# Parent Configuration in Maven

The `parent` tag in the `pom.xml` file specifies the parent project from which this module inherits configuration. The `groupId`, `artifactId`, and `version` tags identify the parent project. The `relativePath` tag is used to locate the parent project in the file system.

```xml
  <parent>
    <groupId>org.camunda.bpm</groupId>
    <artifactId>camunda-database-settings</artifactId>
    <relativePath>../database</relativePath>
    <version>7.22.0-SNAPSHOT</version>
  </parent>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-spring/pom.xml" line="11">

---

# Artifact Configuration in Maven

The `artifactId` tag specifies the identifier of the artifact (the project) that is being built. The `packaging` tag defines how the project should be packaged. The `name` tag provides a human-readable name for the project.

```xml
  <artifactId>camunda-spring-compatibility-root</artifactId>

  <packaging>pom</packaging>
  <name>Camunda Platform - engine - Spring - Root</name>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-spring/pom.xml" line="16">

---

# Modules Configuration in Maven

The `modules` tag is used to specify the modules of the project. Each `module` tag within the `modules` tag represents a module of the project.

```xml
  <modules>
    <module>core</module>
  </modules>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-spring/pom.xml" line="20">

---

# Profiles Configuration in Maven

The `profiles` tag is used to provide specific settings under certain situations. Each `profile` tag within the `profiles` tag represents a profile. The `id` tag is used to identify the profile. The `activation` tag is used to specify when the profile is active. The `modules` tag within the `profile` tag is used to specify the modules of the profile.

```xml
  <profiles>
    <profile>
      <id>jdk17</id>
      <activation>
        <jdk>[17,)</jdk>
      </activation>
      <modules>
        <module>core-6</module>
      </modules>
    </profile>
  </profiles>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-spring/core-6/pom.xml" line="44">

---

# Dependencies Configuration in Maven

The `dependencies` tag is used to specify the dependencies of the project. Each `dependency` tag within the `dependencies` tag represents a dependency. The `groupId`, `artifactId`, and `version` tags identify the dependency. The `scope` tag is used to limit the dependency's scope.

```xml
  <dependencies>
    <dependency>
      <groupId>org.camunda.bpm</groupId>
      <artifactId>camunda-engine</artifactId>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <scope>provided</scope>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-jdbc</artifactId>
      <scope>provided</scope>
    </dependency>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-tx</artifactId>
      <scope>provided</scope>
    </dependency>
    <dependency>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-spring/core-6/pom.xml" line="171">

---

# Build Configuration in Maven

The `build` tag is used to provide build-specific information. The `plugins` tag within the `build` tag is used to specify the plugins used during the build process.

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
              <outputDirectory>${project.build.directory}/generated-sources/java</outputDirectory>
               <resources>
                <resource>
                  <directory>${basedir}/../core/src/main/java</directory>
                  <filtering>false</filtering>
                </resource>
              </resources>
            </configuration>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
