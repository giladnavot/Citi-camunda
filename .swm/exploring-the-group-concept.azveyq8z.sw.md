---
title: Exploring the Group Concept
---
In Citi-camunda, a Group refers to a collection of users that share certain attributes or permissions within the system. It is a key concept in managing access control and permissions. Groups can be created, updated, and deleted. Additionally, users can be added to or removed from groups, and various operations can be performed on the group resource itself.

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/group/create/post.ftl" line="6">

---

# Creating a Group

This is where a new group is created. The 'Create Group' endpoint is used for this purpose.

```ftl
      tag = "Group"
      summary = "Create Group"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/group/{id}/put.ftl" line="6">

---

# Updating a Group

The 'Update Group' endpoint is used to modify the details of an existing group.

```ftl
      tag = "Group"
      summary = "Update Group"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/group/{id}/delete.ftl" line="6">

---

# Deleting a Group

The 'Delete Group' endpoint is used to remove a group from the system.

```ftl
      tag = "Group"
      summary = "Delete Group"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/group/{id}/members/{userId}/put.ftl" line="5">

---

# Managing Group Members

Members can be added to a group using the 'Create Group Member' endpoint.

```ftl
      tag = "Group"
      summary = "Create Group Member"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/group/{id}/members/{userId}/delete.ftl" line="5">

---

# Removing Group Members

Members can be removed from a group using the 'Delete a Group Member' endpoint.

```ftl
      tag = "Group"
      summary = "Delete a Group Member"
```

---

</SwmSnippet>

# Group Functions

Let's delve into the functions related to 'Group' in Citi-camunda.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/authorization/Groups.java" line="1">

---

## Group Functions in Groups.java

The 'Groups.java' file contains the definitions of various group-related operations. These operations include creating, updating, deleting, and retrieving groups. They are essential for managing user groups in the application.

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

/**
 * Holds the set of built-in user identities for Camunda Platform.
 *
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/camunda-bpm-sdk-js/lib/api-client/resources/group.js" line="1">

---

## Group Functions in group.js

The 'group.js' file in the frontend module provides the client-side implementation of the group-related operations. These operations are used to interact with the server-side group functions and manage groups on the client side.

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
