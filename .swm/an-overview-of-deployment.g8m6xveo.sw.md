---
title: An Overview of Deployment
---
Deployment in Citi-camunda refers to the process of moving the developed workflow or process automation from a development environment to a production environment. It involves creating, registering, and managing deployments. Each deployment is identified by a unique id and can contain multiple resources. The deployment process also includes error handling for scenarios where a deployment or a deployment resource does not exist.

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/deployment/create/post.ftl" line="5">

---

## Creating a Deployment

This file defines the API endpoint for creating a new deployment. The endpoint is tagged with 'Deployment', indicating its purpose. The message at line 91 provides a cautionary note about using a cancelling boundary timer event with a time cycle in the deployment.

```ftl
      tag = "Deployment"
      summary = "Create"
      desc = "Creates a deployment.

              **Security Consideration**

              Deployments can contain custom code in form of scripts or EL expressions to customize process behavior.
              This may be abused for remote execution of arbitrary code." />

  <@lib.requestBody
      mediaType = "multipart/form-data"
      dto = "MultiFormDeploymentDto" />

  "responses": {

    <@lib.response
        code = "200"
        dto = "DeploymentWithDefinitionsDto"
        desc = "Request successful."
        examples = ['"example-1": {
                     "summary": "POST `/deployment/create`",
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/deployment/{id}/get.ftl" line="6">

---

## Retrieving a Deployment

This file defines the API endpoint for retrieving a deployment by its ID. The endpoint is tagged with 'Deployment', indicating its purpose. If a deployment with the provided ID does not exist, an error message is returned.

```ftl
      tag = "Deployment"
      summary = "Get"
      desc = "Retrieves a deployment by id, according to the `Deployment` interface of the engine." />

  "parameters" : [

    <@lib.parameter
        name = "id"
        location = "path"
        type = "string"
        required = true
        last = true
        desc = "The id of the deployment." />

  ],

  "responses" : {

    <@lib.response
        code = "200"
        dto = "DeploymentDto"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/deployment/{id}/redeploy/post.ftl" line="6">

---

## Redeploying a Deployment

This file defines the API endpoint for redeploying a deployment. The endpoint is tagged with 'Deployment', indicating its purpose. If a deployment or a deployment resource for the given deployment does not exist, an error message is returned.

```ftl
      tag = "Deployment"
      summary = "Redeploy"
      desc = "Re-deploys an existing deployment.

              The deployment resources to re-deploy can be restricted by using the properties `resourceIds` or
              `resourceNames`. If no deployment resources to re-deploy are passed then all existing resources of the
              given deployment are re-deployed.

              **Warning**: Deployments can contain custom code in form of scripts or EL expressions to customize
              process behavior. This may be abused for remote execution of arbitrary code. See the section on
              [security considerations for custom code](${docsUrl}/user-guide/process-engine/securing-custom-code/) in
              the user guide for details." />

  "parameters" : [

    <@lib.parameter
        name = "id"
        location = "path"
        type = "string"
        required = true
        last = true
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/deployment/{id}/delete.ftl" line="6">

---

## Deleting a Deployment

This file defines the API endpoint for deleting a deployment by its ID. The endpoint is tagged with 'Deployment', indicating its purpose. If a deployment with the provided ID does not exist, an error message is returned.

```ftl
      tag = "Deployment"
      summary = "Delete"
      desc = "Deletes a deployment by id." />

  "parameters" : [

    <@lib.parameter
        name = "id"
        location = "path"
        type = "string"
        required = true
        desc = "The id of the deployment to be deleted." />

    <@lib.parameter
        name = "cascade"
        location = "query"
        type = "boolean"
        defaultValue = 'false'
        desc = "`true`, if all process instances, historic process instances and jobs for this deployment
                should be deleted." />

```

---

</SwmSnippet>

# Deployment Functions

The Deployment functions are a crucial part of the Citi-camunda repository. They are responsible for the deployment of process definitions and other related resources.

<SwmSnippet path="/engine-rest/engine-rest/src/main/java/org/camunda/bpm/engine/rest/dto/repository/DeploymentWithDefinitionsDto.java" line="1">

---

## DeploymentWithDefinitionsDto

The `DeploymentWithDefinitionsDto` function is a Data Transfer Object that carries deployment data along with the definitions associated with the deployment.

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
package org.camunda.bpm.engine.rest.dto.repository;

import org.camunda.bpm.engine.repository.*;

import java.util.HashMap;
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/container/impl/spi/DeploymentOperation.java" line="1">

---

## DeploymentOperation

The `DeploymentOperation` function is responsible for the actual deployment operation. It handles the process of deploying resources to the Camunda engine.

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
package org.camunda.bpm.container.impl.spi;

import org.camunda.bpm.container.impl.ContainerIntegrationLogger;
import org.camunda.bpm.engine.impl.ProcessEngineLogger;

```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/Deployment.java" line="1">

---

## Deployment

The `Deployment` function represents a deployment of resources. It contains information about the deployment such as the deployment id, name, deployment time, and source.

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

import java.util.Date;

/**
```

---

</SwmSnippet>

# Deployment Endpoints

Deployment Endpoints

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/deployment/create/post.ftl" line="1">

---

## Create Deployment Endpoint

The `createDeployment` endpoint is used to create a new deployment. It accepts a multipart/form-data request body and returns a `DeploymentWithDefinitionsDto` object upon successful creation. It also handles parse exceptions and returns a `ParseExceptionDto` object in case one of the bpmn resources cannot be parsed.

```ftl
<#macro endpoint_macro docsUrl="">
{
  <@lib.endpointInfo
      id = "createDeployment"
      tag = "Deployment"
      summary = "Create"
      desc = "Creates a deployment.

              **Security Consideration**

              Deployments can contain custom code in form of scripts or EL expressions to customize process behavior.
              This may be abused for remote execution of arbitrary code." />

  <@lib.requestBody
      mediaType = "multipart/form-data"
      dto = "MultiFormDeploymentDto" />

  "responses": {

    <@lib.response
        code = "200"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/deployment/{id}/redeploy/post.ftl" line="1">

---

## Redeploy Endpoint

The `redeploy` endpoint is used to redeploy an existing deployment. It accepts a JSON request body with `RedeploymentDto` object and returns a `DeploymentWithDefinitionsDto` object upon successful redeployment. It also handles exceptions when the deployment or a deployment resource for the given deployment does not exist.

```ftl
<#macro endpoint_macro docsUrl="">
{

  <@lib.endpointInfo
      id = "redeploy"
      tag = "Deployment"
      summary = "Redeploy"
      desc = "Re-deploys an existing deployment.

              The deployment resources to re-deploy can be restricted by using the properties `resourceIds` or
              `resourceNames`. If no deployment resources to re-deploy are passed then all existing resources of the
              given deployment are re-deployed.

              **Warning**: Deployments can contain custom code in form of scripts or EL expressions to customize
              process behavior. This may be abused for remote execution of arbitrary code. See the section on
              [security considerations for custom code](${docsUrl}/user-guide/process-engine/securing-custom-code/) in
              the user guide for details." />

  "parameters" : [

    <@lib.parameter
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
