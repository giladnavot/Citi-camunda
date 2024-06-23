---
title: Exploring the Tenant Concept
---
In Citi-camunda, a Tenant refers to an entity that is used to segregate processes, cases, and related data within the Camunda Platform. It is a way to partition data into isolated units. Tenants are used to create, update, retrieve, and delete operations. They also have user and group memberships, which can be managed separately.

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/tenant/create/post.ftl" line="6">

---

# Tenant Management

This is where a new tenant is created. The 'name' field represents the name of the tenant.

```ftl
      tag = "Tenant"
      summary = "Create Tenant"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/tenant/get.ftl" line="6">

---

# Tenant Retrieval

This is where tenants are retrieved. The API endpoint allows for fetching tenant information.

```ftl
      tag = "Tenant"
      summary = "Get Tenants"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/tenant/{id}/delete.ftl" line="6">

---

# Tenant Deletion

This is where a tenant is deleted. The API endpoint allows for the removal of a tenant from the system.

```ftl
      tag = "Tenant"
      summary = "Delete Tenant"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/tenant/{id}/put.ftl" line="6">

---

# Tenant Update

This is where a tenant is updated. The API endpoint allows for modifying the details of an existing tenant.

```ftl
      tag = "Tenant"
      summary = "Update Tenant"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/tenant/{id}/user-members/{userId}/put.ftl" line="6">

---

# Tenant Membership Management

This is where tenant memberships are managed. The API endpoint allows for adding and removing users from a tenant.

```ftl
      tag = "Tenant"
      summary = "Create Tenant User Membership"
```

---

</SwmSnippet>

# Tenant Functionality

Tenant Functionality

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/identity/Tenant.java" line="1">

---

## Tenant.java

The Tenant.java file is a part of the identity management system in the Camunda BPM engine. It defines the Tenant class, which represents a tenant in the system. A tenant is a group of users that share the same resources in the system. The Tenant class provides methods for managing the tenant's ID, name, and other properties.

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
package org.camunda.bpm.engine.identity;

import java.io.Serializable;

import org.camunda.bpm.engine.IdentityService;
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/camunda-bpm-sdk-js/lib/api-client/resources/tenant.js" line="1">

---

## tenant.js

The tenant.js file is part of the Camunda BPM SDK. It provides a JavaScript API for interacting with tenants in the Camunda BPM engine. The API includes methods for creating, updating, deleting, and querying tenants.

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
var utils = require('../../utils');
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
