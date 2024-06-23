---
title: Getting Started with Assembly Jakarta
---
Assembly Jakarta in the Citi-camunda project refers to a specific configuration used for building the project with Jakarta EE (Enterprise Edition) specifications. This configuration is defined in the 'assembly-jakarta' directory under 'engine-rest'. It contains XML files that specify how the project should be assembled for different environments and purposes, such as 'assembly-classes.xml', 'assembly-war-wildfly.xml', 'assembly-sources.xml', and 'assembly-tests.xml'. These files are used by Maven, a build automation tool used in Java projects, to package the application in different formats like JAR and WAR.

<SwmSnippet path="/engine-rest/assembly-jakarta/assembly-classes.xml" line="1">

---

# Assembly XML Files

This is an example of an assembly XML file. It defines the format of the assembly as a JAR and specifies that the base directory should not be included.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<assembly xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns="urn:maven:assembly:1.1.2">
  
  <id>classes</id>
  
  <formats>
    <format>jar</format>
  </formats>

  <includeBaseDirectory>false</includeBaseDirectory>
  
</assembly>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/assembly-jakarta/assembly-war-wildfly.xml" line="1">

---

This assembly XML file is used to create a WAR file for Wildfly. It includes specific dependencies and files for Wildfly.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<assembly xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns="urn:maven:assembly:1.1.2">

  <id>wildfly</id>

  <formats>
    <format>war</format>
  </formats>

  <includeBaseDirectory>false</includeBaseDirectory>

  <fileSets>
    <fileSet>
      <directory>src/main/runtime/wildfly/webapp</directory>
      <outputDirectory>/</outputDirectory>
    </fileSet>
  </fileSets>

  <dependencySets>
    <dependencySet>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/assembly-jakarta/pom.xml" line="1">

---

# pom.xml File

The pom.xml file is used to configure the Maven build. It specifies the dependencies for the assembly and configures the maven-assembly-plugin to create the assemblies.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <artifactId>camunda-engine-rest-jakarta</artifactId>
  <name>Camunda Platform - engine - REST - Assembly Jakarta</name>
  <packaging>war</packaging>

  <parent>
    <groupId>org.camunda.bpm</groupId>
    <artifactId>camunda-engine-rest-root</artifactId>
    <version>7.22.0-SNAPSHOT</version>
  </parent>

  <properties>
    <!-- generate a bom of dependencies for the license book.
    We include compile and provided scope dependencies;
    all the dependencies that we include in only one of the
    runtime-specific-WARs are in provided scope -->
    <skip-third-party-bom>false</skip-third-party-bom>
    <third-party-bom-scopes>compile|provided</third-party-bom-scopes>
  </properties>
```

---

</SwmSnippet>

# Assembly Jakarta

Assembly Jakarta is a part of the engine-rest module in the Citi-camunda project. It contains several XML files and a pom.xml file.

<SwmSnippet path="/engine-rest/assembly-jakarta/assembly-classes.xml" line="1">

---

## Assembly Jakarta

The `assembly-classes.xml` file defines the assembly configuration for classes. The `id` element specifies the identifier of the assembly.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<assembly xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns="urn:maven:assembly:1.1.2">
  
  <id>classes</id>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/assembly-jakarta/assembly-tests.xml" line="1">

---

The `assembly-tests.xml` file defines the assembly configuration for tests. It specifies the format, directory structure, and dependencies for the assembly.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<assembly xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns="urn:maven:assembly:1.1.2">

  <id>tests</id>

  <formats>
    <format>jar</format>
  </formats>

  <includeBaseDirectory>false</includeBaseDirectory>

  <dependencySets>
    <dependencySet>
      <outputDirectory>/</outputDirectory>
      <unpack>true</unpack>
      <scope>provided</scope>
      <includes>
        <include>org.camunda.bpm:camunda-engine-rest-core-jakarta:jar:tests:*</include>
      </includes>
    </dependencySet>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/assembly-jakarta/pom.xml" line="1">

---

The `pom.xml` file defines the project object model. It specifies the artifact ID, name, packaging, parent project, properties, dependencies, and build configuration for the project.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <artifactId>camunda-engine-rest-jakarta</artifactId>
  <name>Camunda Platform - engine - REST - Assembly Jakarta</name>
  <packaging>war</packaging>

  <parent>
    <groupId>org.camunda.bpm</groupId>
    <artifactId>camunda-engine-rest-root</artifactId>
    <version>7.22.0-SNAPSHOT</version>
  </parent>

  <properties>
    <!-- generate a bom of dependencies for the license book.
    We include compile and provided scope dependencies;
    all the dependencies that we include in only one of the
    runtime-specific-WARs are in provided scope -->
    <skip-third-party-bom>false</skip-third-party-bom>
    <third-party-bom-scopes>compile|provided</third-party-bom-scopes>
  </properties>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
