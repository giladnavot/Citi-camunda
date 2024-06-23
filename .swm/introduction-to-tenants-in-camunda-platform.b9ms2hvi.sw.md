---
title: Introduction to Tenants in Camunda Platform
---
A Tenant in the context of the Citi-camunda repository refers to a logical grouping of processes, cases, and tasks in the Camunda Platform. It is used to segregate data and configuration within the same Camunda installation. This is particularly useful in multi-tenant applications where you want to ensure data isolation between different tenants. The Tenant concept is implemented in various parts of the codebase, including REST API endpoints for creating, retrieving, updating, and deleting tenants.

# Tenant Isolation

This is the TenantEntity class, which represents a tenant in the system. It contains methods for setting and getting the tenant id, which is used to segregate data for different tenants.

# Starting a Process Instance with a Tenant

This is the StartProcessInstanceCmd class, which is used to start a new process instance. Notice the use of the tenant id in the startProcessInstanceByMessageAndTenantId method. This tenant id is used to segregate the process instance data for different tenants.

# Tenant Functionality

Tenant Functionality

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/identity/Tenant.java" line="1">

---

## Tenant.java

The 'Tenant.java' file contains the main implementation of the Tenant functionality. It defines the Tenant class, which represents a tenant in the system. The class includes methods for getting and setting tenant properties such as ID, name, and email.

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

The 'tenant.js' file is part of the frontend and interacts with the backend to perform operations related to tenants. It includes functions for creating, updating, deleting, and retrieving tenants.

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
