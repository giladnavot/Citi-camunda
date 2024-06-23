---
title: Understanding Basic Concepts of Process Instance
---
A Process Instance in Camunda represents a single execution of a process definition. It is the concrete representation of a running process, containing the current state of the process, including the values of variables, the active activities, and the history of completed activities. Process Instances can be manipulated in various ways, such as being activated, suspended, or deleted. They can also have their variables retrieved or updated, and their execution state modified.

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/process-instance/post.ftl" line="6">

---

## Starting a Process Instance

This is where a new Process Instance is started.

```ftl
      tag = "Process Instance"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/process-instance/{id}/get.ftl" line="6">

---

## Retrieving Process Instance State

This endpoint is used to retrieve the state of a Process Instance.

```ftl
      summary = "Get Process Instance"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/process-instance/{id}/modification/post.ftl" line="7">

---

## Modifying Process Instance Execution State

This endpoint is used to modify the execution state of a Process Instance.

```ftl
      summary = "Modify Process Instance Execution State"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/process-instance/{id}/delete.ftl" line="5">

---

## Deleting a Process Instance

This endpoint is used to delete a Process Instance.

```ftl
      tag = "Process Instance"
```

---

</SwmSnippet>

# Functions of Process Instance

This section will cover the main functions of the Process Instance in Camunda Platform 7.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/runtime/ProcessInstance.java" line="1">

---

## ProcessInstance

The `ProcessInstance` is a central interface that represents an execution of a process definition within the engine. It provides methods for managing and querying process instances.

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

<SwmSnippet path="/engine-rest/engine-rest/src/main/java/org/camunda/bpm/engine/rest/dto/runtime/ActivityInstanceDto.java" line="1">

---

## ActivityInstanceDto

`ActivityInstanceDto` is a Data Transfer Object that carries data related to an activity instance in a process. It is used when interacting with the REST API.

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
package org.camunda.bpm.engine.rest.dto.runtime;

import org.camunda.bpm.engine.runtime.ActivityInstance;

/**
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/history/HistoricActivityInstance.java" line="1">

---

## HistoricActivityInstance

`HistoricActivityInstance` represents a historic activity instance, which is an instance of an activity that was executed in the past. It provides information about the start and end time of the activity, the assigned user, and other details.

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

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
