---
title: Overview of History in Process Execution
---
History in the Citi-camunda repository refers to the historical data related to the execution of processes. It includes information about process instances, tasks, incidents, job logs, external task logs, activity instances, decision instances, batches, user operations, details, cleanups, identity link logs, variable instances, and process definitions. These historical data are crucial for understanding the past states of processes, identifying bottlenecks, and making informed decisions for process improvements.

# Functions of History

The 'history.js' file contains the main functions for handling the history of process instances in the Camunda platform.

<SwmSnippet path="/webapps/frontend/camunda-bpm-sdk-js/lib/api-client/resources/history.js" line="1">

---

## Functions of History

The 'history.js' file contains the main functions for handling the history of process instances in the Camunda platform. These functions provide the ability to query for historic process instances, tasks, activity instances, variable instances, detail instances, job log entries, incident instances, and decision evaluation instances. They also provide the ability to delete historic process instances and tasks.

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

var AbstractClientResource = require('../abstract-client-resource');
var helpers = require('../helpers');
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
