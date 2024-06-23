---
title: Understanding the History Concept
---
In the context of the Citi-camunda repository, 'History' refers to the tracking and storage of past states and activities within the Camunda BPMN process engine. This is achieved through various interfaces and classes that capture and represent historical data. For instance, the `HistoricIncident` interface represents a historic incident that is stored permanently, providing details such as the incident's unique identifier, creation time, end time, and incident message. Similarly, the `CleanableHistoricDecisionInstanceReportResult`, `CleanableHistoricProcessInstanceReportResult`, and `CleanableHistoricCaseInstanceReportResult` interfaces provide historical data related to decision instances, process instances, and case instances respectively. These interfaces include methods to retrieve the history time to live for the selected definition. The `HistoricDetail` interface is a base class for all kinds of information related to a `HistoricProcessInstance` or a `HistoricActivityInstance`. The `HistoricIncidentQuery`, `HistoricDetailQuery` and other similar interfaces allow for programmatic querying of these historic details.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/history/HistoricTaskInstanceQuery.java" line="32">

---

## HistoricTaskInstanceQuery Interface

The 'HistoricTaskInstanceQuery' interface provides methods to query for historic task instances. You can filter the tasks based on task id, process instance id, execution id, process definition id, and many other parameters. You can also sort the results based on various fields.

```java
public interface HistoricTaskInstanceQuery  extends Query<HistoricTaskInstanceQuery, HistoricTaskInstance> {

  /** Only select historic task instances for the given task id. */
  HistoricTaskInstanceQuery taskId(String taskId);

  /** Only select historic task instances for the given process instance. */
  HistoricTaskInstanceQuery processInstanceId(String processInstanceId);

  /** Only select historic task instances for the given root process instance. */
  HistoricTaskInstanceQuery rootProcessInstanceId(String rootProcessInstanceId);

  /** Only select historic tasks for the given process instance business key */
  HistoricTaskInstanceQuery processInstanceBusinessKey(String processInstanceBusinessKey);

  /**
   * Only select historic tasks for any of the given the given process instance business keys.
   */
  HistoricTaskInstanceQuery processInstanceBusinessKeyIn(String... processInstanceBusinessKeys);

  /** Only select historic tasks matching the given process instance business key.
   *  The syntax is that of SQL: for example usage: nameLike(%camunda%)*/
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/history/HistoricIncidentQuery.java" line="27">

---

## HistoricIncidentQuery Interface

The 'HistoricIncidentQuery' interface provides methods to query for historic incidents. You can filter the incidents based on incident id, incident type, process definition id, and many other parameters. You can also sort the results based on various fields.

```java
public interface HistoricIncidentQuery extends Query<HistoricIncidentQuery, HistoricIncident> {

  /** Only select historic incidents which have the given id. **/
  HistoricIncidentQuery incidentId(String incidentId);

  /** Only select historic incidents which have the given incident type. **/
  HistoricIncidentQuery incidentType(String incidentType);

  /** Only select historic incidents which have the given incident message. **/
  HistoricIncidentQuery incidentMessage(String incidentMessage);

  /**
   * Only select historic incidents which incident message is like the given value
   *
   * @param incidentMessageLike The string can include the wildcard character '%' to express
   *    like-strategy: starts with (string%), ends with (%string) or contains (%string%).
   */
  HistoricIncidentQuery incidentMessageLike(String incidentMessageLike);

