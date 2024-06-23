---
title: 'Handling User Permissions, Group Roles, and Authorizations on Client-Side'
---
This document will cover how user permissions, group roles, and authorizations are handled on the client side in the Citi-camunda repository. We'll cover:

1. The role of the Authorization interface
2. The use of the AuthorizationService interface
3. The use of the AuthorizationQuery interface
4. The use of the Permission interface
5. The use of the AuthorizationCheck class
6. The use of the AuthorizationProperty class.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/authorization/Authorization.java" line="24">

---

# The Role of the Authorization Interface

The Authorization interface is central to handling user permissions, group roles, and authorizations. It assigns a set of permissions to an identity to interact with a given resource. It distinguishes two types of identities: users and groups. An authorization can range over all users, an individual user, or a group of users. It defines the way an identity is allowed to interact with a certain resource through permissions. There are three types of authorizations: Global, Grant, and Revoke.

```java
/**
 * <p>An {@link Authorization} assigns a set of {@link Permission Permissions}
 * to an identity to interact with a given {@link Resource}.</p>
 * <p>EXAMPLES:
 * <ul>
 *   <li>User 'jonny' is authorized to start new instances of the 'invoice' process</li>
 *   <li>Group 'marketing' is not authorized to cancel process instances.</li>
 *   <li>Group 'marketing' is not allowed to use the tasklist application.</li>
 *   <li>Nobody is allowed to edit process variables in the cockpit application,
 *   except the distinct user 'admin'.</li>
 * </ul>
 *
 * <h2>Identities</h2>
 * <p>Camunda Platform distinguishes two types of identities: <em>users</em> and
 * <em>groups</em>. Authorizations can either range over all users
 * (userId = {@link #ANY}), an individual {@link User} or a {@link Group} of users.</p>
 *
 * <h2>Permissions</h2>
 * <p>A {@link Permission} defines the way an identity is allowed to interact
 * with a certain resource. Examples of permissions are {@link Permissions#CREATE CREATE},
 * {@link Permissions#READ READ}, {@link Permissions#UPDATE UPDATE},
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/AuthorizationService.java" line="29">

---

# The Use of the AuthorizationService Interface

The AuthorizationService interface allows managing authorizations. It is used to create an authorization object between a user/group and a resource. It describes the user/group's permissions to access that resource. An authorization object can be configured either for a user or a group and a resource. Finally, the permissions to access that resource can be assigned and the authorization object is saved.

```java
/**
 * <p>The authorization service allows managing {@link Authorization Authorizations}.</p>
 * 
 * <h2>Creating an authorization</h2>
 * <p>An authorization is created between a user/group and a resource. It describes 
 * the user/group's <em>permissions</em> to access that resource. An authorization may 
 * express different permissions, such as the permission to READ, UPDATE, DELETE the 
 * resource. (See {@link Authorization} for details).</p>
 * 
 * <h2>Granting / revoking permissions</h2>
 * <p>In order to grant the permission to access a certain resource, an authorization 
 * object is created:
 * <pre>
 * Authorization auth = authorizationService.createNewAuthorization();
 * //... configure auth
 * authorizationService.saveAuthorization(auth);
 * </pre>
 * The authorization object can be configured either for a user or a group:
 * <pre>
 * auth.setUserId("john");
 *   -OR-
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/authorization/AuthorizationQuery.java" line="25">

---

# The Use of the AuthorizationQuery Interface

The AuthorizationQuery interface is used to select authorizations based on various parameters such as id, type, user ids, group ids, resource type, and resource id. It also allows to check for permissions and order the results.

```java
public interface AuthorizationQuery extends Query<AuthorizationQuery, Authorization> {

  /** only selects authorizations for the given id */
  AuthorizationQuery authorizationId(String id);
  
  /** only selects authorizations for the given type. Legal values:
   * {@link Authorization#AUTH_TYPE_GLOBAL}, {@link Authorization#AUTH_TYPE_GRANT}
   * {@link Authorization#AUTH_TYPE_REVOKE} */
  AuthorizationQuery authorizationType(Integer type);
  
  /** only selects authorizations for the given user ids */
  AuthorizationQuery userIdIn(String... userIds);
  
  /** only selects authorizations for the given group ids */
  AuthorizationQuery groupIdIn(String... groupIds);
  
  /** only selects authorizations for the given resource type */
  AuthorizationQuery resourceType(Resource resource);
  
  /** only selects authorizations for the given resource type */
  AuthorizationQuery resourceType(int resourceType);
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/authorization/Permission.java" line="19">

