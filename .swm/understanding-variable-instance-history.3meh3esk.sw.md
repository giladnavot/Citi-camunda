---
title: Understanding Variable Instance History
---
Variable Instance History refers to the historical data of a variable instance in the Camunda Platform. It provides a way to track and manage the lifecycle of a variable instance, including its creation, modification, and deletion. This is particularly useful for auditing and debugging purposes.

The Variable Instance History is accessible through various API endpoints. These endpoints allow you to get a variable instance, get the count of variable instances, and delete a variable instance. Each of these operations is associated with a specific path in the 'history/variable-instance' directory.

For example, the 'get' operation retrieves the details of a variable instance, while the 'delete' operation removes a variable instance. The 'count' operation, on the other hand, returns the total number of variable instances. These operations can be performed either via a GET or POST request, depending on the specific endpoint.

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/history/variable-instance/{id}/get.ftl" line="6">

---

## Retrieving Variable Instances

This API endpoint is used to retrieve a specific variable instance by its ID. If the variable instance does not exist, an error message is returned.

```ftl
      tag = "Historic Variable Instance"
      summary = "Get Variable Instance"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/history/variable-instance/{id}/delete.ftl" line="6">

---

## Deleting Variable Instances

This API endpoint is used to delete a specific variable instance by its ID. If the variable instance does not exist, an error message is returned.

```ftl
      tag = "Historic Variable Instance"
      summary = "Delete Variable Instance"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/history/variable-instance/count/get.ftl" line="6">

---

## Getting Variable Instance Count

This API endpoint is used to get the count of variable instances. This can be useful for understanding the volume of variables within a process instance.

```ftl
      tag = "Historic Variable Instance"
      summary = "Get Variable Instance Count"
```

---

</SwmSnippet>

# Variable Instance History Functions

The Variable Instance History is a key component in the Camunda Platform 7. It is used to track the changes in the variables over the lifecycle of a process instance. This allows for a detailed audit trail and can be used for debugging, analysis, and reporting purposes.

<SwmSnippet path="/engine-rest/engine-rest/src/main/java/org/camunda/bpm/engine/rest/dto/history/HistoricVariableInstanceDto.java" line="1">

---

## HistoricVariableInstanceDto

The `HistoricVariableInstanceDto` class is a Data Transfer Object that carries the data of a historic variable instance between processes. It includes information such as the variable's name, type, value, and the process instance it is associated with.

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

import java.util.Date;

import org.camunda.bpm.engine.history.HistoricVariableInstance;
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest/src/main/java/org/camunda/bpm/engine/rest/dto/history/HistoricVariableInstanceQueryDto.java" line="1">

---

## HistoricVariableInstanceQueryDto

The `HistoricVariableInstanceQueryDto` class is used to create queries for historic variable instances. It allows for filtering based on various criteria such as variable name, process instance ID, and variable value.

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

<SwmSnippet path="/engine-rest/engine-rest/src/main/java/org/camunda/bpm/engine/rest/history/HistoricVariableInstanceRestService.java" line="1">

---

## HistoricVariableInstanceRestService

The `HistoricVariableInstanceRestService` class provides the REST API endpoints for interacting with historic variable instances. This includes operations such as retrieving a specific historic variable instance, querying for historic variable instances, and counting the number of historic variable instances that match a certain criteria.

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
package org.camunda.bpm.engine.rest.history;

import org.camunda.bpm.engine.history.HistoricVariableInstanceQuery;
import org.camunda.bpm.engine.rest.dto.CountResultDto;
import org.camunda.bpm.engine.rest.dto.history.HistoricVariableInstanceDto;
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
