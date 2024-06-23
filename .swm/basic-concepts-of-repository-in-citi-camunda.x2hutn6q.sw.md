---
title: Basic Concepts of Repository in Citi-camunda
---
A repository in the Citi-camunda project refers to a specific directory structure that contains scripts, configurations, and resources for a particular aspect of the application. For instance, the 'repository' directory in the 'webapps/frontend/ui/cockpit/client/scripts/' path contains scripts for managing and interacting with the repository data. This includes directives, controllers, and route configurations.

The 'repositoryData' property found in 'cam-cockpit-resources.js' is a key part of the repository's functionality. It's used to bind data to the scope of the directive, allowing it to be accessed and manipulated within the directive's context.

The 'camCockpitRepositoryViewCtrl' controller, defined in 'routes.js', is associated with the '/repository' route. This controller is responsible for handling the logic and data manipulation when the '/repository' route is accessed in the application.

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/repository/resources/directives/cam-cockpit-resources.js" line="29">

---

# Repository Usage

In this code snippet, 'repositoryData' is a property of the scope object. This property is assigned a value using the '=' operator, which means that it will be bound to a corresponding property in the parent scope. This allows 'repositoryData' to be used as a repository for storing and managing data.

```javascript
      restrict: 'A',
      scope: {
        repositoryData: '='
      },
```

---

</SwmSnippet>

# Repository Functions

The Repository in Citi-camunda is a crucial part of the system, handling the storage and management of process definitions, deployments, and decisions. It is implemented in several parts of the codebase, both on the backend and the frontend.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/RepositoryService.java" line="0">

---

## RepositoryService

The `RepositoryService` is a service provided by the process engine. It allows for the deployment of BPMN 2.0, CMMN 1.1 and DMN 1.1. It also provides methods for querying deployed process definitions, deployments and decisions.

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
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/identity/ReadOnlyIdentityProvider.java" line="0">

---

## ReadOnlyIdentityProvider

The `ReadOnlyIdentityProvider` is an interface that provides read-only access to the identity service. It is used to fetch user and group information without the ability to make changes.

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
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/persistence/entity/TableDataManager.java" line="0">

---

## TableDataManager

The `TableDataManager` is responsible for managing the data in the tables of the database. It provides methods for querying and manipulating the data.

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
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/repository/resources/main.js" line="0">

---

## Frontend Repository

The frontend repository is responsible for displaying the repository data in the user interface. It uses directives to manage the data and controllers to handle user interactions.

```javascript
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
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
