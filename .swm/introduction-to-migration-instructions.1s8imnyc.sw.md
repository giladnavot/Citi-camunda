---
title: Introduction to Migration Instructions
---
MigrationInstruction is an interface that represents an instruction to migrate instances of one activity to another activity. These instructions are always contained in a MigrationPlan. The MigrationInstruction interface provides methods to get the source and target activity IDs, and to check if the event trigger of the flow node is updated during migration.

MigrationInstructionBuilder is an interface that provides a method to determine whether the event trigger should be updated during migration. This is particularly useful when mapping between event-receiving flow nodes that rely on a persistent event trigger.

MigrationInstructionsBuilder is an interface that provides a method to toggle whether the instructions should include updating of the respective event triggers where appropriate. This is useful when updating the event trigger means for a single instruction.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/migration/MigrationInstruction.java" line="25">

---

# MigrationInstruction Interface

This is the definition of the MigrationInstruction interface. It includes methods to get the source and target activity ids, and to check if the event trigger should be updated.

```java
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
   * @return whether this flow node's event trigger is going to be updated during
   *   migration. Can only be true for flow nodes that define a persistent event trigger.
   *   See {@link MigrationInstructionBuilder#updateEventTrigger()} for details
   */
  boolean isUpdateEventTrigger();

```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/migration/MigrationPlanImpl.java" line="35">

---

# Usage of MigrationInstruction

Here, MigrationInstruction is used in the MigrationPlanImpl class. An ArrayList of MigrationInstruction is created and methods are provided to get and set these instructions.

```java
  protected List<MigrationInstruction> instructions;

  protected VariableMap variables;

  public MigrationPlanImpl(String sourceProcessDefinitionId, String targetProcessDefinitionId) {
    this.sourceProcessDefinitionId = sourceProcessDefinitionId;
    this.targetProcessDefinitionId = targetProcessDefinitionId;
    this.instructions = new ArrayList<MigrationInstruction>();
  }

  public String getSourceProcessDefinitionId() {
    return sourceProcessDefinitionId;
  }

  public void setSourceProcessDefinitionId(String sourceProcessDefinitionId) {
    this.sourceProcessDefinitionId = sourceProcessDefinitionId;
  }

  public String getTargetProcessDefinitionId() {
    return targetProcessDefinitionId;
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/migration/instance/MigratingProcessInstance.java" line="107">

---

# MigrationInstruction in MigratingProcessInstance

In the MigratingProcessInstance class, MigrationInstruction is used as a parameter in methods to add activity, transition, and event scope instances.

```java
  public MigratingActivityInstance addActivityInstance(
      MigrationInstruction migrationInstruction,
      ActivityInstance activityInstance,
      ScopeImpl sourceScope,
      ScopeImpl targetScope,
      ExecutionEntity scopeExecution) {

    MigratingActivityInstance migratingActivityInstance = new MigratingActivityInstance(
        activityInstance,
        migrationInstruction,
        sourceScope,
        targetScope,
        scopeExecution);

    migratingActivityInstances.add(migratingActivityInstance);

    if (processInstanceId.equals(activityInstance.getId())) {
      rootInstance = migratingActivityInstance;
    }

    return migratingActivityInstance;
```

---

</SwmSnippet>

# MigrationInstruction Functions

MigrationInstruction Functions

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/migration/MigrationInstruction.java" line="31">

---

## getSourceActivityId

The `getSourceActivityId` function returns the id of the activity of the source process definition that this instruction maps instances from.

```java
  String getSourceActivityId();
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/migration/MigrationInstruction.java" line="37">

---

## getTargetActivityId

The `getTargetActivityId` function returns the id of the activity of the target process definition that this instruction maps instances to.

```java
  String getTargetActivityId();
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/migration/MigrationInstruction.java" line="44">

---

## isUpdateEventTrigger

The `isUpdateEventTrigger` function returns whether this flow node's event trigger is going to be updated during migration. It can only be true for flow nodes that define a persistent event trigger.

```java
  boolean isUpdateEventTrigger();
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
