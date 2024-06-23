---
title: Introduction to Process Definition
---
A Process Definition in Camunda is a BPMN 2.0 process that has been deployed to the engine. It is a blueprint for creating process instances, which are individual executions of the process. Process Definitions are stored in the engine's database and can be managed through the engine's REST API.

The Process Definition is identified by an ID, which is used in various operations such as starting a process instance, retrieving process variables, or suspending and activating a process. The ID is unique to each version of the process definition.

The Process Definition also includes information about the process's tasks, events, gateways, and other BPMN elements. This information is used by the engine to execute the process.

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/process-definition/{id}/static-called-process-definitions/get.ftl" line="1">

---

# Process Definition API

This file defines a GET endpoint for retrieving the static called process definitions for a given process definition. This is an example of how Process Definitions are used in the Camunda Platform's REST API.

```ftl
<#-- Generated From File: camunda-docs-manual/public/reference/rest/process-definition/get-static-called-process-definitions/index.html -->
<#macro endpoint_macro docsUrl="">
{
  <@lib.endpointInfo
      id = "getStaticCalledProcessDefinitions"
      tag = "Process Definition"
      summary = "Get Static Called Process Definitions"
      desc = "For the given process, returns a list of called process definitions corresponding
              to
              the `CalledProcessDefinition` interface in the engine. The list
              contains all process definitions
              that are referenced statically by call activities in the given
              process. This endpoint does not
              resolve process definitions that are referenced with expressions. Each
              called process definition
              contains a list of call activity ids, which specifies the call
              activities that are calling that
              process. This endpoint does not resolve references to case
              definitions."
  />
```

---

</SwmSnippet>

# Functions of Process Definition

The Process Definition in Camunda Platform 7 is a crucial part of the workflow and process automation. It is implemented in various parts of the codebase, including the engine and webapps directories.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/history/HistoricActivityInstance.java" line="1">

---

## HistoricActivityInstance

The `HistoricActivityInstance` function is part of the Process Definition. It is used to track the historical activities of a process instance.

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

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/history/HistoricDetail.java" line="1">

---

## HistoricDetail

The `HistoricDetail` function is another part of the Process Definition. It is used to provide detailed historical data about a process instance.

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


```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/history/HistoricTaskInstance.java" line="1">

---

## HistoricTaskInstance

The `HistoricTaskInstance` function is used to track the historical tasks of a process instance. It is a part of the Process Definition.

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


```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/el/ExpressionManager.java" line="1">

---

## ExpressionManager

The `ExpressionManager` function is used to manage expressions within a process definition. It is a part of the Process Definition.

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
package org.camunda.bpm.engine.impl.el;

import java.lang.reflect.Method;

/**
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/management/ProcessDefinitionStatistics.java" line="1">

---

## ProcessDefinitionStatistics

The `ProcessDefinitionStatistics` function is used to provide statistical data about a process definition. It is a part of the Process Definition.

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
package org.camunda.bpm.engine.management;

import java.util.List;

import org.camunda.bpm.engine.repository.ProcessDefinition;
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/CalledProcessDefinition.java" line="1">

---

## CalledProcessDefinition

The `CalledProcessDefinition` function is used to manage the process definitions that are called by a process instance. It is a part of the Process Definition.

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
package org.camunda.bpm.engine.repository;

import java.util.List;

public interface CalledProcessDefinition extends ProcessDefinition {
```

---

</SwmSnippet>

# Process Definition Endpoints

Understanding Process Definition Endpoints

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/process-definition/{id}/static-called-process-definitions/get.ftl" line="1">

---

## Get Static Called Process Definitions

This endpoint retrieves a list of process definitions that are statically called by the given process. It does not resolve process definitions that are referenced with expressions. The response includes details about each called process definition, such as its id, key, version, and the ids of the call activities that are calling that process.

```ftl
<#-- Generated From File: camunda-docs-manual/public/reference/rest/process-definition/get-static-called-process-definitions/index.html -->
<#macro endpoint_macro docsUrl="">
{
  <@lib.endpointInfo
      id = "getStaticCalledProcessDefinitions"
      tag = "Process Definition"
      summary = "Get Static Called Process Definitions"
      desc = "For the given process, returns a list of called process definitions corresponding
              to
              the `CalledProcessDefinition` interface in the engine. The list
              contains all process definitions
              that are referenced statically by call activities in the given
              process. This endpoint does not
              resolve process definitions that are referenced with expressions. Each
              called process definition
              contains a list of call activity ids, which specifies the call
              activities that are calling that
              process. This endpoint does not resolve references to case
              definitions."
  />

```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/process-definition/{id}/diagram/get.ftl" line="1">

---

## Get Process Definition Diagram

This endpoint retrieves the diagram of a process definition. If the process definition's deployment contains an image resource with the same file name as the process definition, the deployed image will be returned. Supported file extensions for the image are: `svg`, `png`, `jpg`, and `gif`.

```ftl
<#macro endpoint_macro docsUrl="">
{

  <@lib.endpointInfo
      id = "getProcessDefinitionDiagram"
      tag = "Process Definition"
      summary = "Get Diagram"
      desc = "Retrieves the diagram of a process definition.

              If the process definition's deployment contains an image resource with the same file name
              as the process definition, the deployed image will be returned by the Get Diagram endpoint.
              Example: `someProcess.bpmn` and `someProcess.png`.
              Supported file extentions for the image are: `svg`, `png`, `jpg`, and `gif`." />

  "parameters" : [

    <@lib.parameter
        name = "id"
        location = "path"
        type = "string"
        required = true
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
