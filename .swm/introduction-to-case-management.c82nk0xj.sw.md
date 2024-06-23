---
title: Introduction to Case Management
---
Case Management in the context of the Citi-camunda repository refers to the handling of instances of business processes, known as cases. These cases are represented by the `CaseInstance` interface, which extends the `CaseExecution` interface. A case instance can be in various states such as active, available, enabled, disabled, or terminated, and these states can be checked using methods like `isActive()`, `isAvailable()`, `isEnabled()`, `isDisabled()`, and `isTerminated()`. The `CaseInstance` also has a business key, which can be retrieved using the `getBusinessKey()` method.

The `CaseExecution` interface represents a planned item in a case instance. It provides the unique identifier of the case execution, the id of the root of the case execution tree representing the case instance, the id of the case definition of the case execution, and the id of the parent of the case execution. It also provides methods to check if the case execution is required, available, active, enabled, disabled, or terminated.

The `CaseExecutionQuery` and `CaseInstanceQuery` interfaces allow for the creation of queries to fetch case executions and case instances respectively. These queries can be customized to select case executions or instances based on various parameters such as case instance id, case definition id, case definition key, and business key.

The `CaseInstanceBuilder` interface provides a way to create a new case instance, which will be in the `ACTIVE` state. The `CaseService` interface provides access to case instances and case executions, and allows for the creation of case instances by key.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/runtime/CaseInstanceBuilder.java" line="31">

---

# CaseInstanceBuilder Interface

The CaseInstanceBuilder interface provides a fluent builder to create a new case instance. It includes methods to set the business key, tenant id, variables, and more. The create() method is used to create a new CaseInstance, which will be in the ACTIVE state.

```java
public interface CaseInstanceBuilder {

  /**
   * <p>A business key can be provided to associate the case instance with a
   * certain identifier that has a clear business meaning. This business key can
   * then be used to easily look up that case instance, see
   * {@link CaseInstanceQuery#caseInstanceBusinessKey(String)}. Providing such a
   * business key is definitely a best practice.</p>
   *
   * <p>Note that a business key MUST be unique for the given case definition WHEN
   * you have added a database constraint for it. In this case, only case instance
   * from different case definition are allowed to have the same business key and
   * the combination of caseDefinitionKey-businessKey must be unique.</p>
   *
   * @param businessKey
   *          a key that uniquely identifies the case instance in the context
   *          of the given case definition.
   *
   * @return the builder
   *
   */
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/runtime/CaseInstance.java" line="23">

---

# CaseInstance Interface

The CaseInstance interface extends the CaseExecution interface. It provides methods to get the business key of the case instance and to check if the case instance is completed.

```java
public interface CaseInstance extends CaseExecution {

  /**
   * The business key of this process instance.
   */
  String getBusinessKey();

  /**
   * <p>Returns <code>true</code> if the case instance is completed.</p>
   *
   * <p><strong>Note:</strong> If this case execution is not the case instance,
   * it will always return <code>false</code>.</p>
   */
  boolean isCompleted();

}
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/runtime/CaseInstanceQuery.java" line="29">

---

# CaseInstanceQuery Interface

The CaseInstanceQuery interface extends the Query interface and provides methods to filter case instances based on various criteria such as case instance id, business key, case definition key, and more.

```java
public interface CaseInstanceQuery extends Query<CaseInstanceQuery, CaseInstance> {

  /**
   * Select the case instance with the given id
   *
   * @param caseInstanceId the id of the case instance
   *
   * @throws NotValidException when the given case instance id is null
   */
  CaseInstanceQuery caseInstanceId(String caseInstanceId);

  /**
   * Select case instances with the given business key
   *
   * @param caseInstanceBusinessKey the business key of the case instance
   *
   * @throws NotValidException when the given case instance business key is null
   */
  CaseInstanceQuery caseInstanceBusinessKey(String caseInstanceBusinessKey);

  /**
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/runtime/CaseExecution.java" line="23">

---

# CaseExecution Interface

The CaseExecution interface provides methods to check the state of the case execution, such as whether it is required, available, or active.

```java
 *
 * @author Roman Smirnov
 *
 */
public interface CaseExecution {

  /**
   * <p>The unique identifier of the case execution.</p>
   */
  String getId();

  /**
   * <p>Id of the root of the case execution tree representing the case instance.</p>
   *
   * <p>It is the same as {@link #getId()} if this case execution is the case instance.</p>
   */
  String getCaseInstanceId();

  /**
   * <p>The id of the case definition of the case execution.</p>
   */
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/runtime/CaseExecutionQuery.java" line="30">

---

# CaseExecutionQuery Interface

The CaseExecutionQuery interface extends the Query interface and provides methods to filter case executions based on various criteria such as case instance id, case definition key, business key, and more.

```java
public interface CaseExecutionQuery extends Query<CaseExecutionQuery, CaseExecution> {

  /**
   * Only select case executions which have the given case instance id.
   *
   * @param caseInstanceId the id of the case instance
   *
   * @throws NotValidException when the given case instance id is null
   *
   */
  CaseExecutionQuery caseInstanceId(String caseInstanceId);

  /**
   * Only select case executions which have the given case definition id.
   *
   * @param caseDefinitionId the id of the case definition
   *
   * @throws NotValidException when the given case definition id is null
   *
   */
  CaseExecutionQuery caseDefinitionId(String caseDefinitionId);
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
