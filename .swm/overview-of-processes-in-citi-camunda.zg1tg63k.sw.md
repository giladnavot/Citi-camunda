---
title: Overview of Processes in Citi-camunda
---
Processes in Citi-camunda refer to the sequence of tasks that are part of a workflow. They are defined using the BPMN 2.0 standard and are executed by the Camunda process engine. Processes are integral to the automation capabilities of the platform, allowing for complex business workflows to be modeled and executed programmatically.

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/batches/controllers/view-ctrl.js" line="6">

---

# Process Definition

This file is part of the Cockpit application which provides a user interface for managing and monitoring processes. It contains the controller for the view that displays the details of a specific process instance.

```javascript
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
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/batches/controllers/modal-ctrl.js" line="6">

---

# Process Execution

This file contains the controller for a modal dialog that is used to interact with a running process instance. It allows users to start, pause, resume, and cancel process instances.

```javascript
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
```

---

</SwmSnippet>

# Functions of Processes

Let's delve into the functions of Processes in the Citi-camunda project.

<SwmSnippet path="/webapps/frontend/camunda-bpm-sdk-js/lib/api-client/resources/process-definition.js" line="1">

---

## Process Definition Functions

The functions in this file are used to interact with the process definitions in the Camunda engine. They allow for operations such as retrieving a process definition, starting a process instance, and suspending or activating a process definition.

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

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/base/app/views/dashboard/processes.js" line="1">

---

## Process Instance Functions

The functions in this file are used to interact with the process instances. They allow for operations such as retrieving a list of process instances, getting the count of process instances, and retrieving the statistics of a process definition.

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

module.exports = [
  'ViewsProvider',
```

---

</SwmSnippet>

# Batch Endpoint and Controller

Batch View Endpoint

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/batches/config/routes.js" line="26">

---

## /batch Endpoint

The '/batch' endpoint is defined in the 'routes.js' file. When this endpoint is hit, it renders a template and uses a controller to manage the view. It requires authentication and does not reload on search.

```javascript
    $routeProvider.when('/batch', {
      template: template,
      controller: ctrl,
      authentication: 'required',
      reloadOnSearch: false
    });
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/batches/controllers/view-ctrl.js" line="32">

---

## Batch View Controller

The 'view-ctrl.js' file is the controller for the '/batch' endpoint. It handles various operations such as loading details, opening modals, and handling events related to batches.

```javascript
  '$scope',
  'page',
  'camAPI',
  '$location',
  '$uibModal',
  '$translate',
  'Notifications',
  'localConf',
  'configuration',
  'searchWidgetUtils',
  function(
    $scope,
    page,
    camAPI,
    $location,
    $modal,
    $translate,
    Notifications,
    localConf,
    configuration,
    searchWidgetUtils
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
