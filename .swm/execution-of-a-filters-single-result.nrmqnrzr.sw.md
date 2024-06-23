---
title: Execution of a Filters Single Result
---
This document will cover the process of executing a filter's single result in the Camunda BPMN engine. The process includes the following steps:

1. Executing the filter
2. Getting the filter query
3. Initializing form keys
4. Extending the task query
5. Ensuring not in 'or' query
6. Formatting the log
7. Printing the stack trace
8. Logging non-verbose
9. Collecting activity trace.

```mermaid
graph TD;
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/cmd
  execute:::mainFlowStyle --> getFilterQuery
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl
  getFilterQuery:::mainFlowStyle --> initializeFormKeys
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/cmd
  getFilterQuery:::mainFlowStyle --> getFilter
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl
  getFilter:::mainFlowStyle --> extend
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl
  extend:::mainFlowStyle --> withCandidateUsers
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl
  extend:::mainFlowStyle --> withoutCandidateGroups
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl
  extend:::mainFlowStyle --> withoutCandidateUsers
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl
  extend:::mainFlowStyle --> withCandidateGroups
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl
  withCandidateGroups:::mainFlowStyle --> ensureNotInOrQuery
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl
  ensureNotInOrQuery:::mainFlowStyle --> format
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl
  format:::mainFlowStyle --> printStackTrace
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl
  printStackTrace:::mainFlowStyle --> logNonVerbose
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl
  logNonVerbose:::mainFlowStyle --> collectActivityTrace
end
  collectActivityTrace:::mainFlowStyle --> ...

 classDef mainFlowStyle color:#000000,fill:#7CB9F4
  classDef rootsStyle color:#000000,fill:#00FFF4
```

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/cmd/ExecuteFilterSingleResultCmd.java" line="1">

---

# Executing the filter

The `execute` function in `ExecuteFilterSingleResultCmd.java` is the entry point for this process. It is responsible for executing a filter's single result.

