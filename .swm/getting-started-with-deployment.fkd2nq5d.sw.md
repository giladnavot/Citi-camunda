---
title: Getting Started with Deployment
---
In the context of the Citi-camunda repository, a 'Deployment' represents a container for resources such as process definitions, images, forms, etc. When a deployment is 'deployed' through the RepositoryService, the engine will recognize certain resource types and act upon them. For example, process definitions will be parsed to an executable Java artifact. The Deployment interface provides methods to retrieve information about the deployment, such as its ID, name, deployment time, source, and tenant ID.

The DeploymentHandler interface defines custom behavior for determining what resources should be added to a new deployment. It provides methods to determine if a new resource should be deployed, to find a duplicate deployment, and to determine deployments to resume based on process definition keys or deployment name.

The DeploymentBuilder interface provides methods to add resources to a deployment, set the deployment name, and enable duplicate filtering. It also provides methods to add resources from an existing deployment or by resource name or ID. The deploy() method is used to deploy all provided resources to the process engine.

The ProcessApplicationDeployment interface extends the DeploymentWithDefinitions interface and represents a deployment that is associated with a process application. It provides a method to get the ProcessApplicationRegistration performed for this process application deployment.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/Deployment.java" line="21">

---

# Deployment Interface

This is the interface for Deployment. It provides methods to get information about the deployment such as its id, name, deployment time, source, and tenant id.

```java
/**
 * Represents a deployment that is already present in the process repository.
 *
 * A deployment is a container for resources such as process definitions, images, forms, etc.
 *
 * When a deployment is 'deployed' through the {@link org.camunda.bpm.engine.RepositoryService},
 * the engine will recognize certain of such resource types and act upon
 * them (e.g. process definitions will be parsed to an executable Java artifact).
 *
 * To create a Deployment, use the {@link org.camunda.bpm.engine.repository.DeploymentBuilder}.
 * A Deployment on itself is a <b>read-only</b> object and its content cannot be
 * changed after deployment (hence the builder that needs to be used).
 *
 * @author Tom Baeyens
 * @author Joram Barrez
 */
public interface Deployment {

  String getId();

  String getName();
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/DeploymentHandler.java" line="21">

---

# DeploymentHandler Interface

The DeploymentHandler interface should be implemented when there is a need to define a custom behavior for determining what Resources should be added to a new Deployment. It provides methods to determine if there is a difference between a new resource and an existing one, to determine a duplicate deployment, and to determine deployments to resume by deployment name or process definition key.

```java
/**
 * <p>The {@link DeploymentHandler} interface should be implemented when there is a need to
 * define a custom behavior for determining what Resources should be added to a new Deployment.</p>
 *
 * <p>The class that implements this interface must provide a Process Engine parameter in it's
 * constructor. Custom implementations of this interface should be coupled with an implementation
 * of the {@link DeploymentHandlerFactory} interface, which can then be wired to the Process Engine
 * through the
 * {@link org.camunda.bpm.engine.impl.cfg.ProcessEngineConfigurationImpl#setDeploymentHandlerFactory(DeploymentHandlerFactory)}
 * method.</p>
 *
 * <p>See {@link org.camunda.bpm.engine.impl.repository.DefaultDeploymentHandler} for the default
 * behavior of the deployment process.</p>
 */
public interface DeploymentHandler {

