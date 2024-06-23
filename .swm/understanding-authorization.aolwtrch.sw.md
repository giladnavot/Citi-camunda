---
title: Understanding Authorization
---
Authorization in Citi-camunda refers to the process of granting or denying permissions to a user or a group to interact with a given resource. It is implemented through the `Authorization` interface, which assigns a set of permissions to an identity (user or group). The permissions define how an identity can interact with a resource, such as creating, reading, updating, or deleting it. The resources are the entities the user interacts with, such as groups, users, process definitions, process instances, tasks, etc. There are three types of authorizations: Global, Grant, and Revoke. Global Authorizations range over all users and groups and are usually used for setting the base permission for a resource. Grant Authorizations range over users and groups and grant a set of permissions. Revoke Authorizations range over users and groups and revoke a set of permissions.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/authorization/Authorization.java" line="24">

---

# Authorization Interface

The Authorization interface is the main component of the authorization system. It defines methods for managing permissions, such as adding and removing permissions, checking if a permission is granted or revoked, and setting the user or group ID, resource type and ID, and authorization type. It also defines constants for the three types of authorizations: Global, Grant, and Revoke.

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

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/AuthorizationService.java" line="30">

---

# Authorization Usage

The AuthorizationService is used to create, save, and query Authorization objects. It provides methods for creating a new Authorization, saving an Authorization, and creating an AuthorizationQuery to find existing Authorizations.

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

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/authorization/AuthorizationQuery.java" line="25">

---

# Authorization Query

The AuthorizationQuery interface is used to build queries for finding Authorizations. It provides methods for filtering the query by authorization ID, type, user ID, group ID, resource type, and resource ID, as well as checking if a permission is granted.

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
