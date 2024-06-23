---
title: Introduction to the External Task Log
---
The External Task Log in Citi-camunda refers to a historical record of external tasks. It provides functionalities to retrieve these logs, their error details, and their count. These functionalities are exposed via REST APIs, which can be accessed through GET and POST requests. The logs provide valuable insights into the execution of external tasks, which are tasks that are processed by an external worker service.

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/history/external-task-log/{id}/get.ftl" line="6">

---

# Retrieving External Task Log

This API endpoint is used to retrieve the details of a specific External Task Log entry by its ID.

```ftl
      tag = "Historic External Task Log"
      summary = "Get External Task Log"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/history/external-task-log/count/get.ftl" line="6">

---

# Counting External Task Logs

This API endpoint is used to get the count of External Task Log entries. This can be useful for pagination or to get a quick overview of the number of executed external tasks.

```ftl
      tag = "Historic External Task Log"
      summary = "Get External Task Log Count"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/history/external-task-log/{id}/error-details/get.ftl" line="6">

---

# Retrieving Error Details

This API endpoint is used to fetch the error details associated with a specific External Task Log entry. This can be useful for debugging and error handling.

```ftl
      tag = "Historic External Task Log"
      summary = "Get External Task Log Error Details"
```

---

</SwmSnippet>

# External Task Log Functions

The External Task Log functions are primarily used for logging and querying the history of external tasks.

<SwmSnippet path="/engine-rest/engine-rest/src/main/java/org/camunda/bpm/engine/rest/dto/history/HistoricExternalTaskLogDto.java" line="1">

---

## HistoricExternalTaskLogDto

The `HistoricExternalTaskLogDto` function is a Data Transfer Object (DTO) that carries data between processes. In the context of the External Task Log, it is used to transfer data related to the history of external tasks.

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

import org.camunda.bpm.engine.history.HistoricExternalTaskLog;

import java.util.Date;
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest/src/main/java/org/camunda/bpm/engine/rest/dto/history/HistoricExternalTaskLogQueryDto.java" line="1">

---

## HistoricExternalTaskLogQueryDto

The `HistoricExternalTaskLogQueryDto` function is used to create queries for the historic external task log. It allows for the retrieval of specific logs based on certain criteria.

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

import com.fasterxml.jackson.databind.ObjectMapper;
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest/src/main/java/org/camunda/bpm/engine/rest/history/HistoricExternalTaskLogRestService.java" line="1">

---

## HistoricExternalTaskLogRestService

The `HistoricExternalTaskLogRestService` function provides a RESTful interface for interacting with the historic external task log. It allows for the creation, retrieval, and manipulation of logs via HTTP requests.

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

import org.camunda.bpm.engine.rest.dto.CountResultDto;
import org.camunda.bpm.engine.rest.dto.history.HistoricExternalTaskLogDto;
import org.camunda.bpm.engine.rest.dto.history.HistoricExternalTaskLogQueryDto;
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest/src/main/java/org/camunda/bpm/engine/rest/sub/history/HistoricExternalTaskLogResource.java" line="1">

---

## HistoricExternalTaskLogResource

The `HistoricExternalTaskLogResource` function provides a resource-based interface for interacting with the historic external task log. It allows for the manipulation of individual log entries.

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
package org.camunda.bpm.engine.rest.sub.history;

import org.camunda.bpm.engine.rest.dto.history.HistoricExternalTaskLogDto;

import javax.ws.rs.GET;
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
