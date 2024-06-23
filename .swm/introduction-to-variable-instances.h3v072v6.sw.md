---
title: Introduction to Variable Instances
---
A Variable Instance in Camunda refers to a specific instance of a variable that is created during the execution of a process. It holds the value of a variable at a particular point in time and is associated with a specific execution or task within the process.

Variable Instances are used to store and manage data within a process. They can be created, updated, and deleted as the process progresses, allowing for dynamic data handling.

The Variable Instance API in the engine-rest module provides endpoints for managing Variable Instances. This includes retrieving a Variable Instance by its ID, getting the binary data of a Variable Instance, and counting the number of Variable Instances.

# Variable Instance Creation

This file contains the implementation of a Variable Instance. It shows how a Variable Instance is created and how its value can be set and retrieved.

# Variable Instance Usage

This file demonstrates how Variable Instances are used within a service task. It shows how the process retrieves the value of a Variable Instance and uses it to control the flow of the process.

# Variable Instance Functions

Let's delve into the functions of Variable Instance.

<SwmSnippet path="/engine-rest/engine-rest/src/main/java/org/camunda/bpm/engine/rest/dto/runtime/VariableInstanceDto.java" line="1">

---

## VariableInstanceDto

The `VariableInstanceDto` is a Data Transfer Object that carries data between processes. It is used to encapsulate variable instance data for transmission over the network.

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

import org.camunda.bpm.engine.rest.dto.VariableValueDto;
import org.camunda.bpm.engine.runtime.VariableInstance;

```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest/src/main/java/org/camunda/bpm/engine/rest/sub/runtime/VariableInstanceResource.java" line="1">

---

## VariableInstanceResource

The `VariableInstanceResource` is a REST resource that provides access to variable instance data. It allows for the retrieval, modification, and deletion of variable instances.

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
package org.camunda.bpm.engine.rest.sub.runtime;

import javax.ws.rs.DefaultValue;
import javax.ws.rs.GET;
import javax.ws.rs.Path;
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/history/HistoricVariableInstance.java" line="1">

---

## HistoricVariableInstance

The `HistoricVariableInstance` is used to access the history of variable instances. It provides information about the state of a variable at a specific point in time.

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

import org.camunda.bpm.engine.variable.value.TypedValue;
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
