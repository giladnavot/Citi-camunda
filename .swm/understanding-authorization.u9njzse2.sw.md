---
title: Understanding Authorization
---
Authorization in the Citi-camunda project refers to the process of granting or denying access to specific resources within the application. It is a security measure that ensures only authenticated users with the appropriate permissions can access certain resources or perform certain actions.

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/authorization/{id}/get.ftl" line="1">

---

## Authorization API Endpoints

This file is a template for the GET endpoint for an authorization. It is used to retrieve the details of a specific authorization.

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

This file is a template for the PUT endpoint for an authorization. It is used to update the details of a specific authorization.

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

This file is a template for the DELETE endpoint for an authorization. It is used to delete a specific authorization.

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

This file is a template for the GET endpoint for checking authorization. It is used to check if a user is authorized to perform a certain action.

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

Let's delve into the key functions of Authorization in Citi-camunda.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/authorization/Authorization.java" line="1">

---

## Authorization.java

This Java class defines the core Authorization object in the Camunda engine. It likely includes methods for creating, updating, and deleting authorizations.

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

This Java class is part of the Spring Boot starter for Camunda. It likely defines properties related to authorization that can be configured in the application's properties file.

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

This JavaScript file is part of the Camunda SDK. It likely defines functions for interacting with the Authorization API.

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

This JavaScript file is part of the admin UI. It likely defines functions for rendering the authorizations page and handling user interactions.

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

## FreeMarker Templates

The FreeMarker templates define the REST API endpoints for authorization. They include endpoints for getting, updating, and deleting an authorization by ID, checking an authorization, counting authorizations, and creating an authorization.

# Authorization Check Endpoint

Authorization Endpoint

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/authorization/check/get.ftl" line="1">

---

## isUserAuthorized Endpoint

The `isUserAuthorized` endpoint is used to perform an authorization check for the currently authenticated user. It requires parameters such as `permissionName`, `resourceName`, `resourceType`, and optionally `resourceId` and `userId`. The endpoint returns a response indicating whether the user is authorized or not, along with potential error codes and their meanings.

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

      <@lib.parameter
          name = "permissionName"
          location = "query"
          type = "string"
          required = true
          desc = "String value representing the permission name to check for."
      />

      <@lib.parameter
          name = "resourceName"
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
