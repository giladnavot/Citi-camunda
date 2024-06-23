---
title: User Information Management Process
---
This document will cover the process of setting user information in the Camunda BPM platform. The steps include:

1. Removing existing user information
2. Inserting new account details
3. Creating and firing historic identity link events
4. Calculating and providing removal time for historic events
5. Clearing execution data

```mermaid
graph TD;
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/persistence/entity
  setUserInfo:::mainFlowStyle --> remove
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/persistence/entity
  setUserInfo:::mainFlowStyle --> insertAccountDetails
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/persistence/entity
  remove --> clearExecution
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/persistence/entity
  clearExecution --> removeAllTasks
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/persistence/entity
  clearExecution --> removeIncidents
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/persistence/entity
  insertAccountDetails:::mainFlowStyle --> insert
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/persistence/entity
  insert:::mainFlowStyle --> fireHistoricIdentityLinkEvent
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/history/producer/DefaultHistoryEventProducer.java
  fireHistoricIdentityLinkEvent:::mainFlowStyle --> createHistoricIdentityLinkDeleteEvent
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/history/producer/DefaultHistoryEventProducer.java
  fireHistoricIdentityLinkEvent:::mainFlowStyle --> createHistoricIdentityLinkAddEvent
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/history/producer/DefaultHistoryEventProducer.java
  createHistoricIdentityLinkAddEvent:::mainFlowStyle --> createHistoricIdentityLinkEvt
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/history/producer/DefaultHistoryEventProducer.java
  createHistoricIdentityLinkEvt:::mainFlowStyle --> initHistoricIdentityLinkEvent
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/history/producer/DefaultHistoryEventProducer.java
  initHistoricIdentityLinkEvent:::mainFlowStyle --> provideRemovalTime
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/history/producer/DefaultHistoryEventProducer.java
  provideRemovalTime:::mainFlowStyle --> calculateRemovalTime
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/history/producer/DefaultHistoryEventProducer.java
  calculateRemovalTime:::mainFlowStyle --> findProcessDefinitionById
end
  findProcessDefinitionById:::mainFlowStyle --> ...

 classDef mainFlowStyle color:#000000,fill:#7CB9F4
  classDef rootsStyle color:#000000,fill:#00FFF4
```

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/persistence/entity/ExecutionEntity.java" line="1022">

---

# Removing existing user information

The `remove` function is responsible for removing existing user information. This includes removing jobs, incidents, tasks, and clearing the variable store.

```java
  public void remove() {
    super.remove();

    // removes jobs, incidents and tasks, and
    // clears the variable store
    clearExecution();

    // remove all event subscriptions for this scope, if the scope has event
    // subscriptions:
    removeEventSubscriptions();

    // finally delete this execution
    Context.getCommandContext().getExecutionManager().deleteExecution(this);
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/persistence/entity/IdentityLinkEntity.java" line="82">

---

# Inserting new account details

The `insert` function is used to insert new account details into the database. After the insertion, a historic identity link event is fired.

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

# Creating and firing historic identity link events

The `fireHistoricIdentityLinkEvent` function is responsible for creating and firing historic identity link events. These events are used to track changes in the identity link.

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

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/history/producer/DefaultHistoryEventProducer.java" line="1285">

---

# Calculating and providing removal time for historic events

The `calculateRemovalTime` function is used to calculate the removal time for historic events. This is based on the process definition associated with the history event.

```java
  protected Date calculateRemovalTime(HistoryEvent historyEvent) {
    String processDefinitionId = historyEvent.getProcessDefinitionId();
    ProcessDefinition processDefinition = findProcessDefinitionById(processDefinitionId);

    return Context.getProcessEngineConfiguration()
      .getHistoryRemovalTimeProvider()
      .calculateRemovalTime((HistoricProcessInstanceEventEntity) historyEvent, processDefinition);
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/persistence/entity/ExecutionEntity.java" line="531">

---

# Clearing execution data

The `clearExecution` function is responsible for clearing execution data. This includes removing all tasks, variable instances, jobs, and incidents.

```java
  protected void clearExecution() {
    //call the onRemove method of the execution observers
    //so they can do some clean up before
    for (ExecutionObserver observer : executionObservers) {
      observer.onClear(this);
    }

    // delete all the tasks and external tasks
    removeAllTasks();

    // delete all the variable instances
    removeVariablesLocalInternal();

    // remove all jobs
    removeJobs();

    // remove all incidents
    removeIncidents();
  }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="flows"><sup>Powered by [Swimm](/)</sup></SwmMeta>