---

# The Use of the Permission Interface

The Permission interface represents an authorization to interact with a given resource in a specific way. In Camunda Platform, multiple permissions are grouped into an Authorization. For efficient storage and checking of authorizations, the permissions that make up an authorization are coded into a single integer.

```java
/**
 * <p>A permission represents an authorization to interact with a given 
 * resource in a specific way. See {@link Permissions} for a set of built-in 
 * permissions and {@link Authorization} for general overview on authorizations.</p>
 *  
 * <p>In Camunda Platform, multiple permissions are grouped into an {@link Authorization}.
 * For efficient storage and checking of authorizations, the permissons that make
 * up an authorization are coded into a single integer.
 * The implication of this design is that a permission must have a unique integer value 
 * and it must be a power of two, ie 2^0, 2^1, 2^2, 2^3, 2^4 ...
 * 
 * The permission can then be added to an authorization using bitwise OR: 
 * <pre>
 *        Auth: 0000001001001
 * Perm to add: 0000000010000 
 * bit OR (|) : 0000001011001 
 * </pre> 
 * 
 * and removed using bitwise AND of the inverted value: 
 * <pre>
 *        Auth: 0000001001001
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/db/AuthorizationCheck.java" line="31">

---

# The Use of the AuthorizationCheck Class

The AuthorizationCheck class is used as an input for the authorization check algorithm. It contains information about the user, groups, default permissions, and whether the authorization check is enabled or not.

```java
public class AuthorizationCheck implements Serializable {

  private static final long serialVersionUID = 1L;

  /**
   * If true authorization check is enabled. for This switch is
   * useful when implementing a query which may perform an authorization check
   * only under certain circumstances.
   */
  protected boolean isAuthorizationCheckEnabled = false;

  /**
   * If true authorization check is performed.
   */
  protected boolean shouldPerformAuthorizatioCheck = false;

  /**
   * Indicates if the revoke authorization checks are enabled or not.
   * The authorization checks without checking revoke permissions are much more faster.
   */
  protected boolean isRevokeAuthorizationCheckEnabled = false;
```

---

</SwmSnippet>

<SwmSnippet path="/spring-boot-starter/starter/src/main/java/org/camunda/bpm/spring/boot/starter/property/AuthorizationProperty.java" line="21">

---

# The Use of the AuthorizationProperty Class

The AuthorizationProperty class contains properties related to authorization such as whether authorization is enabled, whether authorization for custom code is enabled, the authorization check revokes, and whether tenant check is enabled.

```java
public class AuthorizationProperty {

  /**
   * Enables authorization.
   */
  private boolean enabled = Defaults.INSTANCE.isAuthorizationEnabled();

  /**
   * Enables authorization for custom code.
   */
  private boolean enabledForCustomCode = Defaults.INSTANCE.isAuthorizationEnabledForCustomCode();

  private String authorizationCheckRevokes = Defaults.INSTANCE.getAuthorizationCheckRevokes();

  /**
   * If the value of this flag is set <code>true</code> then the process engine
   * performs tenant checks to ensure that an authenticated user can only access
   * data that belongs to one of his tenants.
   */
  private boolean tenantCheckEnabled = true;

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="follow-up"><sup>Powered by [Swimm](/)</sup></SwmMeta>
