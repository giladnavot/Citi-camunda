---
title: Diving Deeper into the File Structure of the Resources Component
---
This document will cover the reasons behind the breakdown of resources into individual files in the Citi-camunda repository. We'll cover:

1. The role of the ResourceReport interface
2. The use of the PermissionProvider interface
3. The structure of resource directories.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/ResourceReport.java" line="21">

---

# Role of the ResourceReport Interface

The `ResourceReport` interface is used to create a report during parsing. It provides methods to get the resource name where problems occurred and to get lists of errors and warnings. This allows for individual tracking and reporting of issues for each resource file.

```java
/**
 * This a report created during a parsing.
 */
public interface ResourceReport {

  /** Returns the resource name where the problems occurred. */
  String getResourceName();

  /** Returns list of errors in this report */
  List<Problem> getErrors();

  /** Returns list of warnings in this report */
  List<Problem> getWarnings();
}
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/cfg/auth/PermissionProvider.java" line="22">

---

# Use of the PermissionProvider Interface

The `PermissionProvider` interface is used to determine custom permissions and resources. It provides methods to get the permission related to the name and resource type, get all permissions possible for the resource type, and get the name of the resource with the resource type. This allows for granular control of permissions on individual resource files.

```java
/**
 * A simple provider used to determine custom {@link Permission}s and
 * {@link Resource}s
 * 
 * @author Yana.Vasileva
 * @author Tobias Metzke
 *
 */
public interface PermissionProvider {

  /**
   * Gets the permission related to the name and resource type
   * 
   */
  Permission getPermissionForName(String name, int resourceType);

  /**
   * Gets all permissions possible for the resource type
   */
  Permission[] getPermissionsForResource(int resourceType);

```

---

</SwmSnippet>

# Structure of Resource Directories

The resources in the Citi-camunda repository are organized into individual files within various directories. This structure allows for better organization and management of resources. It also makes it easier to locate and work with specific resources.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="follow-up"><sup>Powered by [Swimm](/)</sup></SwmMeta>
