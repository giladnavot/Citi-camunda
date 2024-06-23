---
title: Overview of Task in Process Automation
---
A Task in the context of the Citi-camunda repository refers to a unit of work that the system performs. Tasks are part of the process automation workflow and can be created, updated, and deleted. They can have variables associated with them, which can be manipulated as part of the task's execution. Tasks can also have comments and attachments, providing additional context or data for the task. Furthermore, tasks can be assigned to specific users or groups, and they can be claimed, unclaimed, or delegated. The completion of a task often involves submitting a form with certain variables.

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/task/create/post.ftl" line="6">

---

# Task Creation

Here we see the creation of a Task with a specific name. This is done through a POST request to the `/task/create` endpoint.

```ftl
      tag = "Task"
      summary = "Create"
      desc = "Creates a new task." />

  <@lib.requestBody
      mediaType = "application/json"
      dto = "TaskDto"
      examples = ['"example-1": {
                     "summary": "POST /task/create",
                     "value": {
                       "id": "aTaskId",
                       "name": "My Task",
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/task/{id}/claim/post.ftl" line="6">

---

# Task Operations

This is an example of a task operation - claiming a task. This is done through a POST request to the `/task/{id}/claim` endpoint. Similar operations exist for completing, deleting, and other task manipulations.

```ftl
      tag = "Task"
      summary = "Claim"
      desc = "Claims a task for a specific user.

              **Note:** The difference with the
              [Set Assignee](${docsUrl}/reference/rest/task/post-assignee/)
              method is that here a check is performed to see if the task already has a user
              assigned to it." />

  "parameters" : [

    <@lib.parameter
        name = "id"
        location = "path"
        type = "string"
        required = true
        last = true
        desc = "The id of the task to claim."/>

  ],

```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/task/{id}/variables/get.ftl" line="6">

---

# Task Variables

Tasks can have associated variables, which can be retrieved, updated, or deleted through various endpoints. This example shows the retrieval of task variables through a GET request to the `/task/{id}/variables` endpoint.

```ftl
      tag = "Task Variable"
      summary = "Get Task Variables"
      desc = "Retrieves all variables visible from the task. A variable is visible from the task if it is a local task
              variable or declared in a parent scope of the task. See documentation on
              [visiblity of variables](${docsUrl}/user-guide/process-engine/variables/)." />

  "parameters": [

    <@lib.parameter
        name = "id"
        location = "path"
        type = "string"
        required = true
        desc = "The id of the task to retrieve the variables from."/>

    <@lib.parameter
        name = "deserializeValues"
        location = "query"
        type = "boolean"
        defaultValue = "true"
        last = true
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/task/{id}/comment/get.ftl" line="6">

---

# Task Comments and Attachments

Tasks can have associated comments and attachments. These can be retrieved, created, or deleted through various endpoints. This example shows the retrieval of task comments through a GET request to the `/task/{id}/comment` endpoint.

```ftl
      tag = "Task Comment"
```

---

</SwmSnippet>

# Functions of Task

Functions of Task

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/history/HistoricTaskInstance.java" line="1">

---

## HistoricTaskInstance

The `HistoricTaskInstance` class represents a historic task instance, which is an instance of a task that was run in the past. It provides methods to retrieve information about the task, such as its ID, name, assignee, and execution time.

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

The `TaskDefinition` class represents the definition of a task. It provides methods to set and get properties of the task, such as its ID, name, and assignee.

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

The `Task` class represents a task in the BPMN model. It provides methods to manipulate the task, such as setting its ID, name, and assignee, and to retrieve information about the task.

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

# Task Comment Creation

Task Comment API

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/task/{id}/comment/create/post.ftl" line="1">

---

## createComment Endpoint

The `createComment` endpoint is used to create a comment for a specific task. It requires the task id as a path parameter and a JSON body containing the `message` and `processInstanceId`. The endpoint responds with a `CommentDto` object if the request is successful, or with an error message if the task does not exist, no comment message was submitted, or the history of the engine is disabled.

```ftl
<#macro endpoint_macro docsUrl="">
{

  <@lib.endpointInfo
      id = "createComment"
      tag = "Task Comment"
      summary = "Create"
      desc = "Creates a comment for a task by id." />

  "parameters" : [

    <@lib.parameter
        name = "id"
        location = "path"
        type = "string"
        required = true
        last = true
        desc = "The id of the task to add the comment to." />

  ],

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
