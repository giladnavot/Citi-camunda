---
title: Getting Started with Execution in Citi-camunda
---
Execution in the context of the Citi-camunda repository refers to the process of running a workflow or process automation. It involves the actual running of the tasks and activities defined in the BPMN 2.0 process engine. This includes the execution of tasks, handling of events, and the management of process instances.

# Execution Process

The execution process begins with defining your workflows and processes using the native BPMN 2.0 process engine. These defined processes are then executed within the Java Virtual Machine, allowing for process implementation, execution, design, operations, and human task management. This execution process is integral to the automation capabilities of the Camunda Platform.

# Execution Functions Overview

The Execution functions are a key part of the Camunda Platform's process automation capabilities. They are used to manage and track the execution of tasks and activities within a workflow.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/history/HistoricActivityInstance.java" line="1">

---

## HistoricActivityInstance

The `HistoricActivityInstance` function is used to track the execution of activities within a process. It provides historical data about the activity, such as when it was started, ended, and the duration.

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

The `HistoricTaskInstance` function is similar to `HistoricActivityInstance`, but it specifically tracks tasks. It provides historical data about the task, such as the assignee, due date, and completion time.

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

The `Execution` function is a representation of the runtime execution of a process instance. It is used to manage and control the execution of activities within a process.

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
