---
title: Introduction to the Dashboard
---
The Dashboard in Citi-camunda is a central component that provides an overview of the decision-making processes. It is implemented using AngularJS and is part of the cockpit plugin. The dashboard includes a decision list, which is a table of decisions made in the process. This list is managed by the DecisionListController and the decisionListService. The decisionsTable directive is used to display the decisions in a tabular format.

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/decisionList/app/views/dashboard/index.js" line="20">

---

# Dashboard Code Structure

This file is the entry point for the Dashboard view. It imports necessary modules, configures the Angular module for the Dashboard, and exports the module. The Dashboard view is composed of several components, including a decision list and a decisions table, which are defined and registered in this file.

```javascript
var angular = require('angular');
var camCommon = require('ui/common/scripts/module/index');
var decisionList = require('./views/decision-list');
var DecisionListController = require('./controllers/decision-list');
var decisionListService = require('./services/decision-list');
var decisionsTableComponent = require('./components/decisions-table');

var ngModule = angular.module('cockpit.plugin.decisionList.views.dashboard', [
  camCommon.name
]);

ngModule.config(decisionList);

ngModule.factory('decisionList', decisionListService);

ngModule.controller('DecisionListController', DecisionListController);

ngModule.directive('decisionsTable', decisionsTableComponent);

module.exports = ngModule;
```

---

</SwmSnippet>

# Dashboard Functions

The Dashboard's main functions are implemented across several files and directories, with key components such as the decisions table and decision list services.

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/decisionList/app/views/dashboard/services/decision-list.js" line="1">

---

## Decision List Services

The decision list services are a key part of the dashboard's functionality. They handle the logic for fetching and managing decision lists, which are likely a central part of the dashboard's display.

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
  '$q',
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/decisionList/app/views/dashboard/components/decisions-table.js" line="1">

---

## Decisions Table Component

The decisions table component is another crucial part of the dashboard. It likely handles the display of decision lists on the dashboard, working in tandem with the decision list services to provide a comprehensive view of decision lists.

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

var template = require('./decisions-table.html?raw');

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
