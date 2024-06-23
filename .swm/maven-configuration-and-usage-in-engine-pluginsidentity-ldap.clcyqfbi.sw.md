---
title: Maven Configuration and Usage in engine-plugins/identity-ldap
---
This document provides a detailed walkthrough of how Maven is used in the `engine-plugins/identity-ldap` directory of the project.

<SwmSnippet path="/engine-plugins/identity-ldap/pom.xml" line="1">

---

# Maven Project Configuration

The `pom.xml` file starts by defining the project model version, group ID, artifact ID, packaging type, and name. It also specifies the parent project, which is `camunda-engine-plugins`.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>org.camunda.bpm.identity</groupId>
  <artifactId>camunda-identity-ldap</artifactId>
  <packaging>jar</packaging>
  <name>Camunda Platform - engine plugins - identity - ldap</name>

  <parent>
    <groupId>org.camunda.bpm</groupId>
    <artifactId>camunda-engine-plugins</artifactId>
    <version>7.22.0-SNAPSHOT</version>
  </parent>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-plugins/identity-ldap/pom.xml" line="15">

---

Next, properties for the LDAP server ports are defined.

```xml
  <properties>
    <ldap.server.port>10389</ldap.server.port>
    <ldap.server.port.posix>5027</ldap.server.port.posix>
  </properties>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-plugins/identity-ldap/pom.xml" line="20">

---

# Maven Dependencies

The dependencies section includes all the necessary libraries for the project. This includes `camunda-commons-logging`, Apache Directory Server for testing, `commons-io` for IO operations in tests, and `logback-classic` for logging in tests.

```xml
  <dependencies>
    <dependency>
      <groupId>org.camunda.commons</groupId>
      <artifactId>camunda-commons-logging</artifactId>
      <version>${project.version}</version>
    </dependency>

    <!-- LDAP Libraries to start test server -->
    <dependency>
      <groupId>org.apache.directory.server</groupId>
      <artifactId>apacheds-all</artifactId>
      <exclusions>
        <exclusion>
          <groupId>org.apache.directory.shared</groupId>
          <artifactId>shared-ldap</artifactId>
        </exclusion>
      </exclusions>
      <scope>test</scope>
    </dependency>

    <dependency>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-plugins/identity-ldap/pom.xml" line="54">

---

# Maven Build Configuration

The build configuration specifies the resources for testing and the plugins used. The `maven-surefire-plugin` is configured to not fail if no tests are found, not trim stack traces, and redirect test output to a file.

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
        <artifactId>maven-surefire-plugin</artifactId>
        <configuration>
          <failIfNoTests>false</failIfNoTests>
          <trimStackTrace>false</trimStackTrace>
          <redirectTestOutputToFile>true</redirectTestOutputToFile>
        </configuration>
      </plugin>
    </plugins>
  </build>
```

---

</SwmSnippet>

<SwmSnippet path="/engine-plugins/identity-ldap/src/main/java/org/camunda/bpm/identity/impl/ldap/plugin/LdapIdentityProviderPlugin.java" line="44">

---

# LdapIdentityProviderPlugin Configuration

The `preInit` method in `LdapIdentityProviderPlugin` is called during the initialization of the process engine. It logs the activation of the plugin, accepts untrusted certificates if configured to do so, and sets the identity provider session factory to `LdapIdentityProviderFactory`.

```java
  public void preInit(ProcessEngineConfigurationImpl processEngineConfiguration) {

    LdapPluginLogger.INSTANCE.pluginActivated(getClass().getSimpleName(), processEngineConfiguration.getProcessEngineName());

    if(acceptUntrustedCertificates) {
      CertificateHelper.acceptUntrusted();
      LdapPluginLogger.INSTANCE.acceptingUntrustedCertificates();
    }

    LdapIdentityProviderFactory ldapIdentityProviderFactory = new LdapIdentityProviderFactory();
    ldapIdentityProviderFactory.setLdapConfiguration(this);
    processEngineConfiguration.setIdentityProviderSessionFactory(ldapIdentityProviderFactory);

  }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="build-tool"><sup>Powered by [Swimm](/)</sup></SwmMeta>
