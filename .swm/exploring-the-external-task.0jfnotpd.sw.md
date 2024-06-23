---
title: Exploring the External Task
---
An External Task in Camunda is a BPMN Service Task that is executed by an external worker. This allows for the distribution of the workload across multiple microservices or systems. The worker fetches and locks the task, performs the work, and then completes the task, providing any output variables.

# Defining an External Task

In this BPMN model, a Service Task is defined with an External implementation. The 'camunda:type' attribute is set to 'external' and the 'camunda:topic' attribute is set to the topic that the External Task Client will subscribe to.

# Implementing an External Task Client

This is an example of an External Task Client. It subscribes to the topic defined in the BPMN model and implements the task logic in the 'execute' method. When the task is successfully completed, the 'complete' method is called to inform the Camunda engine.

# External Task Functions

External Task Functions

<SwmSnippet path="/clients/java/client/src/main/java/org/camunda/bpm/client/task/ExternalTaskHandler.java" line="1">

---

## ExternalTaskHandler

The `ExternalTaskHandler` interface defines the contract for classes that handle external tasks. It includes methods for handling a task, handling a failure, and handling a BPMN error.

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

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/ExternalTaskService.java" line="1">

---

## ExternalTaskService

The `ExternalTaskService` interface provides methods for managing and interacting with external tasks. This includes fetching and locking tasks, completing tasks, handling failures, and setting retries.

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
package org.camunda.bpm.engine;

import java.util.List;
import java.util.Map;
import org.camunda.bpm.engine.authorization.BatchPermissions;
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/externaltask/ExternalTaskQuery.java" line="1">

---

## ExternalTaskQuery

The `ExternalTaskQuery` interface provides methods for querying external tasks based on various criteria. This includes filtering by process instance, activity, and execution, as well as ordering the results.

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
import java.util.Set;

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
