---
title: Overview of the Repository Package
---
In the Citi-camunda repository, 'Repository' refers to a package within the codebase. It is located under the path 'org.camunda.bpm.engine.repository'. This package contains various Java classes and interfaces that are integral to the functioning of the Camunda BPM engine. These classes and interfaces define and manage different aspects of the process automation workflow, such as process definitions, deployments, decision definitions, and more.

The 'RepositoryService' is a part of the 'Repository' package. It is an interface that provides methods for managing deployments and process definitions. It is used throughout the codebase to interact with the repository.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/DeploymentQuery.java" line="39">

---

# DeploymentQuery Interface

The `DeploymentQuery` interface provides methods for querying deployments. It includes methods like `deploymentId(String deploymentId)` to select deployments with a given id, `deploymentBefore(Date before)` to select deployments deployed before a given date, and `orderByDeploymentId()` to order the results by deployment id.

```java
public interface DeploymentQuery extends Query<DeploymentQuery, Deployment>{

  /** Only select deployments with the given deployment id. */
  DeploymentQuery deploymentId(String deploymentId);

  /** Only select deployments with the given name. */
  DeploymentQuery deploymentName(String name);

  /** Only select deployments with a name like the given string. */
  DeploymentQuery deploymentNameLike(String nameLike);

  /**
   * If the given <code>source</code> is <code>null</code>,
   * then deployments are returned where source is equal to null.
   * Otherwise only deployments with the given source are
   * selected.
   */
  DeploymentQuery deploymentSource(String source);

  /** Only select deployments deployed before the given date */
  DeploymentQuery deploymentBefore(Date before);
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/ResourceDefinition.java" line="24">

---

# ResourceDefinition Interface

The `ResourceDefinition` interface provides methods for defining resources. It includes methods like `getId()` to get the unique identifier of a resource, `getName()` to get the label used for display purposes, and `getDeploymentId()` to get the deployment in which this definition is contained.

```java
public interface ResourceDefinition {

  /** unique identifier */
  String getId();

  /** category name which is derived from the targetNamespace attribute in the definitions element */
  String getCategory();

  /** label used for display purposes */
  String getName();

  /** unique name for all versions this definition */
  String getKey();

  /** version of this definition */
  int getVersion();

  /** name of {@link RepositoryService#getResourceAsStream(String, String) the resource} of this definition */
  String getResourceName();

  /** The deployment in which this definition is contained. */
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
