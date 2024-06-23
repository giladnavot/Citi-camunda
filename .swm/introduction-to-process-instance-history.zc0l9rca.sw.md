---
title: Introduction to Process Instance History
---
Process Instance History in Camunda refers to the historical data of a process instance. It is a record of all the events that have occurred during the lifecycle of a process instance, including start, end, and any tasks or activities that were executed. This historical data is crucial for auditing, analysis, and troubleshooting purposes.

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/history/process-instance/get.ftl" line="5">

---

## Accessing Process Instance History

This code snippet shows how to access the Process Instance History. The `get` method is used to retrieve the history of a specific process instance.

```ftl
      tag = "Historic Process Instance"
      summary = "Get List"
      desc = "Queries for historic process instances that fulfill the given parameters.
              The size of the result set can be retrieved by using the
              [Get Process Instance Count](${docsUrl}/reference/rest/history/process-instance/get-process-instance-query-count/) method." />
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/history/process-instance/delete/post.ftl" line="5">

---

## Modifying Process Instance History

This code snippet demonstrates how to delete a process instance from the history. The `delete` method is used to remove a specific process instance from the history.

```ftl
      tag = "Historic Process Instance"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/history/process-instance/count/get.ftl" line="5">

---

## Counting Process Instances

This code snippet shows how to get the count of process instances. The `get` method is used to retrieve the count of process instances.

```ftl
      tag = "Historic Process Instance"
      summary = "Get List Count"
      desc = "Queries for the number of historic process instances that fulfill the given parameters.
              Takes the same parameters as the [Get Process Instances](${docsUrl}/reference/rest/history/process-instance/get-process-instance-query/) method." />
```

---

</SwmSnippet>

# Process Instance History Functions

The Process Instance History is a key component in the Citi-camunda project. It is implemented in various parts of the codebase, including the engine and webapps frontend. The main functions related to Process Instance History are HistoricProcessInstanceQueryDto, DeleteProcessInstancesDto, and HistoricProcessInstance.

<SwmSnippet path="/engine-rest/engine-rest/src/main/java/org/camunda/bpm/engine/rest/dto/history/HistoricProcessInstanceQueryDto.java" line="1">

---

## HistoricProcessInstanceQueryDto

The `HistoricProcessInstanceQueryDto` function is used to query historic process instances. It allows for filtering, sorting, and retrieving process instances based on various parameters.

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
package org.camunda.bpm.engine.rest.dto.history;

import static java.lang.Boolean.TRUE;

import java.util.ArrayList;
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest/src/main/java/org/camunda/bpm/engine/rest/dto/runtime/batch/DeleteProcessInstancesDto.java" line="1">

---

## DeleteProcessInstancesDto

The `DeleteProcessInstancesDto` function is used to delete process instances. It provides the functionality to delete a batch of process instances in a single operation.

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
package org.camunda.bpm.engine.rest.dto.runtime.batch;

import org.camunda.bpm.engine.rest.dto.history.HistoricProcessInstanceQueryDto;
import org.camunda.bpm.engine.rest.dto.runtime.ProcessInstanceQueryDto;

```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/history/HistoricProcessInstance.java" line="1">

---

## HistoricProcessInstance

The `HistoricProcessInstance` function represents a historic process instance, which is an instance of a process definition that has completed. It provides information about the process instance, such as the start time, end time, and duration.

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
import org.camunda.bpm.engine.IdentityService;
import org.camunda.bpm.engine.runtime.ProcessInstance;
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
