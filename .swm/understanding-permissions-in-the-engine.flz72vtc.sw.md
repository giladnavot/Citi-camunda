---
title: Understanding Permissions in the Engine
---
Permissions in the engine are a set of built-in authorizations for different operations in the Camunda Platform. They are represented as an enumeration of different permission types, each associated with a specific action or interaction. For example, the `READ` permission indicates that read interactions are permitted, while the `UPDATE` permission allows update interactions. Permissions are used throughout the codebase to manage and control access to resources and operations. They are integral to the security and access control mechanisms of the Camunda Platform.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/authorization/Permissions.java" line="21">

---

# Permissions

The `Permissions` enum defines the set of built-in permissions for the Camunda Platform. Each permission indicates a specific type of interaction that is permitted, such as READ, UPDATE, CREATE, DELETE, etc. Each permission has a name, an id, and a set of resource types it applies to.

```java
/**
 * The set of built-in {@link Permission Permissions} for Camunda Platform.
 *
 * @author Daniel Meyer
 *
 */
public enum Permissions implements Permission {

  /** The none permission means 'no action', 'doing nothing'.
   * It does not mean that no permissions are granted. */
  NONE("NONE", 0, EnumSet.allOf(Resources.class)),

  /**
   * Indicates that  all interactions are permitted.
   * If ALL is revoked it means that the user is not permitted
   * to do everything, which means that at least one permission
   * is revoked. This does not implicate that all individual
   * permissions are revoked.
   *
   * Example: If the UPDATE permission is revoked then the ALL
   * permission is revoked as well, because the user is not authorized
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/authorization/Authorization.java" line="24">

---

# Authorization

The `Authorization` interface assigns a set of permissions to an identity for a given resource. It provides methods to add and remove permissions, and to check if a specific permission is granted. The type of the authorization (global, grant, or revoke) affects how the permissions are interpreted.

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

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/authorization/Authorization.java" line="191">

---

# Setting Permissions

The `setPermissions` method in the `Authorization` interface is used to set the permissions for an authorization. It replaces all existing permissions with the provided ones. The effect of this method depends on the type of the authorization.

```java
  public void setPermissions(Permission[] permissions);
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/authorization/Authorization.java" line="137">

---

# Checking Permissions

The `isPermissionGranted` method in the `Authorization` interface is used to check if a specific permission is granted for the authorization. It throws an `IllegalStateException` if the authorization is of type `AUTH_TYPE_REVOKE`.

```java
  public boolean isPermissionGranted(Permission permission);
```

---

</SwmSnippet>

# Permissions and Authorization

This section will cover the Permissions enum and the methods in the Authorization class, which are key components of the permissions functionality in the Citi-camunda repository.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/authorization/Permissions.java" line="27">

---

## Permissions Enum

The Permissions enum defines the set of built-in permissions for the Camunda Platform. Each enum constant represents a specific permission, such as NONE, ALL, READ, UPDATE, CREATE, DELETE, etc. Each permission is associated with a name and an integer value. The permissions are used to control the interactions with various resources in the system.

```java
public enum Permissions implements Permission {

  /** The none permission means 'no action', 'doing nothing'.
   * It does not mean that no permissions are granted. */
  NONE("NONE", 0, EnumSet.allOf(Resources.class)),

  /**
   * Indicates that  all interactions are permitted.
   * If ALL is revoked it means that the user is not permitted
   * to do everything, which means that at least one permission
   * is revoked. This does not implicate that all individual
   * permissions are revoked.
   *
   * Example: If the UPDATE permission is revoked then the ALL
   * permission is revoked as well, because the user is not authorized
   * to execute all actions anymore.
   */
  ALL("ALL", Integer.MAX_VALUE, EnumSet.allOf(Resources.class)),

  /** Indicates that READ interactions are permitted. */
  READ("READ", 2,
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/authorization/Authorization.java" line="125">

---

## Authorization Methods

The Authorization class provides methods to manage permissions for a given resource. The 'addPermission' method allows granting a permission, the 'removePermission' method revokes a permission, the 'isPermissionGranted' method checks if a specific permission is granted, and the 'getPermissions' and 'setPermissions' methods allow getting and setting the permissions respectively.

```java
  public void addPermission(Permission permission);

  /** allows removing a permission. Out-of-the-box constants can be found in {@link Permissions}.
   * */
  public void removePermission(Permission permission);

  /**
   * Allows checking whether this authorization grants a specific permission.
   *
   * @param perm the permission to check for
   * @throws IllegalStateException if this {@link Authorization} is of type {@link #AUTH_TYPE_REVOKE}
   */
  public boolean isPermissionGranted(Permission permission);

  /**
   * Allows checking whether this authorization revokes a specific permission.
   *
   * @param perm the permission to check for
   * @throws IllegalStateException if this {@link Authorization} is of type {@link #AUTH_TYPE_GRANT}
   */
  public boolean isPermissionRevoked(Permission permission);
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
