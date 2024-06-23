---
title: Overview of Batch Operations
---
Batch in Citi-camunda refers to a set of operations that are executed as a group. These operations are typically related and are executed together to improve performance and efficiency. Batches are used in various parts of the application, such as process execution, task management, and process operations.

# Batch Processing

This is the BatchEntity class, which represents a batch process in Citi-camunda. It contains methods for setting and getting batch properties, such as the batch type, total jobs, batch configuration, etc. These properties are used to define and control the execution of the batch process.

# Batch Execution

This is the BatchExecutionJobHandler class, which is responsible for executing batch jobs. It contains methods for executing the batch job, handling failures, and managing retries. This class is a key component of the batch processing functionality in Citi-camunda.

# Batch Functionality

This section will cover the main functions of Batch in the Citi-camunda project.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/batch/Batch.java" line="1">

---

## Batch

The `Batch` class is a central part of the batch processing functionality. It represents a batch of operations that are executed together.

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

<SwmSnippet path="/engine-rest/engine-rest/src/main/java/org/camunda/bpm/engine/rest/dto/batch/BatchDto.java" line="1">

---

## BatchDto

`BatchDto` is a Data Transfer Object that carries data between processes. In the context of batch processing, it is used to transfer data related to a batch.

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

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/batch/BatchQuery.java" line="1">

---

## BatchQuery

`BatchQuery` is used to programmatically create queries to retrieve batches. It provides methods to filter and sort the results.

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

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
