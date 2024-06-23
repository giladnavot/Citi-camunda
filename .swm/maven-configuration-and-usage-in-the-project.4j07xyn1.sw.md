---
title: Maven Configuration and Usage in the Project
---
This document provides a detailed walkthrough of how Maven is used in the Citi-camunda project. It will cover the configuration and usage of Maven in the project, citing code from the Maven configuration files.

<SwmSnippet path="/pom.xml" line="4">

---

# Maven Parent Configuration

The Maven project is defined with a parent project, which is the `camunda-bpm-release-parent`. This parent project provides common configurations for all child projects. The version of the parent project is specified as `2.3.0`.

```xml
  <parent>
    <groupId>org.camunda</groupId>
    <artifactId>camunda-bpm-release-parent</artifactId>
    <version>2.3.0</version>
    <!-- do not remove empty tag - http://jira.codehaus.org/browse/MNG-4687 -->
    <relativePath />
  </parent>
```

---

</SwmSnippet>

<SwmSnippet path="/pom.xml" line="12">

---

# Maven Project Information

The Maven project's group ID is `org.camunda.bpm`, and the artifact ID is `camunda-root`. The version of the project is `7.22.0-SNAPSHOT`. The packaging type is `pom`, which means this project is expected to produce a POM that other projects can import into their projects to use the dependencies and configurations of this project.

```xml
  <groupId>org.camunda.bpm</groupId>
  <artifactId>camunda-root</artifactId>
  <version>7.22.0-SNAPSHOT</version>
  <packaging>pom</packaging>
  <name>Camunda Platform - Root Pom</name>
  <inceptionYear>2013</inceptionYear>
```

---

</SwmSnippet>

<SwmSnippet path="/pom.xml" line="24">

---

# Maven Properties

The properties section defines some common properties that can be used in the POM file. These properties include versions of dependencies such as `mybatis`, `joda-time`, `uuid-generator`, and `feel-scala`.

```xml
  <properties>
    <license.includeTransitiveDependencies>false</license.includeTransitiveDependencies>

    <!-- These properties are used in both the BOM as well as camunda-parent and subprojects -->
    <version.mybatis>3.5.15</version.mybatis>
    <version.joda-time>2.12.5</version.joda-time>
    <version.uuid-generator>4.3.0</version.uuid-generator>
    <version.feel-scala>1.17.5</version.feel-scala>
  </properties>
```

---

</SwmSnippet>

<SwmSnippet path="/pom.xml" line="34">

---

# Maven Build Plugins

The build section defines the plugins used during the build process. Here, the `license-maven-plugin` is used with version `1.14`. This plugin is used to check and update file headers, and also to generate a report of third-party dependencies.

```xml
  <build>
    <plugins>
      <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>license-maven-plugin</artifactId>
        <version>1.14</version>
        <configuration>
          <acceptPomPackaging>true</acceptPomPackaging>
          <excludedScopes>test</excludedScopes>
        </configuration>
      </plugin>
```

---

</SwmSnippet>

<SwmSnippet path="/pom.xml" line="48">

---

# Maven Profiles

The profiles section defines different build profiles. Each profile has a unique ID and can specify different build configurations. For example, the `distro` profile is activated by default and includes modules like `spring-boot-starter`, `quarkus-extension`, `qa`, and others. The `distro-ce` profile is also activated by default and includes modules like `spring-boot-starter`, `distro/license-book`, `distro/jboss`, and `distro/tomcat`.

```xml
  <profiles>
    <!-- distro profile is default and builds the complete distribution.
         Does not run integration tests. -->
    <profile>
      <id>distro</id>
      <activation>
        <activeByDefault>true</activeByDefault>
      </activation>
      <modules>
        <!-- This profile is run in the CI as the first step (platform-ASSEMBLY); It must not activate
          any modules that have a dependency to the webapps. See also the referenced POMs,
          they usually define which modules are covered by the distro profile -->
        <module>spring-boot-starter</module>

        <module>quarkus-extension</module>

        <module>qa</module>

        <module>javaee/ejb-service</module>
        <module>javaee/ejb-client</module>
        <module>javaee/ejb-client-jakarta</module>
```

