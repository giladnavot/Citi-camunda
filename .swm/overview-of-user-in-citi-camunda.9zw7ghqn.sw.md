---
title: Overview of User in Citi-camunda
---
In Citi-camunda, a User refers to an entity that interacts with the system. Users can perform various actions such as creating, updating, and deleting their profiles. They can also manage their credentials and unlock their accounts. The system provides RESTful APIs to facilitate these operations.

# User Creation

This is where a new user is created in the system. The `createUserQuery` method is used to create a new user.

# User Interaction

This is where a user interacts with the system. The `createTaskQuery` method is used by a user to create a new task.

# User Functions

User Functions Overview

<SwmSnippet path="/webapps/frontend/camunda-bpm-sdk-js/lib/api-client/resources/user.js" line="1">

---

## User.js Functions

The user.js file contains functions that handle operations related to individual users. These functions include creating, updating, deleting, and retrieving user information.

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

var Q = require('q');
var AbstractClientResource = require('./../abstract-client-resource');
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/plugins/base/app/views/dashboard/users.js" line="1">

---

## Users.js Functions

The users.js file contains functions that manage user-related operations on a broader scale. These functions include listing all users, searching for users, and managing user roles and permissions.

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

var template = require('./users.html?raw');

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
