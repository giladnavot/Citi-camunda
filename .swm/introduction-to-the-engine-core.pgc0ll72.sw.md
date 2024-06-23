---
title: Introduction to the Engine Core
---
The Engine Core in Camunda Platform 7 is the heart of the process automation system. It is responsible for executing processes defined in BPMN 2.0. The Engine Core is implemented in Java and can be embedded in any Java application or runtime container. It includes components for process implementation and execution, process design, process operations, and human task management. The Engine Core is highly integrable and embeddable, making it a flexible solution for various automation needs.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/ProcessEngine.java" line="19">

---

# ProcessEngine Class

The ProcessEngine class provides access to all the services that expose the BPM and workflow operations. It includes methods for managing process instances, tasks, users, groups, and admin operations. It is a thread-safe object and is typically stored in a static field or JNDI location.

```java
/**
 * Provides access to all the services that expose the BPM and workflow operations.
 *
 * <ul>
 * <li>
 * <b>{@link org.camunda.bpm.engine.RuntimeService}: </b> Allows the creation of
 * {@link org.camunda.bpm.engine.repository.Deployment}s and the starting of and searching on
 * {@link org.camunda.bpm.engine.runtime.ProcessInstance}s.</li>
 * <li>
 * <b>{@link org.camunda.bpm.engine.TaskService}: </b> Exposes operations to manage human
 * (standalone) {@link org.camunda.bpm.engine.task.Task}s, such as claiming, completing and
 * assigning tasks</li>
 * <li>
 * <b>{@link org.camunda.bpm.engine.IdentityService}: </b> Used for managing
 * {@link org.camunda.bpm.engine.identity.User}s, {@link org.camunda.bpm.engine.identity.Group}s and
 * the relations between them<</li>
 * <li>
 * <b>{@link org.camunda.bpm.engine.ManagementService}: </b> Exposes engine admin and
 * maintenance operations</li>
 *  <li>
 * <b>{@link org.camunda.bpm.engine.HistoryService}: </b> Service exposing information about
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/context/CoreExecutionContext.java" line="22">

---

# CoreExecutionContext Class

The CoreExecutionContext class is an abstract class that represents the context of a process execution. It contains a reference to the execution and provides methods for getting the deployment and the deployment ID.

```java
/**
 * @author Roman Smirnov
 * @author Daniel Meyer
 */
public abstract class CoreExecutionContext<T extends CoreExecution> {

  protected T execution;

  public CoreExecutionContext(T execution) {
    this.execution = execution;
  }

  public T getExecution() {
    return execution;
  }

  protected abstract String getDeploymentId();

  public DeploymentEntity getDeployment() {
    return Context
      .getCommandContext()
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/ProcessEngineConfiguration.java" line="38">

---

# ProcessEngineConfiguration Class

The ProcessEngineConfiguration class provides configuration information from which a process engine can be built. It includes methods for creating a process engine based on the default configuration file, creating a process engine programmatically, and customizing the configuration before building the process engine.

```java
/** Configuration information from which a process engine can be build.
 *
 * <p>Most common is to create a process engine based on the default configuration file:
 * <pre>ProcessEngine processEngine = ProcessEngineConfiguration
 *   .createProcessEngineConfigurationFromResourceDefault()
 *   .buildProcessEngine();
 * </pre>
 * </p>
 *
 * <p>To create a process engine programatic, without a configuration file,
 * the first option is {@link #createStandaloneProcessEngineConfiguration()}
 * <pre>ProcessEngine processEngine = ProcessEngineConfiguration
 *   .createStandaloneProcessEngineConfiguration()
 *   .buildProcessEngine();
 * </pre>
 * This creates a new process engine with all the defaults to connect to
 * a remote h2 database (jdbc:h2:tcp://localhost/activiti) in standalone
 * mode.  Standalone mode means that Activiti will manage the transactions
 * on the JDBC connections that it creates.  One transaction per
 * service method.
 * For a description of how to write the configuration files, see the
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