  /**
   * <p>This method is called in the first stage of the deployment process. It determines if there
   * is a difference between a {@link Resource} that is included in the set of resources provided
   * for deployment, and a Resource of the same name, already deployed to the Process Engine
   * with a previous Deployment. The method will be called for every (new, existing) Resource
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/DeploymentBuilder.java" line="202">

---

# DeploymentBuilder Interface

The DeploymentBuilder interface is used to create a Deployment. It provides a deploy method to perform the deployment.

```java
   *
   * <p> The returned {@link Deployment} instance has no information about the definitions, which are deployed
   * with that deployment. To access this information you can use the {@link #deployWithResult()} method.
   * This method will return an instance of {@link DeploymentWithDefinitions}, which contains the information
   * about the successful deployed definitions.
   * </p>
   *
   * @throws NotFoundException thrown
   *  <ul>
   *    <li>if the deployment specified by {@link #nameFromDeployment(String)} does not exist or</li>
   *    <li>if at least one of given deployments provided by {@link #addDeploymentResources(String)} does not exist.</li>
   *  </ul>
   *
   * @throws NotValidException
   *    if there are duplicate resource names from different deployments to re-deploy.
   *
   * @throws ParseException
   *    In case of a BPMN Parsing exception due to null historyTimeToLive. To disable this behaviour, configure the
   *    feature flag {@code enforceHistoryTimeToLive} to {@code false}.
   *
   * @throws AuthorizationException
```

---

</SwmSnippet>

# Deployment Functions

This section covers the main functions related to deployments in the Citi-camunda repository.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/DeploymentBuilder.java" line="34">

---

## DeploymentBuilder Interface

The DeploymentBuilder interface is used to create new deployments. It provides methods for adding resources to the deployment, setting the deployment source, and deploying the resources. The resources can be added as input streams, classpath resources, strings, or model instances. The deploy method is used to deploy all provided sources to the process engine and returns the created deployment.

```java
/**
 * <p>Builder for creating new deployments.</p>
 *
 * <p>A builder instance can be obtained through {@link org.camunda.bpm.engine.RepositoryService#createDeployment()}.</p>
 *
 * <p>Multiple resources can be added to one deployment before calling the {@link #deploy()}
 * operation.</p>
 *
 * <p>After deploying, no more changes can be made to the returned deployment
 * and the builder instance can be disposed.</p>
 *
 * <p>In order the resources to be processed as definitions, their names must have one of allowed suffixes (file extensions in case of file reference).</p>
 * <table>
 * <thead>
 *   <tr><th>Resource name suffix</th><th>Will be treated as</th></tr>
 * <thead>
 * <tbody>
 *    <tr>
 *      <td>.bpmn20.xml, .bpmn</td><td>BPMN process definition</td>
 *    </tr>
 *    <tr>
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/DeploymentQuery.java" line="24">

---

## DeploymentQuery Interface

The DeploymentQuery interface allows for programmatic querying of deployments. It provides methods for selecting deployments based on various criteria such as deployment id, deployment name, and deployment time. It also provides methods for ordering the results based on deployment id, name, or time.

```java
/**
 * Allows programmatic querying of {@link Deployment}s.
 *
 * Note that it is impossible to retrieve the deployment resources through the
 * results of this operation, since that would cause a huge transfer of
 * (possibly) unneeded bytes over the wire.
 *
 * To retrieve the actual bytes of a deployment resource use the operations on the
 * {@link RepositoryService#getDeploymentResourceNames(String)}
 * and {@link RepositoryService#getResourceAsStream(String, String)}
 *
 * @author Tom Baeyens
 * @author Joram Barrez
 * @author Ingo Richtsmeier
 */
public interface DeploymentQuery extends Query<DeploymentQuery, Deployment>{

  /** Only select deployments with the given deployment id. */
  DeploymentQuery deploymentId(String deploymentId);

  /** Only select deployments with the given name. */
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/DeploymentHandler.java" line="21">

---

## DeploymentHandler Interface

The DeploymentHandler interface should be implemented when there is a need to define a custom behavior for determining what resources should be added to a new deployment. It provides methods for determining if a resource should be deployed, determining a duplicate deployment, and determining deployments to resume.

```java
/**
 * <p>The {@link DeploymentHandler} interface should be implemented when there is a need to
 * define a custom behavior for determining what Resources should be added to a new Deployment.</p>
 *
 * <p>The class that implements this interface must provide a Process Engine parameter in it's
 * constructor. Custom implementations of this interface should be coupled with an implementation
 * of the {@link DeploymentHandlerFactory} interface, which can then be wired to the Process Engine
 * through the
 * {@link org.camunda.bpm.engine.impl.cfg.ProcessEngineConfigurationImpl#setDeploymentHandlerFactory(DeploymentHandlerFactory)}
 * method.</p>
 *
 * <p>See {@link org.camunda.bpm.engine.impl.repository.DefaultDeploymentHandler} for the default
 * behavior of the deployment process.</p>
 */
public interface DeploymentHandler {

  /**
   * <p>This method is called in the first stage of the deployment process. It determines if there
   * is a difference between a {@link Resource} that is included in the set of resources provided
   * for deployment, and a Resource of the same name, already deployed to the Process Engine
   * with a previous Deployment. The method will be called for every (new, existing) Resource
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
