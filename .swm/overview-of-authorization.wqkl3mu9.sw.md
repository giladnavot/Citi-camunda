---
title: Overview of Authorization
---
Authorization in Citi-camunda refers to the process of granting or denying access to specific resources in the application. It is a security measure that ensures that users can only access the resources they are permitted to use. This is achieved through the use of authorization checks, which are implemented in various parts of the application.

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/authorization/{id}/get.ftl" line="1">

---

## Authorization API Endpoints

This file defines the GET endpoint for retrieving an authorization record by its ID.

```ftl
<#macro endpoint_macro docsUrl="">
{
  <@lib.endpointInfo
      id = "getAuthorization"
      tag = "Authorization"
      summary = "Get Authorization"
      desc = "Retrieves an authorization by id."
  />

  "parameters" : [
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/authorization/{id}/put.ftl" line="1">

---

This file defines the PUT endpoint for updating an authorization record by its ID.

```ftl
<#macro endpoint_macro docsUrl="">
{
  <@lib.endpointInfo
      id = "updateAuthorization"
      tag = "Authorization"
      summary = "Update an Authorization"
      desc = "Updates an authorization by id."
  />

  "parameters" : [
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/authorization/{id}/delete.ftl" line="1">

---

This file defines the DELETE endpoint for removing an authorization record by its ID.

```ftl
<#macro endpoint_macro docsUrl="">
{
  <@lib.endpointInfo
      id = "deleteAuthorization"
      tag = "Authorization"
      summary = "Delete Authorization"
      desc = "Deletes an authorization by id."
  />

  "parameters" : [
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/authorization/check/get.ftl" line="1">

---

## Authorization Check Endpoint

This file defines the GET endpoint for checking the authorization status of a user.

```ftl
<#macro endpoint_macro docsUrl="">
{
  <@lib.endpointInfo
      id = "isUserAuthorized"
      tag = "Authorization"
      summary = "Perform an Authorization Check"
      desc = "Performs an authorization check for the currently authenticated user."
  />

  "parameters" : [
```

---

</SwmSnippet>

# Authorization Functions

This section discusses the main functions related to authorization in Citi-camunda.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/authorization/Authorization.java" line="1">

---

## Authorization.java

This Java class defines the core authorization model in the engine. It includes methods for managing permissions and roles.

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
package org.camunda.bpm.engine.authorization;

import org.camunda.bpm.engine.identity.Group;
import org.camunda.bpm.engine.identity.User;

```

---

</SwmSnippet>

<SwmSnippet path="/spring-boot-starter/starter/src/main/java/org/camunda/bpm/spring/boot/starter/property/AuthorizationProperty.java" line="1">

---

## AuthorizationProperty.java

This Java class is used for configuring authorization properties in the Spring Boot starter.

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
package org.camunda.bpm.spring.boot.starter.property;

import static org.camunda.bpm.spring.boot.starter.property.CamundaBpmProperties.joinOn;

public class AuthorizationProperty {
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/camunda-bpm-sdk-js/lib/api-client/resources/authorization.js" line="1">

---

## authorization.js

This JavaScript file provides client-side functions for interacting with the authorization API.

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
 */

'use strict';

var AbstractClientResource = require('./../abstract-client-resource');

```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/client/scripts/pages/authorizations.js" line="1">

---

## authorizations.js

This JavaScript file handles the UI for managing authorizations in the admin interface.

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
 */

'use strict';

var template = require('./authorizations.html?raw');
var confirmTemplate = require('./confirm-delete-authorization.html?raw');
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
