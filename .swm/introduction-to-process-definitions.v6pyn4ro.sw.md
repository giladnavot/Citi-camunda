---
title: Introduction to Process Definitions
---
A Process Definition in Camunda is an object structure representing an executable process composed of activities and transitions. It is created from process definition files (usually BPMN 2.0 XML files) that are added to a deployment artifact. At deploy time, the engine parses these files into an executable instance of a Process Definition. This instance can then be used to start a Process Instance. A Process Definition includes information such as the process id, key, name, version, and deployment id. It also provides methods to query and interact with deployed processes.

The Process Definition interface extends the ResourceDefinition interface, inheriting its methods. It also provides additional methods specific to process definitions. For example, the `getDescription` method returns the description of the process, `getVersionTag` returns the version tag of the process definition, and `isStartableInTasklist` returns a boolean indicating whether the process definition is startable in the Tasklist.

The ProcessDefinitionQuery interface allows programmatic querying of Process Definitions. It provides methods to filter and sort process definitions based on various properties such as process definition id, key, name, and version. For example, the `processDefinitionName` method only selects process definitions with the given name, and the `orderByProcessDefinitionName` method orders the query results by the name of the process definitions.

The CalledProcessDefinition interface extends the ProcessDefinition interface. It represents a process definition that is called by a call activity in another process. It provides additional methods to get the id of the calling process definition and the ids of the activities from which the process is called.

The DeploymentHandler interface defines custom behavior for determining what resources should be added to a new deployment. It provides methods to determine if a resource should be deployed, to find a duplicate deployment, and to determine deployments to resume by process definition key.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/ProcessDefinition.java" line="22">

---

# ProcessDefinition Interface

This is the definition of the ProcessDefinition interface. It extends the ResourceDefinition interface and provides several methods to get information about the process definition, such as its description, start form key, suspension state, version tag, and whether it is startable in the tasklist.

```java
/** An object structure representing an executable process composed of
 * activities and transitions.
 *
 * Business processes are often created with graphical editors that store the
 * process definition in certain file format. These files can be added to a
 * {@link Deployment} artifact, such as for example a Business Archive (.bar)
 * file.
 *
 * At deploy time, the engine will then parse the process definition files to an
 * executable instance of this class, that can be used to start a {@link ProcessInstance}.
 *
 * @author Tom Baeyens
 * @author Joram Barez
 * @author Daniel Meyer
 */
public interface ProcessDefinition extends ResourceDefinition {

  /** description of this process **/
  String getDescription();

  /** Does this process definition has a {@link FormService#getStartFormData(String) start form key}. */
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/cmd/DeployCmd.java" line="65">

---

# Usage of ProcessDefinition

Here, the ProcessDefinition interface is used in the DeployCmd class. This class is responsible for deploying process definitions to the Camunda platform.

```java
import org.camunda.bpm.engine.repository.ProcessDefinition;
import org.camunda.bpm.engine.repository.Resource;
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/ProcessDefinitionQueryImpl.java" line="37">

---

# Querying ProcessDefinitions

The ProcessDefinitionQuery interface provides a way to programmatically query for ProcessDefinitions. This is an example of its usage in the ProcessDefinitionQueryImpl class.

```java
import org.camunda.bpm.engine.impl.util.CompareUtil;
import org.camunda.bpm.engine.repository.ProcessDefinition;
import org.camunda.bpm.engine.repository.ProcessDefinitionQuery;
import org.camunda.bpm.model.bpmn.BpmnModelInstance;
import org.camunda.bpm.model.bpmn.instance.Documentation;
import org.camunda.bpm.model.xml.instance.ModelElementInstance;
import static org.camunda.bpm.engine.impl.util.EnsureUtil.ensureNotNull;
import static org.camunda.bpm.engine.impl.util.EnsureUtil.ensurePositive;


/**
 * @author Tom Baeyens
 * @author Joram Barrez
 * @author Daniel Meyer
 * @author Saeid Mirzaei
 */
public class ProcessDefinitionQueryImpl extends AbstractQuery<ProcessDefinitionQuery, ProcessDefinition>
  implements ProcessDefinitionQuery {
```

---

</SwmSnippet>

# ProcessDefinition Functions

This section covers the main functions of the ProcessDefinition interface and its implementations.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/ProcessDefinitionQuery.java" line="36">

---

## ProcessDefinitionId

The `processDefinitionId` function is used to select a process definition with a specific id.

```java
  ProcessDefinitionQuery processDefinitionId(String processDefinitionId);
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/ProcessDefinitionQuery.java" line="78">

---

## ProcessDefinitionKey

The `processDefinitionKey` function is used to select a process definition with a specific key.

```java
  ProcessDefinitionQuery processDefinitionKey(String processDefinitionKey);
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/ProcessDefinitionQuery.java" line="42">

---

## ProcessDefinitionCategory

The `processDefinitionCategory` function is used to select process definitions with a specific category.

```java
  ProcessDefinitionQuery processDefinitionCategory(String processDefinitionCategory);
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/ProcessDefinitionQuery.java" line="51">

---

## ProcessDefinitionName

The `processDefinitionName` function is used to select process definitions with a specific name.

```java
  ProcessDefinitionQuery processDefinitionName(String processDefinitionName);
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/ProcessDefinitionQuery.java" line="63">

---

## DeploymentId

The `deploymentId` function is used to select process definitions that are deployed in a deployment with the given deployment id.

```java
  ProcessDefinitionQuery deploymentId(String deploymentId);
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/ProcessDefinitionQuery.java" line="104">

---

## ProcessDefinitionVersion

The `processDefinitionVersion` function is used to select a process definition with a certain version.

```java
  ProcessDefinitionQuery processDefinitionVersion(Integer processDefinitionVersion);
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/ProcessDefinitionQuery.java" line="131">

---

## ProcessDefinitionResourceName

The `processDefinitionResourceName` function is used to select a process definition with a specific resource name.

```java
  ProcessDefinitionQuery processDefinitionResourceName(String resourceName);
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/ProcessDefinitionQuery.java" line="149">

---

## Active

The `active` function is used to select process definitions which are active.

```java
  ProcessDefinitionQuery active();
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/ProcessDefinitionQuery.java" line="215">

---

## StartableInTasklist

The `startableInTasklist` function is used to select process definitions which could be started in Tasklist.

```java
  ProcessDefinitionQuery startableInTasklist();
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
