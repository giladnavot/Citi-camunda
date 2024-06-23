---
title: Introduction to Cockpit UI Process Instance
---
The Cockpit UI Process Instance in the Citi-camunda repository refers to the visual representation and management of a single instance of a process within the Camunda Cockpit. It provides a detailed view of the process, including its current state, variables, and activities. It also allows for interaction with the process instance, such as modifying variables, handling user tasks, and managing incidents. The Cockpit UI Process Instance is primarily implemented in JavaScript and HTML, and is part of the Camunda Webapp frontend.

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/base/app/views/processInstance/called-process-instance-table.html" line="1">

---

# Process Instance Table

This file defines the HTML structure of the process instance table. It uses AngularJS directives to bind data to the UI and handle user interactions.

```html
<!-- # CE - camunda-bpm-webapp/webapp/src/main/resources-plugin/base/app/views/processInstance/called-process-instance-table.html -->
<div cam-widget-loader
     loading-state="{{ loadingState }}"
     text-empty="{{ 'PLUGIN_CALLED_PROCESS_NO_PROCESS_INSTANCES' | translate }}">
  <table class="called-process-instance cam-table">

    <thead sortable-table-head
           head-columns="headColumns"
           on-sort-change="onSortChange(sortObj)"
           default-sort="sortObj">
    </thead>

    <tbody>
      <tr ng-repeat="calledProcessInstance in calledProcessInstances | orderBy:sortObj.sortBy:sortObj.sortReverse">
        <td class="state">
          <div ng-if="calledProcessInstance.incidents.length > -1" state-circle incidents="calledProcessInstance.incidents"></div>
          <div ng-if="calledProcessInstance.incidents == undefined">
            <span class="glyphicon glyphicon-refresh animate-spin"></span>
          </div>
        </td>
        <td class="called-process-instance"
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/base/app/views/processInstance/calledProcessInstanceTable.js" line="26">

---

# Process Instance Controller

This file defines the controller for the process instance table. It handles the logic for loading process instances, sorting them, and updating the view when the data changes.

```javascript
  ngModule.controller('CalledProcessInstanceController', [
    '$scope',
    'PluginProcessInstanceResource',
    '$translate',
    'localConf',
    function($scope, PluginProcessInstanceResource, $translate, localConf) {
      // input: processInstance, processData

      var calledProcessInstanceData = $scope.processData.newChild($scope);

      // var processInstance = $scope.processInstance;

      // prettier-ignore
      $scope.headColumns = [
        { class: 'state', request: 'incidents', sortable: true, content: 'State' },
        { class: 'called-process-instance', request: 'id', sortable: true, content: $translate.instant('PLUGIN_CALLED_PROCESS_PROCESS_INSTANCE')},
        { class: 'process-definition', request: 'processDefinitionLabel', sortable: true, content: $translate.instant('PLUGIN_CALLED_PROCESS_PROCESS_DEFINITION')},
        { class: 'activity', request: 'instance.name', sortable: true, content: $translate.instant('PLUGIN_CALLED_PROCESS_ACTIVITY')}
      ];

      // Default sorting
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/tests/pages/process-instance/tabs/called-process-instances-tab.js" line="1">

---

# Process Instance Tests

This file defines tests for the process instance table. It checks that the table displays the correct data and responds correctly to user interactions.

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

var Table = require('./../../table');

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
