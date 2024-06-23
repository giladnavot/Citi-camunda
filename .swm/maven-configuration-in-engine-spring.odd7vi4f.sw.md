---
title: Maven Configuration in engine-spring
---
This document provides a detailed walkthrough of how Maven is used in the <SwmToken path="/engine-spring/core-6/pom.xml" pos="5:6:8" line-data="  &lt;artifactId&gt;camunda-engine-spring-6&lt;/artifactId&gt;">`engine-spring`</SwmToken> module of the project. It will cover the configuration and usage of Maven in the `pom.xml` files located in the <SwmPath>[engine-spring/](/engine-spring/)</SwmPath> directory.

<SwmSnippet path="/engine-spring/pom.xml" line="4">

---

# Parent Configuration in Maven

The <SwmToken path="/engine-spring/pom.xml" pos="4:2:2" line-data="  &lt;parent&gt;">`parent`</SwmToken> tag in the <SwmPath>[engine-spring/pom.xml](/engine-spring/pom.xml)</SwmPath> file specifies the <SwmToken path="/engine-spring/pom.xml" pos="4:2:2" line-data="  &lt;parent&gt;">`parent`</SwmToken> project from which this module inherits configuration. The <SwmToken path="/engine-spring/core-6/pom.xml" pos="46:2:2" line-data="      &lt;groupId&gt;org.camunda.bpm&lt;/groupId&gt;">`groupId`</SwmToken>, <SwmToken path="/engine-spring/core-6/pom.xml" pos="47:2:2" line-data="      &lt;artifactId&gt;camunda-engine&lt;/artifactId&gt;">`artifactId`</SwmToken>, and <SwmToken path="/engine-spring/pom.xml" pos="8:2:2" line-data="    &lt;version&gt;7.22.0-SNAPSHOT&lt;/version&gt;">`version`</SwmToken> tags identify the parent project. The <SwmToken path="/engine-spring/pom.xml" pos="7:2:2" line-data="    &lt;relativePath&gt;../database&lt;/relativePath&gt;">`relativePath`</SwmToken> tag is used to locate the parent project in the file system.

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

The <SwmToken path="/engine-spring/core-6/pom.xml" pos="47:2:2" line-data="      &lt;artifactId&gt;camunda-engine&lt;/artifactId&gt;">`artifactId`</SwmToken> tag specifies the identifier of the artifact (the project) that is being built. The <SwmToken path="/engine-spring/pom.xml" pos="13:2:2" line-data="  &lt;packaging&gt;pom&lt;/packaging&gt;">`packaging`</SwmToken> tag defines how the project should be packaged. The <SwmToken path="/engine-spring/pom.xml" pos="14:2:2" line-data="  &lt;name&gt;Camunda Platform - engine - Spring - Root&lt;/name&gt;">`name`</SwmToken> tag provides a human-readable name for the project.

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

The <SwmToken path="/engine-spring/pom.xml" pos="26:2:2" line-data="      &lt;modules&gt;">`modules`</SwmToken> tag is used to specify the modules of the project. Each <SwmToken path="/engine-spring/pom.xml" pos="17:2:2" line-data="    &lt;module&gt;core&lt;/module&gt;">`module`</SwmToken> tag within the <SwmToken path="/engine-spring/pom.xml" pos="26:2:2" line-data="      &lt;modules&gt;">`modules`</SwmToken> tag represents a module of the project.

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

The <SwmToken path="/engine-spring/pom.xml" pos="20:2:2" line-data="  &lt;profiles&gt;">`profiles`</SwmToken> tag is used to provide specific settings under certain situations. Each <SwmToken path="/engine-spring/pom.xml" pos="21:2:2" line-data="    &lt;profile&gt;">`profile`</SwmToken> tag within the <SwmToken path="/engine-spring/pom.xml" pos="20:2:2" line-data="  &lt;profiles&gt;">`profiles`</SwmToken> tag represents a profile. The <SwmToken path="/engine-spring/pom.xml" pos="22:2:2" line-data="      &lt;id&gt;jdk17&lt;/id&gt;">`id`</SwmToken> tag is used to identify the profile. The <SwmToken path="/engine-spring/pom.xml" pos="23:2:2" line-data="      &lt;activation&gt;">`activation`</SwmToken> tag is used to specify when the profile is active. The <SwmToken path="/engine-spring/pom.xml" pos="26:2:2" line-data="      &lt;modules&gt;">`modules`</SwmToken> tag within the <SwmToken path="/engine-spring/pom.xml" pos="21:2:2" line-data="    &lt;profile&gt;">`profile`</SwmToken> tag is used to specify the modules of the profile.

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

The <SwmToken path="/engine-spring/core-6/pom.xml" pos="44:2:2" line-data="  &lt;dependencies&gt;">`dependencies`</SwmToken> tag is used to specify the dependencies of the project. Each <SwmToken path="/engine-spring/core-6/pom.xml" pos="45:2:2" line-data="    &lt;dependency&gt;">`dependency`</SwmToken> tag within the <SwmToken path="/engine-spring/core-6/pom.xml" pos="44:2:2" line-data="  &lt;dependencies&gt;">`dependencies`</SwmToken> tag represents a dependency. The <SwmToken path="/engine-spring/core-6/pom.xml" pos="46:2:2" line-data="      &lt;groupId&gt;org.camunda.bpm&lt;/groupId&gt;">`groupId`</SwmToken>, <SwmToken path="/engine-spring/core-6/pom.xml" pos="47:2:2" line-data="      &lt;artifactId&gt;camunda-engine&lt;/artifactId&gt;">`artifactId`</SwmToken>, and <SwmToken path="/engine-spring/pom.xml" pos="8:2:2" line-data="    &lt;version&gt;7.22.0-SNAPSHOT&lt;/version&gt;">`version`</SwmToken> tags identify the dependency. The <SwmToken path="/engine-spring/core-6/pom.xml" pos="52:2:2" line-data="      &lt;scope&gt;provided&lt;/scope&gt;">`scope`</SwmToken> tag is used to limit the dependency's scope.

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

The <SwmToken path="/engine-spring/core-6/pom.xml" pos="171:2:2" line-data="  &lt;build&gt;">`build`</SwmToken> tag is used to provide build-specific information. The <SwmToken path="/engine-spring/core-6/pom.xml" pos="172:2:2" line-data="    &lt;plugins&gt;">`plugins`</SwmToken> tag within the <SwmToken path="/engine-spring/core-6/pom.xml" pos="171:2:2" line-data="  &lt;build&gt;">`build`</SwmToken> tag is used to specify the plugins used during the build process.

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

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda"><sup>Powered by [Swimm](https://app.swimm.io/)</sup></SwmMeta>
