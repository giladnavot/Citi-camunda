---
title: Understanding the Execution Concept
---
Execution in the Citi-camunda project refers to the running instance of a process. It is a fundamental concept in the Camunda BPMN platform, representing the smallest unit of work within a process. Executions are responsible for carrying out the modeled behavior of a process, such as transitioning through various states, triggering events, and managing local variables.

The Execution API, as seen in the engine-rest module, provides a set of operations for interacting with executions. These operations include retrieving execution details, triggering an execution, managing local variables of an execution, and more. Each operation is represented by a different endpoint in the API.

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/execution/{id}/signal/post.ftl" line="6">

---

# Trigger Execution

This endpoint is used to trigger an execution. It starts or resumes the execution of a process.

```ftl
      tag = "Execution"
      summary = "Trigger Execution"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/execution/{id}/localVariables/get.ftl" line="6">

---

# Manage Execution Variables

This endpoint is used to get the local variables of an execution. These variables can be used to store and manage data within the scope of the execution.

```ftl
      tag = "Execution"
      summary = "Get Local Execution Variables"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/execution/{id}/get.ftl" line="6">

---

# Retrieve Execution Data

This endpoint is used to retrieve data about an execution. It provides information about the state of the execution and any associated data.

```ftl
      tag = "Execution"
      summary = "Get Execution"
      desc = "Retrieves an execution by id, according to the `Execution` interface in the
```

---

</SwmSnippet>

# Execution Functions

This section covers the main functions related to Execution in the Camunda BPM platform.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/history/HistoricActivityInstance.java" line="1">

---

## HistoricActivityInstance

The `HistoricActivityInstance` function is used to track the execution of activities in the process. It provides historical data about the execution of activities.

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
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */
package org.camunda.bpm.engine.history;

import java.util.Date;

/**
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/history/HistoricTaskInstance.java" line="1">

---

## HistoricTaskInstance

The `HistoricTaskInstance` function is used to track the execution of tasks in the process. It provides historical data about the execution of tasks.

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
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */
package org.camunda.bpm.engine.history;

import java.util.Date;


```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/runtime/Execution.java" line="1">

---

## Execution

The `Execution` function is the main function that handles the execution of processes. It is responsible for managing the state of the process and coordinating the execution of activities and tasks.

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
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */
package org.camunda.bpm.engine.runtime;



/**
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
