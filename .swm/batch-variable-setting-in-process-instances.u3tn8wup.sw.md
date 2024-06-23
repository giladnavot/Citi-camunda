---
title: Batch Variable Setting in Process Instances
---
This document will cover the process of setting variables to process instances in batches, which includes:

 1. Collecting process instance IDs
 2. Setting variables by batch ID
 3. Checking Java serialization
 4. Inserting identity link entities
 5. Firing historic identity link events
 6. Creating historic identity link events
 7. Initializing historic identity link events
 8. Providing removal time for historic batches
 9. Listing deployment ID mappings
10. Executing the query.

```mermaid
graph TD;
subgraph engine/src/main/java/org/camunda/bpm/engine/impl
  execute:::mainFlowStyle --> collectProcessInstanceIds
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/core
  execute:::mainFlowStyle --> setVariablesByBatchId
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl
  collectProcessInstanceIds --> listDeploymentIdMappings
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl
  listDeploymentIdMappings --> execute
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/core
  setVariablesByBatchId:::mainFlowStyle --> setVariableByBatchId
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/core
  setVariableByBatchId:::mainFlowStyle --> checkJavaSerialization
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl
  setVariableByBatchId:::mainFlowStyle --> createAndInsert
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/core
  checkJavaSerialization --> javaSerializationProhibitedException
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl
  javaSerializationProhibitedException --> format
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl
  createAndInsert:::mainFlowStyle --> insert
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl
  insert:::mainFlowStyle --> fireHistoricIdentityLinkEvent
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl
  fireHistoricIdentityLinkEvent:::mainFlowStyle --> createHistoricIdentityLinkDeleteEvent
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl
  fireHistoricIdentityLinkEvent:::mainFlowStyle --> createHistoricIdentityLinkAddEvent
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl
  createHistoricIdentityLinkAddEvent:::mainFlowStyle --> createHistoricIdentityLinkEvt
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl
  createHistoricIdentityLinkEvt:::mainFlowStyle --> initHistoricIdentityLinkEvent
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl
  initHistoricIdentityLinkEvent:::mainFlowStyle --> provideRemovalTime
end
  provideRemovalTime:::mainFlowStyle --> ...

 classDef mainFlowStyle color:#000000,fill:#7CB9F4
  classDef rootsStyle color:#000000,fill:#00FFF4
```

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/cmd/batch/variables/SetVariablesToProcessInstancesBatchCmd.java" line="115">

---

# Collecting process instance IDs

The function `collectProcessInstanceIds` is used to collect the IDs of process instances. It checks if the process instance IDs are not empty and then adds the deployment mappings to the `elementConfiguration`.

