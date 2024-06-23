---
title: Introduction to Process Instances
---
A Process Instance in Camunda represents a single execution of a process definition. It is the concrete representation of a running process, containing the current state, variables, and activity of that process. Each instance has a unique ID and can be manipulated and queried through various parts of the Camunda platform, such as the Cockpit or the REST API. Process Instances are used extensively throughout the Citi-camunda codebase, particularly in the Cockpit's frontend, where they are displayed, sorted, and managed.

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/base/app/views/processInstance/calledProcessInstanceTable.js" line="126">

---

# Process Instance in Code

Here, a Process Instance is being used as a controller in the 'CalledProcessInstanceTable' component. This allows the component to interact with the process instance and its associated data.

```javascript
      controller: 'CalledProcessInstanceController',
      priority: 10
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/base/app/views/processInstance/cancelProcessInstanceAction.js" line="37">

---

In this code snippet, a function called 'processInstance' is defined which returns the current process instance from the scope. This function can be used to retrieve the current process instance when needed.

```javascript
              processInstance: function() {
                return $scope.processInstance;
              }
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/base/app/views/processInstance/userTasksTable.js" line="100">

---

Here, the process instance is being used to create a new child scope for user task data. This allows the user task data to be associated with the specific process instance.

```javascript
        processInstance = $scope.processInstance,
        taskIdIdToExceptionMessageMap,
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/base/app/views/processInstance/called-process-instance-table.html" line="21">

---

In this HTML template, the process instance is being used to generate a table of called process instances. Each row in the table represents a single process instance, with the 'id' of the process instance being used as a unique identifier.

```html
        <td class="called-process-instance"
            cam-widget-clipboard="calledProcessInstance.id">
          <a href="#/process-instance/{{ calledProcessInstance.id }}/runtime">
            {{ calledProcessInstance.id }}
          </a>
        </td>
```

---

</SwmSnippet>

# Functions of Process Instance

This section will cover the main functions of Process Instance in Camunda Platform 7.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/runtime/ProcessInstance.java" line="1">

---

## Creation of Process Instances

The creation of a process instance is handled by the `ProcessInstance` class. This class provides methods to start a new process instance, set variables for the process instance, and retrieve the process instance's ID and process definition ID.

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
package org.camunda.bpm.engine.runtime;

import org.camunda.bpm.engine.repository.ProcessDefinition;

/**
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/runtime/ActivityInstantiationBuilder.java" line="1">

---

## Execution of Process Instances

The execution of a process instance is managed by the `ActivityInstantiationBuilder` class. This class provides methods to control the execution flow of the process instance, such as starting a specific activity in the process instance.

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
package org.camunda.bpm.engine.runtime;

import java.util.Map;

/**
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/base/app/views/processInstance/cancelProcessInstanceAction.js" line="1">

---

## Termination of Process Instances

The termination of a process instance is handled by the `cancelProcessInstanceAction` function. This function provides a user interface for users to cancel a running process instance.

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

var dialogTemplate = require('./cancel-process-instance-dialog.html?raw');
var actionTemplate = require('./cancel-process-instance-action.html?raw');
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
