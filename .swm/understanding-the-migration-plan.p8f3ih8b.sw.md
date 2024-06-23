---
title: Understanding the Migration Plan
---
The MigrationPlan in Citi-camunda refers to a specification that dictates how process instances from one process definition (the source process definition) should be migrated to another process definition (the target process definition). It consists of a number of MigrationInstructions that map which activity corresponds to which. The migration logic does not perform migration steps that are not given by the instructions. A MigrationPlan can also include variables which will be set into the process instance scope after the migration.

The MigrationPlanBuilder is an interface that provides methods to build a MigrationPlan. It allows to map activities from the source to the target process definition, set variables for the process instance after migration, and build the final MigrationPlan.

The MigrationPlanExecutionBuilder is an interface that provides methods to execute a migration. It allows to set the process instance ids to migrate, skip custom listeners and io mappings during migration, and execute the migration either synchronously or asynchronously.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/migration/MigrationPlan.java" line="23">

---

# MigrationPlan Interface

This is the definition of the MigrationPlan interface. It includes methods to get the list of migration instructions, the source and target process definition IDs, and the variables to be set after the migration.

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

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/migration/MigrationPlanExecutionBuilderImpl.java" line="39">

---

# Using MigrationPlan

This is an example of how the MigrationPlan is used. In this case, the MigrationPlan is passed to the MigrationPlanExecutionBuilderImpl constructor, which is used to execute the migration.

```java
  public MigrationPlanExecutionBuilderImpl(CommandExecutor commandExecutor, MigrationPlan migrationPlan) {
    this.commandExecutor = commandExecutor;
    this.migrationPlan = migrationPlan;
  }

  public MigrationPlan getMigrationPlan() {
    return migrationPlan;
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/migration/MigrationPlanBuilder.java" line="57">

---

# Building a MigrationPlan

The build method is used to create a MigrationPlan with all previously specified instructions. It throws a MigrationPlanValidationException if the migration plan contains instructions that are not valid.

```java
  MigrationPlan build();
```

---

</SwmSnippet>

# Migration Plan Functions

This section will cover the main functions of the Migration Plan.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/migration/MigrationPlan.java" line="38">

---

## getInstructions

The `getInstructions` function returns the list of instructions that the Migration Plan consists of. Each instruction represents a mapping from a source activity to a target activity.

```java
  /**
   * @return the list of instructions that this plan consists of
   */
  List<MigrationInstruction> getInstructions();
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/migration/MigrationPlan.java" line="43">

---

## getSourceProcessDefinitionId

The `getSourceProcessDefinitionId` function returns the ID of the process definition that is being migrated from. This is the source process definition that the instances are currently running on.

```java
  /**
   * @return the id of the process definition that is migrated from
   */
  String getSourceProcessDefinitionId();
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/migration/MigrationPlan.java" line="48">

---

## getTargetProcessDefinitionId

The `getTargetProcessDefinitionId` function returns the ID of the process definition that is being migrated to. This is the target process definition that the instances will be running on after the migration.

```java
  /**
   * @return the id of the process definition that is migrated to
   */
  String getTargetProcessDefinitionId();
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/migration/MigrationPlan.java" line="53">

---

## getVariables

The `getVariables` function returns the variables that will be set into the process instance scope after the migration. These variables can be used to pass data between the source and target process definitions.

```java
  /**
   * @return the variables to be set after the migration to the process instances' scope
   */
  VariableMap getVariables();
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
