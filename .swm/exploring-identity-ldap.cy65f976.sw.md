---
title: Exploring Identity LDAP
---
Identity LDAP in the Citi-camunda project refers to the implementation of LDAP (Lightweight Directory Access Protocol) for identity management. It is primarily handled by the `LdapIdentityProviderSession` class, which implements the `ReadOnlyIdentityProvider` interface. This class is responsible for managing the LDAP configuration and client, and provides methods for user and group queries.

The `LdapIdentityProviderSession` class is initialized with an `LdapConfiguration` object, which holds the configuration details for the LDAP connection. This class also uses an `LdapClient` to interact with the LDAP server.

The `LdapIdentityProviderSession` class is used in various places in the codebase. For example, it is used in `LdapGroupQuery.java` and `LdapUserQueryImpl.java` to execute user and group queries. It is also used in `LdapIdentityProviderFactory.java` to open a new session.

The `LdapIdentityProviderFactory` class is responsible for creating new instances of `LdapIdentityProviderSession`. It holds an `LdapConfiguration` object, which can be set using the `setLdapConfiguration` method.

The `LdapIdentityProviderPlugin` class extends `LdapConfiguration` and implements the `ProcessEnginePlugin` interface. This class is responsible for initializing the `LdapIdentityProviderFactory` and setting the LDAP configuration.

<SwmSnippet path="/engine-plugins/identity-ldap/src/main/java/org/camunda/bpm/identity/impl/ldap/LdapIdentityProviderSession.java" line="70">

---

# LdapIdentityProviderSession Class

The LdapIdentityProviderSession class is the main class for interacting with the LDAP server. It contains methods for querying users and groups, and for managing the session lifecycle.

```java
public class LdapIdentityProviderSession implements ReadOnlyIdentityProvider {

  protected LdapConfiguration ldapConfiguration;

  protected LdapClient ldapClient;

  public LdapIdentityProviderSession(LdapConfiguration ldapConfiguration) {
    this.ldapConfiguration = ldapConfiguration;
    this.ldapClient = new LdapClient(ldapConfiguration);
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine-plugins/identity-ldap/src/main/java/org/camunda/bpm/identity/impl/ldap/LdapConfiguration.java" line="31">

---

# LdapConfiguration Class

The LdapConfiguration class is used to hold the configuration details for the LDAP server. It includes properties such as the server URL, manager DN and password, base DN, user and group search base and filters, and various other LDAP-related settings.

```java
public class LdapConfiguration {

  public static String LDAP_QUERY_WILDCARD = "*";
  public static String DB_QUERY_WILDCARD = "%";

  protected String initialContextFactory = "com.sun.jndi.ldap.LdapCtxFactory";
  protected String securityAuthentication = "simple";

  protected Map<String, String> contextProperties = new HashMap<>();

  protected String serverUrl;
  protected String managerDn = "";
  protected String managerPassword = "";

  protected String baseDn = "";

  protected String userDnPattern = "";

  protected String userSearchBase = "";
  protected String userSearchFilter = "(objectclass=person)";

```

---

</SwmSnippet>

<SwmSnippet path="/engine-plugins/identity-ldap/src/main/java/org/camunda/bpm/identity/impl/ldap/plugin/LdapIdentityProviderPlugin.java" line="40">

---

# LdapIdentityProviderPlugin Class

The LdapIdentityProviderPlugin class extends the LdapConfiguration class and implements the ProcessEnginePlugin interface. This allows it to be used as a plugin in the Camunda BPM platform, providing LDAP identity provider support.

```java
public class LdapIdentityProviderPlugin extends LdapConfiguration implements ProcessEnginePlugin {

  protected boolean acceptUntrustedCertificates = false;

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

