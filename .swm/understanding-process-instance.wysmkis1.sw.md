---
title: Understanding Process Instance
---
A Process Instance in Camunda refers to an execution of a process definition. It represents a single path of execution through a process, including its current state, past activities, and data associated with the process. It's essentially a running instance of a process model, with its own set of variables and activities.

## Starting a Process Instance

This code snippet shows how to start a Process Instance. The `startProcessInstanceByKey` method is used, which takes the process definition key as a parameter. This key is used to find the latest version of the process definition and start a new instance of it.

## Managing Process Instances

This code snippet shows how to manage Process Instances. The `runtimeService` provides methods to control and query Process Instances. For example, the `suspendProcessInstanceById` method is used to suspend a running Process Instance.

# Functions of Process Instance

Let's delve into the functions of Process Instance.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/runtime/ProcessInstance.java" line="1">

---

## ProcessInstance.java

The ProcessInstance.java file contains the main functions that define a process instance. These functions include methods for starting, stopping, and managing the process instance.

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

import org.camunda.bpm.engine.repository.ProcessDefinition;

/**
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/runtime/ProcessInstanceQuery.java" line="1">

---

## ProcessInstanceQuery.java

The ProcessInstanceQuery.java file contains functions for querying process instances. These functions allow you to retrieve process instances based on various criteria, such as process definition, business key, and process instance variables.

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

import java.io.Serializable;
import java.util.Set;

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
