---
title: Understanding Batch Operations
---
Batch in Citi-camunda refers to a set of operations that are executed as a group. It is a concept used in the Camunda Platform to handle large volumes of process instances, tasks, or decisions. Batches are created, managed, and executed through the Batch interface in the engine. They provide functionalities such as retrieving a batch by id, suspending a batch, and deleting a batch. Additionally, they offer methods to get batch statistics and count.

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/batch/{id}/get.ftl" line="6">

---

# Batch Operations

This is an example of a batch operation. The batch ID is used to retrieve the status of the batch.

```ftl
      tag = "Batch"
      summary = "Get"
      desc = "Retrieves a batch by id, according to the Batch interface in the engine." />
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/batch/statistics/get.ftl" line="6">

---

# Batch Statistics

Batch statistics provide an overview of the progress of all batch operations. This can be used to monitor the overall performance of batch processing.

```ftl
      tag = "Batch"
      summary = "Get Statistics"
      desc = "Queries for batch statistics that fulfill given parameters.
              Parameters may be the properties of batches, such as the id or type.
              The size of the result set can be retrieved by using the 
              [Get Batch Statistics Count](${docsUrl}/reference/rest/batch/get-statistics-query-count/) method." />
```

---

</SwmSnippet>

# Batch Functionality

Batch functionality in Citi-camunda is a crucial part of the process automation. It allows for execution of a series of jobs in a controlled manner.

<SwmSnippet path="/engine-rest/engine-rest/src/main/java/org/camunda/bpm/engine/rest/dto/batch/BatchDto.java" line="1">

---

## BatchDto

BatchDto is a Data Transfer Object that carries data between processes. It's used to encapsulate batch data as it's moved around.

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
package org.camunda.bpm.engine.rest.dto.batch;

import org.camunda.bpm.engine.batch.Batch;

import java.util.Date;
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/batch/Batch.java" line="1">

---

## Batch

Batch is the main class that represents a batch process. It contains methods for managing and controlling the batch process.

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
package org.camunda.bpm.engine.batch;

import org.camunda.bpm.engine.ManagementService;

import java.util.Date;
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/batch/BatchQuery.java" line="1">

---

## BatchQuery

BatchQuery is used to programmatically create queries to retrieve batches. It provides a fluent API to specify search criteria.

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
package org.camunda.bpm.engine.batch;

import org.camunda.bpm.engine.query.Query;

/**
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/batch/history/HistoricBatch.java" line="1">

---

## HistoricBatch

HistoricBatch represents a batch process that has completed. It provides methods to retrieve information about the batch process after it has finished.

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
package org.camunda.bpm.engine.batch.history;

import java.util.Date;

/**
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
