---
title: Maven Configuration in engine-rest/engine-rest
---
This document provides a detailed explanation of how Maven is used in the `engine-rest/engine-rest` directory of the project. It focuses on the configuration and dependencies defined in the `pom.xml` file.

<SwmSnippet path="/engine-rest/engine-rest/pom.xml" line="1">

---

# Project Information

The `pom.xml` file starts by defining the project information. The `modelVersion` is set to `4.0.0`, which is the latest model version of Maven. The `artifactId` is `camunda-engine-rest-core`, which is the identifier of the project artifact. The `packaging` type is `jar`, indicating that the build will produce a JAR file. The project is a child of the `camunda-engine-rest-root` parent project.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <artifactId>camunda-engine-rest-core</artifactId>
  <name>Camunda Platform - engine - REST</name>
  <packaging>jar</packaging>

  <parent>
    <groupId>org.camunda.bpm</groupId>
    <artifactId>camunda-engine-rest-root</artifactId>
    <relativePath>../</relativePath>
    <version>7.22.0-SNAPSHOT</version>
  </parent>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest/pom.xml" line="14">

---

# Project Properties

The `properties` section defines some properties that are used throughout the `pom.xml`. The `version.tomcat` property is set to `7.0.50`, which is the version of Tomcat that will be used. The `rest.http.port` property is set to `38080`, which is the port on which the REST server will listen. The `javax.activation.version` property is set to `1.1.1`, which is the version of the Java Activation Framework that will be used.

```xml
  <properties>
    <!-- pin tomcat version for engine-rest -->
    <version.tomcat>7.0.50</version.tomcat>
    <rest.http.port>38080</rest.http.port>
    <javax.activation.version>1.1.1</javax.activation.version>
  </properties>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest/pom.xml" line="21">

---

# Project Dependencies

The `dependencies` section lists all the dependencies that are needed for the project. These dependencies include libraries for file upload (`commons-fileupload`), JSON processing (`jackson-jaxrs-json-provider`), servlet API (`jboss-servlet-api_3.0_spec`), and the Camunda engine (`camunda-engine`), among others. Some dependencies are marked as `provided`, meaning that they are expected to be supplied by the runtime environment and are not included in the final packaged artifact. Some dependencies are marked as `test`, meaning that they are only needed for compiling and running tests.

```xml
  <dependencies>
    <dependency>
      <groupId>commons-fileupload</groupId>
      <artifactId>commons-fileupload</artifactId>
      <exclusions>
        <exclusion>
          <groupId>commons-io</groupId>
          <artifactId>commons-io</artifactId>
        </exclusion>
      </exclusions>
    </dependency>
    <!-- override managed version from commons-fileupload -->
    <dependency>
      <groupId>commons-io</groupId>
      <artifactId>commons-io</artifactId>
    </dependency>

    <dependency>
      <groupId>com.fasterxml.jackson.jaxrs</groupId>
      <artifactId>jackson-jaxrs-json-provider</artifactId>
      <!--
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest/pom.xml" line="247">

---

# Build Configuration

The `build` section defines how the project should be built. It specifies the resources to be included in the test phase, the plugins to be used during the build, and the configuration for these plugins. For example, the `maven-source-plugin` is used to attach the source code to the project's artifact, and the `maven-jar-plugin` is used to create a JAR file. The `maven-surefire-plugin` is used to run tests, and its configuration includes a system property for the RestEasy version and an argument to increase the maximum heap size for the JVM.

```xml
  <build>
    <testResources>
      <testResource>
        <directory>src/test/resources</directory>
        <filtering>true</filtering>
      </testResource>
    </testResources>

    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-source-plugin</artifactId>
        <executions>
          <execution>
            <!-- This id must match the -Prelease-profile id value or else sources will be "uploaded" twice, which causes Nexus to fail -->
            <id>attach-sources</id>
            <goals>
              <goal>jar</goal>
            </goals>
          </execution>
        </executions>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest/pom.xml" line="316">

---

# Project Profiles

The `profiles` section defines different configurations that can be activated under certain conditions. These profiles can modify the build process by changing properties, changing dependencies, or modifying the build or reporting sections. For example, the `distro` profile skips tests, the `resteasy` profile adds additional dependencies for RestEasy, and the `jersey2` profile activates by default and adds dependencies for Jersey 2.

```xml
  <profiles>
    <profile>
      <id>distro</id>
      <dependencies>
        <dependency>
          <groupId>org.jboss.spec.javax.ws.rs</groupId>
          <artifactId>jboss-jaxrs-api_2.1_spec</artifactId>
          <scope>provided</scope>
        </dependency>
      </dependencies>
      <build>
        <plugins>
          <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-surefire-plugin</artifactId>
            <configuration>
              <skipTests>true</skipTests>
            </configuration>
          </plugin>
        </plugins>
      </build>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
