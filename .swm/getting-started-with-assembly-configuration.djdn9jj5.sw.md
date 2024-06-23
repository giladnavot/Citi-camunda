---
title: Getting Started with Assembly Configuration
---
In the context of the Citi-camunda repository, 'Assembly' refers to the configuration files used by Maven Assembly Plugin. These files define how to create a distribution archive (like JAR, WAR) of the project. They specify the format of the archive, whether to include the base directory, and what dependencies, file sets, and other elements to include in the archive. For example, the 'assembly-war-wildfly.xml' file is used to create a WAR file for deployment on WildFly application server, including specific dependencies and excluding certain files.

<SwmSnippet path="/engine-rest/assembly/assembly-classes.xml" line="1">

---

# Assembly Definition

This is an example of an assembly definition file. It specifies that the assembly id is 'classes' and the format of the assembly is 'jar'. The 'includeBaseDirectory' is set to false, meaning the base directory of the project is not included in the assembly.

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

# Assembly with Dependencies

This assembly file is more complex. It includes 'fileSets' and 'dependencySets'. 'fileSets' specify the files to be included in the assembly. 'dependencySets' specify the project dependencies to be included in the assembly. The 'unpack' option is set to true, meaning the dependencies are unpacked into the specified directory.

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

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