  /** Only select historic incidents which have the given process definition id. **/
  HistoricIncidentQuery processDefinitionId(String processDefinitionId);
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/history/CleanableHistoricDecisionInstanceReportResult.java" line="23">

---

## CleanableHistoricDecisionInstanceReportResult Interface

The 'CleanableHistoricDecisionInstanceReportResult' interface defines the result of a cleanable historic decision instance report. It provides methods to get details like decision definition id, decision definition key, history time to live, and the count of finished and cleanable decision instances.

```java
public interface CleanableHistoricDecisionInstanceReportResult {

  /**
   * Returns the decision definition id for the selected definition.
   */
  String getDecisionDefinitionId();

  /**
   * Returns the decision definition key for the selected definition.
   */
  String getDecisionDefinitionKey();

  /**
   * Returns the decision definition name for the selected definition.
   */
  String getDecisionDefinitionName();

  /**
   * Returns the decision definition version for the selected definition.
   */
  int getDecisionDefinitionVersion();
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/history/CleanableHistoricProcessInstanceReportResult.java" line="23">

---

## CleanableHistoricProcessInstanceReportResult Interface

The 'CleanableHistoricProcessInstanceReportResult' interface defines the result of a cleanable historic process instance report. It provides methods to get details like process definition id, process definition key, history time to live, and the count of finished and cleanable process instances.

```java
public interface CleanableHistoricProcessInstanceReportResult {

  /**
   * Returns the process definition id for the selected definition.
   */
  String getProcessDefinitionId();

  /**
   * Returns the process definition key for the selected definition.
   */
  String getProcessDefinitionKey();

  /**
   * Returns the process definition name for the selected definition.
   */
  String getProcessDefinitionName();

  /**
   * Returns the process definition version for the selected definition.
   */
  int getProcessDefinitionVersion();
```

---

</SwmSnippet>

# Historic Instance Interfaces

This section covers the methods in the HistoricProcessInstance, HistoricActivityInstance, and HistoricDecisionInstance interfaces.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/history/HistoricProcessInstance.java" line="23">

---

## HistoricProcessInstance Interface

The HistoricProcessInstance interface represents a single execution of a process definition that is stored permanently. It provides methods to get details about the process instance such as the unique identifier, business key, process definition key and id, start time, end time, and duration.

```java
/**
 * A single execution of a whole process definition that is stored permanently.
 *
 * @author Christian Stettler
 * @author Askar Akhmerov
 */
public interface HistoricProcessInstance {

  String STATE_ACTIVE = "ACTIVE";
  String STATE_SUSPENDED = "SUSPENDED";
  String STATE_COMPLETED = "COMPLETED";
  String STATE_EXTERNALLY_TERMINATED = "EXTERNALLY_TERMINATED";
  String STATE_INTERNALLY_TERMINATED = "INTERNALLY_TERMINATED";

  /** The process instance id (== as the id for the runtime {@link ProcessInstance process instance}). */
  String getId();

  /** The user provided unique reference to this process instance. */
  String getBusinessKey();

  /** The process definition key reference. */
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/history/HistoricActivityInstance.java" line="23">

---

## HistoricActivityInstance Interface

The HistoricActivityInstance interface represents one execution of an activity. It provides methods to get details about the activity instance such as the unique identifier, activity id and name, process definition key and id, start time, end time, and task id.

```java
 *
 * @author Christian Stettler
 */
public interface HistoricActivityInstance {

  /** The unique identifier of this historic activity instance. */
  String getId();

  /** return the id of the parent activity instance */
  String getParentActivityInstanceId();

  /** The unique identifier of the activity in the process */
  String getActivityId();

  /** The display name for the activity */
  String getActivityName();

  /**
   * The activity type of the activity.
   * Typically the activity type correspond to the XML tag used in the BPMN 2.0 process definition file.
   *
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/history/HistoricDecisionInstance.java" line="24">

---

## HistoricDecisionInstance Interface

The HistoricDecisionInstance interface represents one evaluation of a decision. It provides methods to get details about the decision instance such as the unique identifier, decision definition key and id, evaluation time, and the user that started the process instance.

```java
/**
 * Represents one evaluation of a decision.
 *
 * @author Philipp Ossler
 * @author Ingo Richtsmeier
 *
 */
public interface HistoricDecisionInstance {

  /** The unique identifier of this historic decision instance. */
  String getId();

  /** The decision definition reference. */
  String getDecisionDefinitionId();

  /** The unique identifier of the decision definition */
  String getDecisionDefinitionKey();

  /** The name of the decision definition */
  String getDecisionDefinitionName();

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
