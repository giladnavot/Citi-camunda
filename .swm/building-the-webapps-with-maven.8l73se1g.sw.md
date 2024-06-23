---
title: Building the Webapps with Maven
---
This document provides a detailed explanation of how Maven is used in the webapps directory of the Citi-camunda project. It will go through the configuration steps in the `webapps/pom.xml` file step by step.

<SwmSnippet path="/webapps/pom.xml" line="1">

---

# Maven Project Configuration

The `pom.xml` file starts with the declaration of the project model version, which is `4.0.0` for Maven 2 and 3. The `parent` tag is used to indicate the parent project from which this project inherits properties. Here, the parent project is `camunda-database-settings` with version `7.22.0-SNAPSHOT`. The `artifactId` is `camunda-webapp-root` and the `groupId` is `org.camunda.bpm.webapp`, which together uniquely identify the project in the repository. The `packaging` type is `pom`, indicating that this project is purely for aggregation of modules. The `name` tag provides a human-readable name for the project, which is `Camunda Platform - Webapp - Root`.

```xml
<?xml version="1.0"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">

  <modelVersion>4.0.0</modelVersion>

  <parent>
    <groupId>org.camunda.bpm</groupId>
    <artifactId>camunda-database-settings</artifactId>
    <version>7.22.0-SNAPSHOT</version>
    <relativePath>../database</relativePath>
  </parent>

  <artifactId>camunda-webapp-root</artifactId>
  <groupId>org.camunda.bpm.webapp</groupId>
  <packaging>pom</packaging>
  <name>Camunda Platform - Webapp - Root</name>

```

---

</SwmSnippet>

<SwmSnippet path="/webapps/pom.xml" line="18">

---

# Maven Properties Configuration

The `properties` tag is used to define project-wide properties that can be referenced elsewhere in the `pom.xml`. These properties include the Jetty version, web resources override path, history level, frontend app path, shell to execute commands, and others. These properties are used to customize the build process.

```xml
  <properties>
    <version.jetty>9.4.31.v20200723</version.jetty>

    <web.resources.override>src/main/runtime/default/webapp</web.resources.override>

    <history.level>full</history.level>

    <frontend.app.path>${project.build.directory}/webapp/</frontend.app.path>

    <frontend.development.cockpit.path>${frontend.app.path}</frontend.development.cockpit.path>
    <frontend.development.tasklist.path>${frontend.app.path}</frontend.development.tasklist.path>

    <exec.shell>bash</exec.shell>
    <exec.arg>-c</exec.arg>

    <skip.frontend.build>false</skip.frontend.build>

    <authorizationCheckRevokes>auto</authorizationCheckRevokes>

    <jdbcBatchProcessing>true</jdbcBatchProcessing>

```

---

</SwmSnippet>

<SwmSnippet path="/webapps/pom.xml" line="46">

---

# Maven Dependency Management

The `dependencyManagement` tag is used to manage the versions of dependencies. In this case, the `camunda-core-internal-dependencies` artifact is imported, which means that the versions of its dependencies will be used whenever they are required in this project.

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
    </dependencies>
  </dependencyManagement>
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/pom.xml" line="58">

---

# Maven Dependencies

The `dependencies` tag lists all the dependencies required by this project. These include `camunda-engine`, `camunda-commons-logging`, `junit`, `h2`, `assertj-core`, `mockito-core`, `jetty-webapp`, `jersey-common`, and others. Some dependencies are marked as `provided`, meaning they are required for compiling the project code, but should not be included in the final package as they are provided by the runtime environment. Some dependencies are marked as `test`, meaning they are required for compiling and running tests, but not required for normal runtime.

```xml
  <dependencies>

    <dependency>
      <groupId>org.camunda.bpm</groupId>
      <artifactId>camunda-engine</artifactId>
      <scope>provided</scope>
    </dependency>

    <dependency>
      <groupId>org.camunda.commons</groupId>
      <artifactId>camunda-commons-logging</artifactId>
      <version>${project.version}</version>
      <exclusions>
        <exclusion>
          <groupId>org.slf4j</groupId>
          <artifactId>slf4j-api</artifactId>
        </exclusion>
      </exclusions>
    </dependency>

    <!-- tests -->
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/pom.xml" line="138">

---

# Maven Build Configuration

The `build` tag is used to provide build-specific information. This includes the configuration of the `maven-clean-plugin` to clean the `./frontend/target` directory, the `frontend-maven-plugin` to build the frontend, and other plugins for testing, code generation, and packaging. The `pluginManagement` tag is used to provide configuration details that are shared among multiple plugins.

```xml
  <build>
    <plugins>
      <plugin>
        <artifactId>maven-clean-plugin</artifactId>
        <inherited>false</inherited>
        <configuration>
          <filesets>
            <fileset>
              <directory>./frontend/target</directory>
            </fileset>
          </filesets>
        </configuration>
      </plugin>
      <plugin>
        <groupId>com.github.eirslett</groupId>
        <artifactId>frontend-maven-plugin</artifactId>
        <inherited>false</inherited>
        <configuration>
          <workingDirectory>./frontend</workingDirectory>
          <outputdir>${project.build.directory}/webapp</outputdir>
          <skip>${skip.frontend.build}</skip>
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/pom.xml" line="323">

---

# Maven Modules

The `modules` tag is used to declare modules that should be collected, and their build order. Here, the `assembly` and `assembly-jakarta` modules are declared.

```xml
  <modules>
    <module>assembly</module>
    <module>assembly-jakarta</module>
  </modules>
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/pom.xml" line="328">

---

# Maven Profiles

The `profiles` tag is used to provide specific configurations for different build environments. Here, a profile named `skipFrontendBuild` is defined, which sets the `skip.frontend.build` property to `true`.

```xml
  <profiles>
    <profile>
      <id>skipFrontendBuild</id>
      <properties>
        <skip.frontend.build>true</skip.frontend.build>
      </properties>
    </profile>
  </profiles>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="general-build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
