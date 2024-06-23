---
title: Understanding Activity Instance
---
An Activity Instance in the context of the Citi-camunda repository refers to a specific execution of an activity within a process. It is a historical record of the activity's execution, capturing details such as the start time, end time, and duration. This information is crucial for process analysis and optimization. The Activity Instance is part of the Camunda Platform's history service, which provides detailed information about the execution of processes and activities.

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/history/activity-instance/{id}/get.ftl" line="6">

---

# Historic Activity Instance

This is an example of an API endpoint that retrieves a specific Historic Activity Instance by its ID.

```ftl
      tag = "Historic Activity Instance"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/history/activity-instance/count/get.ftl" line="5">

---

# Count of Historic Activity Instances

This API endpoint retrieves the count of Historic Activity Instances. It takes the same parameters as the Get Historic Activity Instance method.

```ftl
      tag = "Historic Activity Instance"
      summary = "Get List Count"
      desc = "Queries for the number of historic activity instances that fulfill the given parameters.
              Takes the same parameters as the [Get Historic Activity Instance](${docsUrl}/reference/rest/history/activity-instance/get-activity-instance-query/)  method." />
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/history/activity-instance/get.ftl" line="5">

---

# Query for Historic Activity Instances

This API endpoint allows you to query for Historic Activity Instances. It provides a link to the Get Historic Activity Instance Count method for convenience.

```ftl
      tag = "Historic Activity Instance"
      summary = "Get List"
      desc = "Queries for historic activity instances that fulfill the given parameters.
              The size of the result set can be retrieved by using the
              [Get Historic Activity Instance Count](${docsUrl}/reference/rest/history/activity-instance/get-activity-instance-query-count/) method." />
```

---

</SwmSnippet>

# Functions of Activity Instance

This section provides an overview of the main functions of Activity Instance in Camunda Platform 7.

<SwmSnippet path="/engine-rest/engine-rest/src/main/java/org/camunda/bpm/engine/rest/dto/runtime/ActivityInstanceDto.java" line="1">

---

## ActivityInstanceDto

The `ActivityInstanceDto` is a Data Transfer Object that carries data between processes. It is used to encapsulate the state of an Activity Instance, including its ID, parent activity instance ID, child activity instance IDs, and other related information.

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

The `HistoricActivityInstance` function provides historical data about an Activity Instance. It includes information such as the start time, end time, duration, and whether the activity was completed or cancelled.

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

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/persistence/entity/ActivityInstanceImpl.java" line="1">

---

## ActivityInstanceImpl

The `ActivityInstanceImpl` function is an implementation of the Activity Instance. It provides the functionality for managing the state of an Activity Instance, including starting, stopping, and transitioning between states.

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
package org.camunda.bpm.engine.impl.persistence.entity;

import java.io.StringWriter;
import java.util.ArrayList;
import java.util.List;
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/runtime/ActivityInstance.java" line="1">

---

## ActivityInstance

The `ActivityInstance` function is the main interface for interacting with an Activity Instance. It provides methods for retrieving the current state of the instance, as well as for manipulating the instance, such as triggering transitions or completing the activity.

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

import org.camunda.bpm.engine.RuntimeService;

/**
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
