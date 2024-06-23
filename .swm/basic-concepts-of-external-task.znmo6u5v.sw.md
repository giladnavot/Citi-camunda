---
title: Basic Concepts of External Task
---
An External Task in the context of Camunda Platform 7 is a unit of work that is external to the BPMN process. It is a mechanism that allows you to delegate the processing of certain tasks within a process to an external system, while still maintaining control over the state of the process. External tasks are typically used when the work to be done as part of a process is not directly executable by the process engine, for example, when the work involves calling external services or performing complex computations.

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/external-task/fetchAndLock/post.ftl" line="6">

---

# Fetch and Lock

This is where the 'fetchAndLock' operation for an External Task is defined. It allows a worker to fetch and lock a task for processing.

```ftl
      tag = "External Task"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/external-task/{id}/priority/put.ftl" line="6">

---

# Set Priority

This is where the 'priority' operation for an External Task is defined. It allows a worker to set the priority of a task.

```ftl
      tag = "External Task"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/external-task/{id}/bpmnError/post.ftl" line="6">

---

# Handle Errors

This is where the 'bpmnError' operation for an External Task is defined. It allows a worker to report a BPMN error for a task.

```ftl
      tag = "External Task"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/external-task/{id}/retries/put.ftl" line="6">

---

# Manage Retries

This is where the 'retries' operation for an External Task is defined. It allows a worker to manage the number of retries for a task.

```ftl
      tag = "External Task"
```

---

</SwmSnippet>

# External Task Functions

Let's delve into the main functions of External Task.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/externaltask/ExternalTask.java" line="1">

---

## ExternalTask.java

The `ExternalTask.java` file defines the main interface for an external task. It includes methods for retrieving task details such as the task id, process instance id, activity id, and more. It also provides methods for handling errors and setting variables.

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
package org.camunda.bpm.engine.externaltask;

import java.util.Date;
import java.util.Map;

```

---

</SwmSnippet>

<SwmSnippet path="/clients/java/client/src/main/java/org/camunda/bpm/client/task/ExternalTaskHandler.java" line="1">

---

## ExternalTaskHandler.java

The `ExternalTaskHandler.java` file defines the interface for handling external tasks. It includes methods for executing the task and handling failures. This is where the business logic for processing the task is implemented.

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
package org.camunda.bpm.client.task;

/**
 * <p>Interface for a custom implementation of the handler, which is invoked for each fetched and locked task</p>
 *
```

---

</SwmSnippet>

# External Task Error Details Retrieval

External Task API

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/external-task/{id}/errorDetails/get.ftl" line="1">

---

## getExternalTaskErrorDetails Endpoint

The `getExternalTaskErrorDetails` endpoint is used to retrieve the error details of a running external task by its ID. It requires the ID of the external task as a path parameter. The response includes the error details for the external task if the request is successful. If the external task does not exist or has no error details, appropriate responses are returned.

```ftl
<#macro endpoint_macro docsUrl="">
{

  <@lib.endpointInfo
      id = "getExternalTaskErrorDetails"
      tag = "External Task"
      summary = "Get Error Details"
      desc = "Retrieves the error details in the context of a running external task by id." />

  "parameters" : [

    <@lib.parameter
        name = "id"
        location = "path"
        type = "string"
        required = true
        last = true
        desc = "The id of the external task for which the error details should be retrieved."/>

  ],

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
