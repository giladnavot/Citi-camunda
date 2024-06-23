---
title: Overview of User
---
In Citi-camunda, 'User' refers to an entity that interacts with the system. Users have unique identifiers and can perform various actions such as creating, updating, and deleting their profiles. They can also unlock their accounts. The system provides methods for retrieving user information and counting the total number of users.

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/user/create/post.ftl" line="6">

---

# User Operations

This file is tagged with 'User', indicating that it contains operations for creating a new user.

```ftl
      tag = "User"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/user/{id}/profile/put.ftl" line="6">

---

This file is also tagged with 'User'. It contains operations for updating a user's profile.

```ftl
      tag = "User"
      summary = "Update User Profile"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/user/{id}/unlock/post.ftl" line="6">

---

This file, tagged with 'User', contains operations for unlocking a user.

```ftl
      tag = "User"
      summary = "Unlock User"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/user/{id}/delete.ftl" line="6">

---

This file is tagged with 'User' and contains operations for deleting a user.

```ftl
      tag = "User"
```

---

</SwmSnippet>

# User Functions

This section discusses the functions related to the User entity in the Citi-camunda project.

<SwmSnippet path="/webapps/frontend/camunda-bpm-sdk-js/lib/api-client/resources/user.js" line="1">

---

## User Functions in user.js

The user.js file contains functions that interact with the User entity. These functions are used to perform various operations such as creating, updating, deleting, and fetching User data.

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

## User Functions in users.js

The users.js file contains functions that are used to manage the User entities on the dashboard. These functions are used to display, sort, filter, and paginate User data on the dashboard.

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