  public void postInit(ProcessEngineConfigurationImpl processEngineConfiguration) {
    // nothing to do
```

---

</SwmSnippet>

# Identity LDAP Functions

This section will cover the main functions related to Identity LDAP in the Citi-camunda repository. These functions are primarily used for managing user identities and groups in the LDAP system.

<SwmSnippet path="/engine-plugins/identity-ldap/src/main/java/org/camunda/bpm/identity/impl/ldap/LdapIdentityProviderSession.java" line="70">

---

## LdapIdentityProviderSession

The `LdapIdentityProviderSession` class implements the `ReadOnlyIdentityProvider` interface. It is used to manage user sessions in the LDAP system. It includes methods for user and group queries, as well as session lifecycle management such as `flush` and `close` methods.

```java
public class LdapIdentityProviderSession implements ReadOnlyIdentityProvider {

  protected LdapConfiguration ldapConfiguration;

  protected LdapClient ldapClient;

  public LdapIdentityProviderSession(LdapConfiguration ldapConfiguration) {
    this.ldapConfiguration = ldapConfiguration;
    this.ldapClient = new LdapClient(ldapConfiguration);
  }

  // Session Lifecycle //////////////////////////////////

  public void flush() {
    // nothing to do
  }

  public void close() {
    ldapClient.closeLdapCtx();
  }

```

---

</SwmSnippet>

<SwmSnippet path="/engine-plugins/identity-ldap/src/main/java/org/camunda/bpm/identity/impl/ldap/LdapIdentityProviderFactory.java" line="27">

---

## LdapIdentityProviderFactory

The `LdapIdentityProviderFactory` class is used to create instances of `LdapIdentityProviderSession`. It contains a reference to `LdapConfiguration` which holds the configuration for the LDAP system.

```java
public class LdapIdentityProviderFactory implements SessionFactory {

  protected LdapConfiguration ldapConfiguration;
  
  public Class<?> getSessionType() {
    return ReadOnlyIdentityProvider.class;
  }

  public Session openSession() {
    return new LdapIdentityProviderSession(ldapConfiguration);
  }
  
  public LdapConfiguration getLdapConfiguration() {
    return ldapConfiguration;
  }
  
  public void setLdapConfiguration(LdapConfiguration ldapConfiguration) {
    this.ldapConfiguration = ldapConfiguration;
  }

}
```

---

</SwmSnippet>

<SwmSnippet path="/engine-plugins/identity-ldap/src/main/java/org/camunda/bpm/identity/impl/ldap/LdapConfiguration.java" line="31">

---

## LdapConfiguration

The `LdapConfiguration` class holds the configuration for the LDAP system. It includes properties such as the initial context factory, security authentication, server URL, manager DN and password, base DN, user and group search base and filters, and various attribute names.

```java
public class LdapConfiguration {

  public static String LDAP_QUERY_WILDCARD = "*";
  public static String DB_QUERY_WILDCARD = "%";

  protected String initialContextFactory = "com.sun.jndi.ldap.LdapCtxFactory";
  protected String securityAuthentication = "simple";

  protected Map<String, String> contextProperties = new HashMap<>();

  protected String serverUrl;
  protected String managerDn = "";
  protected String managerPassword = "";

  protected String baseDn = "";

  protected String userDnPattern = "";

  protected String userSearchBase = "";
  protected String userSearchFilter = "(objectclass=person)";

```

---

</SwmSnippet>

<SwmSnippet path="/engine-plugins/identity-ldap/src/main/java/org/camunda/bpm/identity/impl/ldap/LdapClient.java" line="44">

---

## LdapClient

The `LdapClient` class is used to interact with the LDAP server. It includes methods for opening and closing the LDAP context, performing searches, and handling request and response controls.

```java
public class LdapClient {

  protected LdapContext initialContext;
  protected LdapConfiguration ldapConfiguration;

  public LdapClient(LdapConfiguration ldapConfiguration) {
    this.ldapConfiguration = ldapConfiguration;
  }

  protected void ensureContextInitialized() {
    if (initialContext == null) {
      initialContext = openContext();
    }
  }

  public LdapContext openContext(String dn, String password) {
    Hashtable<String, String> env = new Hashtable<>();
    env.put(Context.INITIAL_CONTEXT_FACTORY, ldapConfiguration.getInitialContextFactory());
    env.put(Context.SECURITY_AUTHENTICATION, ldapConfiguration.getSecurityAuthentication());
    env.put(Context.PROVIDER_URL, ldapConfiguration.getServerUrl());
    env.put(Context.SECURITY_PRINCIPAL, dn);
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
