---
title: Basic Concepts of Deployment in Citi-camunda
---
Deployment in Citi-camunda refers to the process of moving the developed workflow or process automation from a development environment to a production environment. It involves the creation, registration, and management of deployments. This is facilitated through various REST API endpoints, each serving a specific function such as creating a new deployment, retrieving information about registered deployments, deleting a deployment, redeploying a deployment, and managing deployment resources.

# Deployment Process

This section of the code in `DeploymentManager.java` handles the creation of the process archive (PAR) and its deployment to the Camunda engine. It uses the `RepositoryService` to create a deployment, add resources to it, and then deploy it.

# Deployment Verification

After deployment, it's important to verify that the deployment was successful. This section of the code in `DeploymentManager.java` retrieves the deployed process definitions from the Camunda engine using the `RepositoryService` and checks if the expected process definitions are present.

# Functions of Deployment

Let's delve into the functions of Deployment in the Citi-camunda project.

<SwmSnippet path="/engine-rest/engine-rest/src/main/java/org/camunda/bpm/engine/rest/dto/repository/DeploymentWithDefinitionsDto.java" line="1">

---

## DeploymentWithDefinitionsDto

The `DeploymentWithDefinitionsDto` function is a Data Transfer Object that carries deployment data along with definitions between processes.

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

The `DeploymentOperation` function is responsible for the operation of deployment, managing the process of deploying the workflow and process automation.

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

The `Deployment` function is the core function for deployment, handling the deployment of the process automation and workflow.

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

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