```java
/*
 * Copyright Camunda Services GmbH and/or licensed to Camunda Services GmbH
 * under one or more contributor license agreements. See the NOTICE file
 * distributed with this work for additional information regarding copyright
 * ownership. Camunda licenses this file to you under the Apache License,
 * Version 2.0; you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *     http://www.apache.org/licenses/LICENSE-2.0
 *
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/cmd/AbstractExecuteFilterCmd.java" line="65">

---

# Getting the filter query

The `getFilterQuery` function is called to retrieve the filter query. If the query is an instance of `TaskQuery`, its form keys are initialized.

```java
  protected Query<?, ?> getFilterQuery(CommandContext commandContext) {
    Filter filter = getFilter(commandContext);
    Query<?, ?> query = filter.getQuery();
    if (query instanceof TaskQuery) {
      ((TaskQuery) query).initializeFormKeys();
    }
    return query;
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/TaskQueryImpl.java" line="1067">

---

# Initializing form keys

The `initializeFormKeys` function is called to ensure that the form keys are not in 'or' query.

```java
  @Override
  public TaskQuery initializeFormKeys() {
    ensureNotInOrQuery("initializeFormKeys()");
    this.initializeFormKeys = true;
    return this;
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/TaskQueryImpl.java" line="1803">

---

# Extending the task query

The `extend` function is called to extend the task query with additional parameters. This includes task name, assignee, involved user, owner, and many others.

```java
  @Override
  public TaskQuery extend(TaskQuery extending) {
    TaskQueryImpl extendingQuery = (TaskQueryImpl) extending;
    TaskQueryImpl extendedQuery = new TaskQueryImpl();

    // only add the base query's validators to the new query;
    // this is because the extending query's validators may not be applicable to the base
    // query and should therefore be executed before extending the query
    extendedQuery.validators = new HashSet<>(validators);

    if (extendingQuery.getName() != null) {
      extendedQuery.taskName(extendingQuery.getName());
    }
    else if (this.getName() != null) {
      extendedQuery.taskName(this.getName());
    }

    if (extendingQuery.getNameLike() != null) {
      extendedQuery.taskNameLike(extendingQuery.getNameLike());
    }
    else if (this.getNameLike() != null) {
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/TaskQueryImpl.java" line="1229">

---

# Ensuring not in 'or' query

The `ensureNotInOrQuery` function is called to ensure that the query is not in 'or' query. If it is, an exception is thrown.

```java
  protected void ensureNotInOrQuery(String methodName) {
    if (isOrQueryActive) {
      throw new ProcessEngineException(String.format("Invalid query usage: cannot set %s within 'or' query", methodName));
    }
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/util/LogUtil.java" line="82">

---

# Formatting the log

The `format` function is called to format the log record. It includes the date, thread ID, message, and other details.

```java
    public String format(LogRecord record) {
      StringBuilder line = new StringBuilder();
      line.append(dateFormat.format(new Date()));
      if (Level.FINE.equals(record.getLevel())) {
        line.append(" FIN ");
      } else if (Level.FINEST.equals(record.getLevel())) {
        line.append(" FST ");
      } else if (Level.INFO.equals(record.getLevel())) {
        line.append(" INF ");
      } else if (Level.SEVERE.equals(record.getLevel())) {
        line.append(" SEV ");
      } else if (Level.WARNING.equals(record.getLevel())) {
        line.append(" WRN ");
      } else if (Level.FINER.equals(record.getLevel())) {
        line.append(" FNR ");
      } else if (Level.CONFIG.equals(record.getLevel())) {
        line.append(" CFG ");
      }

      int threadId = record.getThreadID();
      String threadIndent = getThreadIndent(threadId);
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/interceptor/BpmnStackTrace.java" line="39">

---

# Printing the stack trace

The `printStackTrace` function is called to print the BPMN stack trace. It logs the failed operation and the activity trace.

```java
  public void printStackTrace(boolean verbose) {
    if(perfromedInvocations.isEmpty()) {
      return;
    }

    StringWriter writer = new StringWriter();
    writer.write("BPMN Stack Trace:\n");

    if(!verbose) {
      logNonVerbose(writer);
    }
    else {
      logVerbose(writer);
    }

    LOG.bpmnStackTrace(writer.toString());

    perfromedInvocations.clear();
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/interceptor/BpmnStackTrace.java" line="59">

---

# Logging non-verbose

The `logNonVerbose` function is called to log the stack trace in a non-verbose manner. It logs the failed operation and the activity trace.

```java
  protected void logNonVerbose(StringWriter writer) {

    // log the failed operation verbosely
    writeInvocation(perfromedInvocations.get(perfromedInvocations.size() - 1), writer);

    // log human consumable trace of activity ids and names
    List<Map<String, String>> activityTrace = collectActivityTrace();
    logActivityTrace(writer, activityTrace);
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/interceptor/BpmnStackTrace.java" line="99">

---

# Collecting activity trace

The `collectActivityTrace` function is called to collect the activity trace. It returns a list of activities with their IDs and names.

```java
  protected List<Map<String, String>> collectActivityTrace() {
    List<Map<String, String>> activityTrace = new ArrayList<Map<String, String>>();
    for (AtomicOperationInvocation atomicOperationInvocation : perfromedInvocations) {
      String activityId = atomicOperationInvocation.getActivityId();
      if(activityId == null) {
        continue;
      }

      Map<String, String> activity = new HashMap<String, String>();
      activity.put("activityId", activityId);

      String activityName = atomicOperationInvocation.getActivityName();
      if (activityName != null) {
        activity.put("activityName", activityName);
      }

      if(activityTrace.isEmpty() ||
          !activity.get("activityId").equals(activityTrace.get(0).get("activityId"))) {
        activityTrace.add(0, activity);
      }
    }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="flows"><sup>Powered by [Swimm](/)</sup></SwmMeta>
