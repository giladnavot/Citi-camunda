---
title: Understanding the Authorization Engine
---
The Authorization engine in Citi-camunda is a crucial component that manages permissions and access control within the system. It is designed around the concept of an Authorization, which assigns a set of Permissions to an identity (user or group) to interact with a given Resource. The Authorization interface in the system defines three types of authorizations: Global, Grant, and Revoke. Global Authorizations apply to all users and groups and are typically used to set the base permission for a resource. Grant Authorizations apply to specific users or groups and are used to grant a set of permissions. Revoke Authorizations are used to revoke a set of permissions from a user or group. The system also provides a way to check if a specific permission is granted or revoked. The Authorization engine is used extensively across the codebase, ensuring secure and controlled access to various resources.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/authorization/Authorization.java" line="24">

---

# Authorization Interface

This is the Authorization interface. It defines the structure of an Authorization object, which includes methods for managing permissions and identifying the user or group the authorization applies to. It also defines constants for the different types of authorizations.

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

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/authorization/AuthorizationQuery.java" line="25">

---

# Authorization Query Interface

This is the AuthorizationQuery interface. It provides methods for querying authorizations, allowing you to retrieve authorizations based on various criteria such as the authorization ID, type, user ID, group ID, resource type, and resource ID.

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

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/AuthorizationService.java" line="30">

---

# Authorization Service

This is the AuthorizationService interface. It provides methods for managing authorizations, including creating new authorizations, saving authorizations, and creating authorization queries.

```java
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
 * auth.setGroupId("management");
```

---

</SwmSnippet>

# Authorization Engine Overview

This section provides an overview of the Authorization engine in the Citi-camunda repository. It focuses on the Authorization class and the AuthorizationQuery interface, explaining their methods and usage in the codebase.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/authorization/Authorization.java" line="24">

---

## Authorization Class

The Authorization class represents an authorization that assigns a set of permissions to an identity to interact with a given resource. It includes methods to manage permissions, check if a permission is granted or revoked, and get the type of the authorization.

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

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/authorization/AuthorizationQuery.java" line="25">

---

## AuthorizationQuery Interface

The AuthorizationQuery interface provides methods to query authorizations based on various parameters like id, type, user ids, group ids, resource type, and resource id. It also provides methods to order the results by resource type or resource id.

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

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
