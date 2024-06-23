---
title: Understanding Migration Process
---
Migration in the context of the Citi-camunda repository refers to the process of moving instances from one activity to another within a process definition. This is achieved through the use of a MigrationPlan, which consists of a set of MigrationInstructions. Each MigrationInstruction specifies the source and target activities for the migration. The MigrationPlan can be executed synchronously or asynchronously, and can include variables to be set in the process instance scope after the migration.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/migration/MigrationInstruction.java" line="19">

---

The MigrationInstruction interface defines the methods for getting the source and target activity IDs for the migration, and for checking if the event trigger of the flow node will be updated during the migration.

```java
/**
 * Represents an instruction to migrate instances of one activity to another activity.
 * Migration instructions are always contained in a {@link MigrationPlan}.
 *
 * @author Thorben Lindhauer
 */
public interface MigrationInstruction {

  /**
   * @return the id of the activity of the source process definition that this
   * instruction maps instances from
   */
  String getSourceActivityId();

  /**
   * @return the id of the activity of the target process definition that this
   * instruction maps instances to
   */
  String getTargetActivityId();

  /**
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/migration/MigrationPlan.java" line="23">

---

The MigrationPlan interface provides the methods for getting the source and target process definition IDs, the list of MigrationInstructions, and the variables to be set after the migration.

```java
/**
 * <p>Specifies how process instances from one process definition (the <i>source process definition</i>)
 * should be migrated to another process definition (the <i>target process definition</i>).
 *
 * <p>A migration plan consists of a number of {@link MigrationInstruction}s that tell which
 *   activity maps to which. The set of instructions is complete, i.e. the migration logic does not perform
 *   migration steps that are not given by the instructions
 *
 * <p>A migration plan can include variables which will be set into the process instance scope
 * after the migration.
 *
 * @author Thorben Lindhauer
 */
public interface MigrationPlan {

  /**
   * @return the list of instructions that this plan consists of
   */
  List<MigrationInstruction> getInstructions();

  /**
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/migration/MigrationPlanExecutionBuilder.java" line="29">

---

The MigrationPlanExecutionBuilder interface provides the methods for specifying the process instances to migrate, whether to skip custom listeners and IO mappings, and for executing the migration either synchronously or asynchronously.

```java
/**
 * Builder to execute a migration.
 */
public interface MigrationPlanExecutionBuilder {

  /**
   * @param processInstanceIds the process instance ids to migrate.
   */
  MigrationPlanExecutionBuilder processInstanceIds(List<String> processInstanceIds);

  /**
   * @param processInstanceIds the process instance ids to migrate.
   */
  MigrationPlanExecutionBuilder processInstanceIds(String... processInstanceIds);

  /**
   * @param processInstanceQuery a query which selects the process instances to migrate.
   *   Query results are restricted to process instances for which the user has {@link Permissions#READ} permission.
   */
  MigrationPlanExecutionBuilder processInstanceQuery(ProcessInstanceQuery processInstanceQuery);

```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/migration/MigrationInstruction.java" line="19">

---

# MigrationInstruction Interface

The MigrationInstruction interface represents an instruction to migrate instances of one activity to another. It contains methods to get the source and target activity IDs and to check if the event trigger is updated during migration.

```java
/**
 * Represents an instruction to migrate instances of one activity to another activity.
 * Migration instructions are always contained in a {@link MigrationPlan}.
 *
 * @author Thorben Lindhauer
 */
public interface MigrationInstruction {

  /**
   * @return the id of the activity of the source process definition that this
   * instruction maps instances from
   */
  String getSourceActivityId();

  /**
   * @return the id of the activity of the target process definition that this
   * instruction maps instances to
   */
  String getTargetActivityId();

  /**
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/migration/MigrationPlan.java" line="23">

---

# MigrationPlan Interface

The MigrationPlan interface specifies how process instances should be migrated from one process definition to another. It consists of a list of MigrationInstructions and includes methods to get the source and target process definition IDs and the variables to be set after the migration.

```java
/**
 * <p>Specifies how process instances from one process definition (the <i>source process definition</i>)
 * should be migrated to another process definition (the <i>target process definition</i>).
 *
 * <p>A migration plan consists of a number of {@link MigrationInstruction}s that tell which
 *   activity maps to which. The set of instructions is complete, i.e. the migration logic does not perform
 *   migration steps that are not given by the instructions
 *
 * <p>A migration plan can include variables which will be set into the process instance scope
 * after the migration.
 *
 * @author Thorben Lindhauer
 */
public interface MigrationPlan {

  /**
   * @return the list of instructions that this plan consists of
   */
  List<MigrationInstruction> getInstructions();

  /**
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/migration/MigrationPlanExecutionBuilder.java" line="29">

---

# MigrationPlanExecutionBuilder Interface

The MigrationPlanExecutionBuilder interface provides methods to execute a migration. It allows specifying the process instance IDs to migrate, whether to skip custom listeners and io mappings, and whether to execute the migration synchronously or asynchronously.

```java
/**
 * Builder to execute a migration.
 */
public interface MigrationPlanExecutionBuilder {

  /**
   * @param processInstanceIds the process instance ids to migrate.
   */
  MigrationPlanExecutionBuilder processInstanceIds(List<String> processInstanceIds);

  /**
   * @param processInstanceIds the process instance ids to migrate.
   */
  MigrationPlanExecutionBuilder processInstanceIds(String... processInstanceIds);

  /**
   * @param processInstanceQuery a query which selects the process instances to migrate.
   *   Query results are restricted to process instances for which the user has {@link Permissions#READ} permission.
   */
  MigrationPlanExecutionBuilder processInstanceQuery(ProcessInstanceQuery processInstanceQuery);

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
