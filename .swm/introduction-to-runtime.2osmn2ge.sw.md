---
title: Introduction to Runtime
---
In the context of the Citi-camunda repository, Runtime refers to a package within the Camunda BPM engine. This package, `org.camunda.bpm.engine.runtime`, contains classes and interfaces that are crucial for the execution of processes. These include `ProcessInstance`, `ActivityInstance`, `CaseExecution`, and others. These classes and interfaces define the behavior of process instances, activities, and cases at runtime. They are used to manage and control process execution, handle incidents, and interact with process variables.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/runtime/RestartProcessInstanceBuilder.java" line="73">

---

# The 'execute' Method

This method is part of the Runtime functionality. It is used to execute the restart of a process instance synchronously. If the affected instances count exceeds the maximum results limit, a 'BadUserRequestException' is thrown. The maximum results limit can be specified with the process engine configuration property 'queryMaxResultsLimit'. If the limit is exceeded, it is recommended to use the batch operation 'executeAsync()' instead.

```java
  /**
   * Executes the restart synchronously.
   * @throws BadUserRequestException
   *   When the affected instances count exceeds the maximum results limit. A maximum results
   *   limit can be specified with the process engine configuration property
   *   <code>queryMaxResultsLimit</code> (default {@link Integer#MAX_VALUE}).
   *   Please use the batch operation {@link #executeAsync()} instead.
   */
  void execute();
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
