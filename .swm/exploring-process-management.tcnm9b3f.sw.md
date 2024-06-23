---
title: Exploring Process Management
---
Process Management in the Citi-camunda repository is primarily handled through the `ProcessInstance` interface and the `ProcessInstanceQuery` interface. The `ProcessInstance` interface represents one execution of a `ProcessDefinition` and provides methods to retrieve information about the process instance, such as the process definition id, business key, root process instance id, and case instance id. It is used extensively throughout the codebase to manage and manipulate process instances. The `ProcessInstanceQuery` interface allows for programmatic querying of `ProcessInstance`s, providing a range of methods to filter and sort process instances based on various criteria such as process definition key, process instance id, and business key. It is used to retrieve specific process instances for further operations.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/runtime/ProcessInstanceQuery.java" line="33">

---

# ProcessInstanceQuery Interface

The ProcessInstanceQuery interface provides methods for querying process instances. It allows for the selection of process instances based on various parameters such as process instance ID, business key, process definition key, etc. It also provides methods for ordering the results of the query.

```java
public interface ProcessInstanceQuery extends Query<ProcessInstanceQuery, ProcessInstance> {

  /**
   * Select the process instance with the given id
   */
  ProcessInstanceQuery processInstanceId(String processInstanceId);

  /**
   * Select process instances whose id is in the given set of ids
   */
  ProcessInstanceQuery processInstanceIds(Set<String> processInstanceIds);

  /**
   * Select process instances with the given business key
   */
  ProcessInstanceQuery processInstanceBusinessKey(String processInstanceBusinessKey);

  /**
   * Select process instance with the given business key, unique for the given process definition
   */
  ProcessInstanceQuery processInstanceBusinessKey(String processInstanceBusinessKey, String processDefinitionKey);
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/runtime/ProcessInstance.java" line="28">

---

# ProcessInstance Interface

The ProcessInstance interface represents one execution of a process definition. It provides methods to get information about the process instance such as the process definition ID, business key, root process instance ID, etc. It also provides a method to check if the process instance is suspended.

```java
public interface ProcessInstance extends Execution {

  /**
   * The id of the process definition of the process instance.
   */
  String getProcessDefinitionId();

  /**
   * The business key of this process instance.
   */
  String getBusinessKey();

  /**
   * The id of the root process instance associated with this process instance.
   */
  String getRootProcessInstanceId();

  /**
   * The id of the case instance associated with this process instance.
   */
  String getCaseInstanceId();
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/ProcessInstanceQueryImpl.java" line="47">

---

# Usage of ProcessInstanceQuery and ProcessInstance

Here is an example of how the ProcessInstanceQuery interface is used in the codebase. An instance of ProcessInstanceQueryImpl is created and the methods of the interface are used to set the parameters for the query. The query is then executed to return a list of ProcessInstances that match the query parameters.

```java
public class ProcessInstanceQueryImpl extends AbstractVariableQueryImpl<ProcessInstanceQuery, ProcessInstance> implements ProcessInstanceQuery, Serializable {

  private static final long serialVersionUID = 1L;
  protected String processInstanceId;
  protected String businessKey;
  protected String businessKeyLike;
  protected String processDefinitionId;
  protected Set<String> processInstanceIds;
  protected String processDefinitionKey;
  protected String[] processDefinitionKeys;
  protected String[] processDefinitionKeyNotIn;
  protected String deploymentId;
  protected String superProcessInstanceId;
  protected String subProcessInstanceId;
  protected SuspensionState suspensionState;
  protected boolean withIncident;
  protected String incidentType;
  protected String incidentId;
  protected String incidentMessage;
  protected String incidentMessageLike;
  protected String caseInstanceId;
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
