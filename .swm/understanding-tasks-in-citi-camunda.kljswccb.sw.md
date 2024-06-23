---
title: Understanding Tasks in Citi-camunda
---
A Task in the context of Citi-camunda refers to a unit of work that the system performs as part of a process. Tasks are defined in the process model (BPMN 2.0) and are created during the execution of a process instance. They can be performed by the system (Service Task) or by a human (User Task). Tasks can be managed, assigned, and completed through the provided REST API endpoints.

# Defining a Task

Here we can see a task being defined within a process model. The `createTask()` method is used to create a new task and set its properties.

# Executing a Task

This snippet shows how a task is executed using the `executeTask()` method. The task is identified by its ID, and the method performs the action associated with the task.

# Task Functionality

Task Functionality

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/history/HistoricTaskInstance.java" line="1">

---

## HistoricTaskInstance

The `HistoricTaskInstance` class represents a historic task instance, which is an instance of a task that has been completed. It provides methods to retrieve information about the task, such as its ID, name, assignee, and completion time.

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

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/task/TaskDefinition.java" line="1">

---

## TaskDefinition

The `TaskDefinition` class defines the properties and behavior of a task. It includes methods for setting and getting the task's name, description, assignee, and other properties. It also includes methods for executing the task.

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
package org.camunda.bpm.engine.impl.task;

import java.util.HashMap;
import java.util.HashSet;
import java.util.List;
```

---

</SwmSnippet>

<SwmSnippet path="/model-api/bpmn-model/src/main/java/org/camunda/bpm/model/bpmn/instance/Task.java" line="1">

---

## Task

The `Task` interface represents a task in a BPMN process. It provides methods for setting and getting the task's properties, such as its ID, name, and assignee. It also provides methods for executing the task.

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
package org.camunda.bpm.model.bpmn.instance;

import org.camunda.bpm.model.bpmn.instance.bpmndi.BpmnShape;

/**
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
