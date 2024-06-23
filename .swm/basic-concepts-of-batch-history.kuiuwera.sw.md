---
title: Basic Concepts of Batch History
---
Batch History in Citi-camunda refers to the historical data of batch operations. It provides functionalities such as retrieving the count of cleanable batch reports, getting a cleanable batch report, setting the removal time for a batch, deleting a historic batch, and getting a historic batch or its count. These operations are crucial for managing and maintaining the process engine's history.

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/history/batch/get.ftl" line="6">

---

# Historic Batch Management

This is where the 'Get Historic Batch' endpoint is defined. It is used to retrieve a specific historic batch.

```ftl
      tag = "Historic Batch"
      summary = "Get Historic Batches"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/history/batch/{id}/delete.ftl" line="6">

---

# Historic Batch Deletion

This is where the 'Delete Historic Batch' endpoint is defined. It is used to delete a specific historic batch.

```ftl
      tag = "Historic Batch"
      summary = "Delete Historic Batch"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/history/batch/set-removal-time/post.ftl" line="6">

---

# Setting Batch Removal Time

This is where the 'Set Removal Time' endpoint is defined. It is used to set the removal time for a batch.

```ftl
      tag = "Historic Batch"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/history/batch/cleanable-batch-report/get.ftl" line="6">

---

# History Cleanup

This is where the 'Get Cleanable Batch Report' endpoint is defined. It is part of the history cleanup process.

```ftl
      tag = "Historic Batch"
      summary = "Get Cleanable Batch Report"
```

---

</SwmSnippet>

# Batch History Functions

Batch History Functions

<SwmSnippet path="/engine-rest/engine-rest/src/main/java/org/camunda/bpm/engine/rest/dto/history/batch/HistoricBatchDto.java" line="1">

---

## HistoricBatchDto

The `HistoricBatchDto` class is a Data Transfer Object that carries batch history data between processes. It encapsulates the batch history data and provides methods for accessing this data.

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
package org.camunda.bpm.engine.rest.dto.history.batch;

import java.util.Date;

import org.camunda.bpm.engine.batch.history.HistoricBatch;
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/batch/Batch.java" line="1">

---

## Batch

The `Batch` class represents a batch operation in the system. It provides methods for managing and manipulating batches.

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

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/batch/history/HistoricBatch.java" line="1">

---

## HistoricBatch

The `HistoricBatch` class represents the historical data of a batch operation. It provides methods for accessing the historical data of a batch.

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
