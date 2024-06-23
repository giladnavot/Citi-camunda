---
title: Getting Started with Resource Interfaces
---
In the Citi-camunda repository, a 'Resource' refers to an interface that represents a deployable resource in the Camunda BPM platform. It provides methods to get the ID, name, deployment ID, and bytes of the resource. This interface is used in various parts of the codebase, such as in the DeploymentHandler and DeploymentBuilder classes.

The 'ResourceDefinition' interface represents a definition of a deployed resource. It provides methods to get the ID, category, name, key, version, resource name, deployment ID, diagram resource name, tenant ID, and history time to live of the resource definition. This interface is used in various parts of the codebase, such as in the ModelInstanceCache and ResourceDefinitionEntity classes.

The 'ResourceType' interface represents a type of resource. It provides methods to get the name and value of the resource type. This interface is used in various parts of the codebase, such as in the ByteArrayEntity and ByteArrayField classes.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/Resource.java" line="22">

---

# Resource Interface

This is the 'Resource' interface. It provides methods to retrieve the ID, name, and deployment ID of the resource, as well as the actual content of the resource in the form of a byte array.

```java
public interface Resource {


  String getId();

  String getName();

  String getDeploymentId();

  byte[] getBytes();

}
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/DeploymentHandler.java" line="38">

---

# Usage of Resource Interface

Here, the 'Resource' interface is used in the 'DeploymentHandler' class. It is used to determine if there is a difference between a resource that is included in the set of resources provided for deployment, and a resource of the same name, already deployed to the Process Engine with a previous Deployment.

```java
   * <p>This method is called in the first stage of the deployment process. It determines if there
   * is a difference between a {@link Resource} that is included in the set of resources provided
   * for deployment, and a Resource of the same name, already deployed to the Process Engine
   * with a previous Deployment. The method will be called for every (new, existing) Resource
   * pair. If a Resource of the same name doesn't exist in the Process Engine database, the new
   * Resource is deployed by default and this method is not called.</p>
   *
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/ResourceDefinition.java" line="24">

---

# ResourceDefinition Interface

The 'ResourceDefinition' interface extends the 'Resource' interface and provides additional methods to retrieve more detailed information about a resource, such as its version, category, key, and tenant ID. It also provides methods to retrieve the name of the resource and the name of the diagram resource, if it exists.

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

# Resource Functions

This section will cover the functions related to resources in the Citi-camunda repository.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/ResourceDefinition.java" line="21">

---

## ResourceDefinition Interface

The ResourceDefinition interface defines the basic properties of a resource. These include the ID, category, name, key, version, resource name, deployment ID, diagram resource name, tenant ID, and history time to live. Each of these properties has a corresponding getter method.

```java
/**
 * Definition of a resource which was deployed
 */
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
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/Resource.java" line="19">

---

## Resource Interface

The Resource interface defines the basic behaviors of a resource. These include getting the ID, name, deployment ID, and bytes of the resource. Each of these behaviors has a corresponding method.

```java
/**
 * @author kristin.polenz@camunda.com
 */
public interface Resource {


  String getId();

  String getName();

  String getDeploymentId();

  byte[] getBytes();

}
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