```java
  protected BatchElementConfiguration collectProcessInstanceIds(CommandContext commandContext) {
    BatchElementConfiguration elementConfiguration = new BatchElementConfiguration();

    if (!CollectionUtil.isEmpty(processInstanceIds)) {
      ProcessInstanceQueryImpl query = new ProcessInstanceQueryImpl();
      query.processInstanceIds(new HashSet<>(processInstanceIds));
      List<ImmutablePair<String, String>> mappings =
          commandContext.runWithoutAuthorization(query::listDeploymentIdMappings);
      elementConfiguration.addDeploymentMappings(mappings);
    }

    ProcessInstanceQueryImpl processInstanceQuery =
        (ProcessInstanceQueryImpl) this.processInstanceQuery;
    if (processInstanceQuery != null) {
      List<ImmutablePair<String, String>> mappings =
          processInstanceQuery.listDeploymentIdMappings();
      elementConfiguration.addDeploymentMappings(mappings);
    }

    HistoricProcessInstanceQueryImpl historicProcessInstanceQuery =
        (HistoricProcessInstanceQueryImpl) this.historicProcessInstanceQuery;
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/core/variable/VariableUtil.java" line="109">

---

# Setting variables by batch ID

The function `setVariableByBatchId` is used to set variables by batch ID. It checks if the variable is transient and throws an exception if it is. It then checks Java serialization and creates and inserts a variable instance.

```java
  public static void setVariableByBatchId(String batchId, String variableName, Object variableValue) {
    TypedValue variableTypedValue = Variables.untypedValue(variableValue);

    boolean isTransient = variableTypedValue.isTransient();
    if (isTransient) {
      throw CMD_LOGGER.exceptionSettingTransientVariablesAsyncNotSupported(variableName);
    }

    checkJavaSerialization(variableName, variableTypedValue);

    VariableInstanceEntity variableInstance =
        VariableInstanceEntity.createAndInsert(variableName, variableTypedValue);

    variableInstance.setVariableScopeId(batchId);
    variableInstance.setBatchId(batchId);
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/core/variable/VariableUtil.java" line="81">

---

# Checking Java serialization

The function `checkJavaSerialization` is used to check if Java serialization is prohibited for the variable. If it is, it throws a `javaSerializationProhibitedException`.

```java
  public static void checkJavaSerialization(String variableName, TypedValue value) {
    if (isJavaSerializationProhibited(value)) {
      throw CORE_LOGGER.javaSerializationProhibitedException(variableName);
    }
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/persistence/entity/IdentityLinkEntity.java" line="82">

---

# Inserting identity link entities

The function `insert` is used to insert an identity link entity and then fire a historic identity link event.

```java
  public void insert() {
    Context
      .getCommandContext()
      .getDbEntityManager()
      .insert(this);
    fireHistoricIdentityLinkEvent(HistoryEventTypes.IDENTITY_LINK_ADD);
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/persistence/entity/IdentityLinkEntity.java" line="204">

---

# Firing historic identity link events

The function `fireHistoricIdentityLinkEvent` is used to fire a historic identity link event. It checks if the history level is event produced and then processes history events.

```java
  public void fireHistoricIdentityLinkEvent(final HistoryEventType eventType) {
    ProcessEngineConfigurationImpl processEngineConfiguration = Context.getProcessEngineConfiguration();

    HistoryLevel historyLevel = processEngineConfiguration.getHistoryLevel();
    if(historyLevel.isHistoryEventProduced(eventType, this)) {

      HistoryEventProcessor.processHistoryEvents(new HistoryEventProcessor.HistoryEventCreator() {
        @Override
        public HistoryEvent createHistoryEvent(HistoryEventProducer producer) {
          HistoryEvent event = null;
          if (HistoryEvent.IDENTITY_LINK_ADD.equals(eventType.getEventName())) {
            event = producer.createHistoricIdentityLinkAddEvent(IdentityLinkEntity.this);
          } else if (HistoryEvent.IDENTITY_LINK_DELETE.equals(eventType.getEventName())) {
            event = producer.createHistoricIdentityLinkDeleteEvent(IdentityLinkEntity.this);
          }
          return event;
        }
      });

    }
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/history/producer/DefaultHistoryEventProducer.java" line="945">

---

# Creating historic identity link events

The function `createHistoricIdentityLinkEvt` is used to create a historic identity link event. It initializes the historic identity link event with the identity link and event type.

```java
  @Override
  public HistoryEvent createHistoricIdentityLinkDeleteEvent(IdentityLink identityLink) {
    return createHistoricIdentityLinkEvt(identityLink, HistoryEventTypes.IDENTITY_LINK_DELETE);
  }

  protected HistoryEvent createHistoricIdentityLinkEvt(IdentityLink identityLink, HistoryEventTypes eventType) {
    // create historic identity link event
    HistoricIdentityLinkLogEventEntity evt = newIdentityLinkEventEntity();
    // Mapping all the values of identity link to HistoricIdentityLinkEvent
    initHistoricIdentityLinkEvent(evt, identityLink, eventType);
    return evt;
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/history/producer/DefaultHistoryEventProducer.java" line="962">

---

# Initializing historic identity link events

The function `initHistoricIdentityLinkEvent` is used to initialize a historic identity link event. It sets various properties of the event and provides removal time if the history removal time strategy is start.

```java
  protected void initHistoricIdentityLinkEvent(HistoricIdentityLinkLogEventEntity evt, IdentityLink identityLink, HistoryEventType eventType) {

    if (identityLink.getTaskId() != null) {
      TaskEntity task = Context
          .getCommandContext()
          .getTaskManager()
          .findTaskById(identityLink.getTaskId());

      evt.setProcessDefinitionId(task.getProcessDefinitionId());

      if (task.getProcessDefinition() != null) {
        evt.setProcessDefinitionKey(task.getProcessDefinition().getKey());
      }

      ExecutionEntity execution = task.getExecution();
      if (execution != null) {
        evt.setRootProcessInstanceId(execution.getRootProcessInstanceId());

        if (isHistoryRemovalTimeStrategyStart()) {
          provideRemovalTime(evt);
        }
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/history/producer/DefaultHistoryEventProducer.java" line="1300">

---

# Providing removal time for historic batches

The function `provideRemovalTime` is used to provide removal time for historic batches. It calculates the removal time and sets it if it is not null.

```java
  protected void provideRemovalTime(HistoricBatchEntity historicBatch) {
    Date removalTime = calculateRemovalTime(historicBatch);
    if (removalTime != null) {
      historicBatch.setRemovalTime(removalTime);
    }
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/AbstractQuery.java" line="369">

---

# Listing deployment ID mappings

The function `listDeploymentIdMappings` is used to list deployment ID mappings. It executes the command and checks the max results limit.

```java
  @SuppressWarnings("unchecked")
  public List<ImmutablePair<String, String>> listDeploymentIdMappings() {
    this.resultType = ResultType.LIST_DEPLOYMENT_ID_MAPPINGS;
    List<ImmutablePair<String, String>> ids = null;
    if (commandExecutor != null) {
      ids = (List<ImmutablePair<String, String>>) commandExecutor.execute(this);
    } else {
      ids = evaluateExpressionsAndExecuteDeploymentIdMappingsList(Context.getCommandContext());
    }

    if (ids != null) {
      QueryMaxResultsLimitUtil.checkMaxResultsLimit(ids.size());
    }

    return ids;
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/AbstractQuery.java" line="191">

---

# Executing the query

The function `execute` is used to execute the query. It checks the result type and calls the appropriate function to execute the query.

```java
  public Object execute(CommandContext commandContext) {
    if (resultType==ResultType.LIST) {
      return evaluateExpressionsAndExecuteList(commandContext, null);
    } else if (resultType==ResultType.SINGLE_RESULT) {
      return executeSingleResult(commandContext);
    } else if (resultType==ResultType.LIST_PAGE) {
      return evaluateExpressionsAndExecuteList(commandContext, null);
    } else if (resultType == ResultType.LIST_IDS) {
      return evaluateExpressionsAndExecuteIdsList(commandContext);
    } else if (resultType == ResultType.LIST_DEPLOYMENT_ID_MAPPINGS) {
      return evaluateExpressionsAndExecuteDeploymentIdMappingsList(commandContext);
    } else {
      return evaluateExpressionsAndExecuteCount(commandContext);
    }
  }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="flows"><sup>Powered by [Swimm](/)</sup></SwmMeta>
