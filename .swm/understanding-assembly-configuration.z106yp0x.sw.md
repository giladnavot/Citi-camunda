---
title: Understanding Assembly Configuration
---
In the Citi-camunda project, 'Assembly' refers to the configuration files used by Maven Assembly Plugin. These files define how to create a distribution archive (like JAR, WAR) of the project. They specify what files to include in the archive, the format of the archive, and other details. For example, the 'assembly-war-wildfly.xml' file is used to create a WAR file for deployment on WildFly application server. It includes the necessary dependencies and excludes certain files like test and source files.

<SwmSnippet path="/engine-rest/assembly/assembly-classes.xml" line="1">

---

# Assembly Descriptor Files

This is an example of an assembly descriptor file. It specifies that the distribution format should be a JAR (`<format>jar</format>`), the base directory should not be included (`<includeBaseDirectory>false</includeBaseDirectory>`), and no specific files, directories, or dependencies are included or excluded.

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

<SwmSnippet path="/engine-rest/assembly/assembly-war-wildfly.xml" line="1">

---

This is another example of an assembly descriptor file. It specifies that the distribution format should be a WAR (`<format>war</format>`), the base directory should not be included (`<includeBaseDirectory>false</includeBaseDirectory>`), and it includes specific file sets and dependencies.

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

# Assembly Configuration

Assembly in Citi-camunda

## Assembly Overview

Assembly in the Citi-camunda project refers to the configuration and setup of different environments for the application. This is done through XML files located in the engine-rest/assembly directory. Each XML file corresponds to a different environment or setup.

<SwmSnippet path="/engine-rest/assembly/assembly-classes.xml" line="1">

---

## Assembly Files

The `assembly-classes.xml` file is used for setting up the classes for the application.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<assembly xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns="urn:maven:assembly:1.1.2">
  
  <id>classes</id>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/assembly/assembly-war-wildfly.xml" line="1">

---

The `assembly-war-wildfly.xml` file is used for setting up the Wildfly environment for the application.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<assembly xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns="urn:maven:assembly:1.1.2">
  
  <id>wildfly</id>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/assembly/assembly-war-wls.xml" line="1">

---

The `assembly-war-wls.xml` file is used for setting up the WebLogic Server (WLS) environment for the application.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<assembly xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns="urn:maven:assembly:1.1.2">
  
  <id>wls</id>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/assembly/assembly-war-was.xml" line="1">

---

The `assembly-war-was.xml` file is used for setting up the WebSphere Application Server (WAS) environment for the application.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<assembly xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns="urn:maven:assembly:1.1.2">

  <id>was</id>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/assembly/assembly-war-tomcat.xml" line="1">

---

The `assembly-war-tomcat.xml` file is used for setting up the Tomcat environment for the application.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<assembly xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns="urn:maven:assembly:1.1.2">
  
  <id>tomcat</id>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/assembly/assembly-sources.xml" line="1">

---

The `assembly-sources.xml` file is used for setting up the sources for the application.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<assembly xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns="urn:maven:assembly:1.1.2">

  <id>sources</id>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/assembly/assembly-tests.xml" line="1">

---

The `assembly-tests.xml` file is used for setting up the tests for the application.

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
        <include>org.camunda.bpm:camunda-engine-rest-core:jar:tests:*</include>
      </includes>
    </dependencySet>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