---

</SwmSnippet>

<SwmSnippet path="/pom.xml" line="311">

---

# Maven Repositories

The repositories section defines where Maven looks for dependencies. Three repositories are defined: Maven Central, Camunda Platform Maven Repository, and Camunda Nexus.

```xml
  <repositories>
    <repository>
      <id>maven-central</id>
      <name>Maven Central</name>
      <url>https://repo1.maven.org/maven2</url>
      <snapshots>
        <enabled>false</enabled>
      </snapshots>
    </repository>
    <repository>
      <!-- Required for local builds by community users on master branch -->
      <id>camunda-public-repository</id>
      <name>Camunda Platform Maven Repository</name>
      <url>https://artifacts.camunda.com/artifactory/public/</url>
    </repository>
    <repository>
      <!-- Required for local builds by developers on maintainance branches -->
      <id>camunda-nexus</id>
      <name>Camunda Nexus</name>
      <url>https://artifacts.camunda.com/artifactory/internal</url>
    </repository>
```

---

</SwmSnippet>

<SwmSnippet path="/mvnw" line="38">

---

# Maven Environment Variables

The Maven wrapper script `mvnw` checks for the existence of environment variables in `/etc/mavenrc` and `/usr/local/etc/mavenrc`, and if they exist, the script sources them. These files can be used to set environment variables that affect the behavior of Maven.

```
  if [ -f /usr/local/etc/mavenrc ] ; then
    . /usr/local/etc/mavenrc
  fi

  if [ -f /etc/mavenrc ] ; then
    . /etc/mavenrc
  fi
```

---

</SwmSnippet>

<SwmSnippet path="/mvnw" line="135">

---

# Maven Base Directory

The `find_maven_basedir` function in `mvnw` is used to find the base directory of the Maven project. It traverses the directory structure from the current working directory to the filesystem root. The first directory with a `.mvn` subdirectory is considered the project base directory.

```
# traverses directory structure from process work directory to filesystem root
# first directory with .mvn subdirectory is considered project base directory
find_maven_basedir() {
  if [ -z "$1" ]
  then
    echo "Path not specified to find_maven_basedir"
    return 1
  fi

  basedir="$1"
  wdir="$1"
  while [ "$wdir" != '/' ] ; do
    if [ -d "$wdir"/.mvn ] ; then
      basedir=$wdir
      break
    fi
    # workaround for JBEAP-8937 (on Solaris 10/Sparc)
    if [ -d "${wdir}" ]; then
      wdir=$(cd "$wdir/.." || exit 1; pwd)
    fi
    # end of workaround
```

---

</SwmSnippet>

<SwmSnippet path="/distro/wildfly26/modules/assembly.xml" line="1">

---

# Maven Assembly Files

The `assembly.xml` file in the `distro/wildfly26/modules` directory is a Maven Assembly descriptor. It is used to create a distribution archive of the project.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<assembly xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns="urn:maven:assembly:1.1.2">

  <id>assemble</id>
```

---

</SwmSnippet>

<SwmSnippet path="/distro/sql-script/assembly.xml" line="1">

---

The `assembly.xml` file in the `distro/sql-script` directory is another Maven Assembly descriptor. It is used to create a distribution archive of the SQL scripts in the project.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<assembly xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns="urn:maven:assembly:1.1.2">
  
  <id>artifacts</id>
```

---

</SwmSnippet>

<SwmSnippet path="/distro/wildfly/distro/assembly.xml" line="1">

---

The `assembly.xml` file in the `distro/wildfly/distro` directory is a Maven Assembly descriptor. It is used to create a distribution archive of the project for the WildFly application server.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<assembly xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns="urn:maven:assembly:1.1.2">
  
  <id>distro</id>
```

---

</SwmSnippet>

<SwmSnippet path="/distro/tomcat/distro/assembly.xml" line="1">

---

The `assembly.xml` file in the `distro/tomcat/distro` directory is a Maven Assembly descriptor. It is used to create a distribution archive of the project for the Tomcat server.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<assembly xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          xmlns="urn:maven:assembly:1.1.2">

  <id>distro</id>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="general-build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
