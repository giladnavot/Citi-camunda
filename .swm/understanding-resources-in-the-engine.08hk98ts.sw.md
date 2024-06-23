---
title: Understanding Resources in the Engine
---
In the context of the Citi-camunda repository, 'Resources' in the engine refers to the entities that a user or a group is authorized to interact with. Examples of resources are applications, process definitions, process instances, tasks, etc. Each resource has a type and an id. The type allows grouping all resources of the same kind, while the id is the identifier of an individual resource instance. The 'Resources' enum in the codebase provides a set of built-in resource constants.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/authorization/Resource.java" line="35">

---

# Resource Interface

The `Resource` interface defines the methods that every resource must implement. These include `resourceName()` which returns the name of the resource, and `resourceType()` which returns an integer representing the type of the resource.

```java
public interface Resource {
  
  /** returns the name of the resource */
  String resourceName();
  
  /** an integer representing the type of the resource.
   * @return the type identitfyer of the resource */
  int resourceType();

}
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/authorization/Resources.java" line="27">

---

# Resources Enum

The `Resources` enum lists all the built-in resource names. Each enum value represents a different type of resource, such as APPLICATION, USER, GROUP, etc. Each resource has a name and an id.

```java
public enum Resources implements Resource {

  APPLICATION(EntityTypes.APPLICATION, 0),
  USER(EntityTypes.USER, 1),
  GROUP(EntityTypes.GROUP, 2),
  GROUP_MEMBERSHIP(EntityTypes.GROUP_MEMBERSHIP, 3),
  AUTHORIZATION(EntityTypes.AUTHORIZATION, 4),
  FILTER(EntityTypes.FILTER, 5),
  PROCESS_DEFINITION(EntityTypes.PROCESS_DEFINITION, 6),
  TASK(EntityTypes.TASK, 7),
  PROCESS_INSTANCE(EntityTypes.PROCESS_INSTANCE, 8),
  DEPLOYMENT(EntityTypes.DEPLOYMENT, 9),
  DECISION_DEFINITION(EntityTypes.DECISION_DEFINITION, 10),
  TENANT(EntityTypes.TENANT, 11),
  TENANT_MEMBERSHIP(EntityTypes.TENANT_MEMBERSHIP, 12),
  BATCH(EntityTypes.BATCH, 13),
  DECISION_REQUIREMENTS_DEFINITION(EntityTypes.DECISION_REQUIREMENTS_DEFINITION, 14),
  REPORT(EntityTypes.REPORT, 15),
  DASHBOARD(EntityTypes.DASHBOARD, 16),
  OPERATION_LOG_CATEGORY(EntityTypes.OPERATION_LOG_CATEGORY, 17),
  @Deprecated
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/authorization/Authorization.java" line="207">

---

# Authorization Interface

The `Authorization` interface has methods `setResourceType(int resourceTypeId)` and `setResource(Resource resource)` to set the type of the resource. These methods are used when creating an Authorization to specify the resource it applies to.

```java
  /**
   * sets the type of the resource
   */
  public void setResourceType(int resourceTypeId);

  /**
   * sets the type of the resource
   */
  public void setResource(Resource resource);
```

---

</SwmSnippet>

# Resource Functions

This section will cover the 'resourceName' and 'resourceType' functions in the 'Resources' of the 'engine'.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/authorization/Resources.java" line="61">

---

## resourceName Function

The 'resourceName' function returns the name of the resource. It is used in various places in the codebase to get the name of the resource for a particular operation.

```java
  public String resourceName() {
    return name;
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/authorization/Resources.java" line="65">

---

## resourceType Function

The 'resourceType' function returns the id of the resource. It is used in various places in the codebase to get the id of the resource for a particular operation.

```java
  public int resourceType() {
    return id;
  }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
