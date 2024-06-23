---
title: Caching Mechanisms for Optimizing Permission Checks
---
This document will cover the caching mechanisms in place to optimize permission checks in the Citi-camunda repository. We'll cover:

1. The OptimizePermissions enum
2. The PermissionCheck class
3. The JobExecutorContext class
4. The SpinFunctions class

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/authorization/OptimizePermissions.java" line="19">

---

# OptimizePermissions Enum

The `OptimizePermissions` enum defines the set of permissions for the Optimize resource in Camunda Platform. It includes NONE, ALL, EDIT, and SHARE permissions. Each permission has a name and an id. The `getTypes` method returns the resources associated with these permissions.

```java
/**
 * The set of built-in {@link Permission Permissions} for
 * {@link Resources#OPTIMIZE Optimize resource} in Camunda Platform.
 *
 * @deprecated These permissions have no effect
 */
@Deprecated
public enum OptimizePermissions implements Permission {

  /**
   * The none permission means 'no action', 'doing nothing'. It does not mean
   * that no permissions are granted.
   */
  NONE("NONE", 0),

  /**
   * Indicates that all interactions are permitted. If ALL is revoked it means
   * that the user is not permitted to do everything, which means that at least
   * one permission is revoked. This does not implicate that all individual
   * permissions are revoked.
   * 
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/db/PermissionCheck.java" line="23">

---

# PermissionCheck Class

The `PermissionCheck` class is used to check permissions for a specific resource. It contains the permission to check for, the type of the resource, and the id of the resource. It also provides methods to set and get these properties.

```java
/**
 * @author Roman Smirnov
 *
 */
public class PermissionCheck {

  /** the permission to check for */
  protected Permission permission;
  protected int perms;

  /** the type of the resource to check permissions for */
  protected Resource resource;
  protected int resourceType;

  /** the id of the resource to check permission for */
  protected String resourceId;

  /** query parameter for resource Id. Is injected as RAW parameter into the query */
  protected String resourceIdQueryParam;

  protected Long authorizationNotFoundReturnValue = null;
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/jobexecutor/JobExecutorContext.java" line="24">

---

# JobExecutorContext Class

The `JobExecutorContext` class contains a list of current processor job queue and a current job. It also has a `DbEntityCache` for caching entities. The `getEntityCache` method is used to retrieve the cache.

```java
/**
 * @author Daniel Meyer
 */
public class JobExecutorContext {

  protected List<String> currentProcessorJobQueue = new LinkedList<String>();

  /** the currently executed job */
  protected JobEntity currentJob;

  /** reusable cache */
  protected DbEntityCache entityCache;

  public List<String> getCurrentProcessorJobQueue() {
    return currentProcessorJobQueue;
  }

  public boolean isExecutingExclusiveJob() {
    return currentJob == null ? false : currentJob.isExclusive();
  }

```

---

</SwmSnippet>

<SwmSnippet path="/engine-plugins/spin-plugin/src/main/java/org/camunda/spin/plugin/impl/SpinFunctions.java" line="19">

---

# SpinFunctions Class

The `SpinFunctions` class provides functions for Expression Language. It supports lazy loading and caching of Java Methods. It defines constants S, XML, and JSON.

```java
/**
 * A FunctionMapper which resolves the Spin functions for Expression Language.
 *
 * <p>Lazy loading: This implementation supports lazy loading: the Java Methods
 * are loaded upon the first request.</p>
 *
 * <p>Caching: once the methods are loaded, they are cached in a Map for efficient
 * retrieval.</p>
 *
 * @author Daniel Meyer
 *
 */
public class SpinFunctions {
  public static final String S = "S";
  public static final String XML = "XML";
  public static final String JSON = "JSON";
}
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="follow-up"><sup>Powered by [Swimm](/)</sup></SwmMeta>
