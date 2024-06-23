---
title: Understanding the Group Concept
---
In the context of the Citi-camunda repository, a 'Group' refers to a collection of users who share common access rights or roles within the Camunda BPM platform. It is a key concept in managing user permissions and access control. The 'Group' concept is used in the REST API endpoints to perform operations such as creating a new group, retrieving group information, updating a group, and deleting a group. It also allows for operations on group members and counting the number of groups.

# Defining Groups

This section of the code shows how to define a new group. You need to specify the group's name and role.

# Assigning Users to Groups

This section of the code shows how to assign a user to a group. You need to specify the user's ID and the group's name.

# Defining Access Control Policies for Groups

This section of the code shows how to define access control policies for a group. You need to specify the group's name and the permissions that should be granted to it.

# Group Functions

Let's take a look at the Group functions in the 'Groups.java' and 'group.js' files.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/authorization/Groups.java" line="1">

---

## Group Functions in 'Groups.java'

The 'Groups.java' file contains the definitions for the Group functions. These functions are used for managing user groups within the application, including creating, updating, deleting, and retrieving groups.

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

## Group Functions in 'group.js'

The 'group.js' file contains the implementation of the Group functions. These functions interact with the backend to perform the actual operations on the user groups.

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
