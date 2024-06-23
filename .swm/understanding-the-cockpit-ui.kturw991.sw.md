---
title: Understanding the Cockpit UI
---
Cockpit UI is the user interface component of the Camunda Platform. It is designed to provide a visual interface for process management and operations. The Cockpit UI is built using JavaScript and AngularJS, and it interacts with the Camunda Platform's backend services to fetch and display data. It provides features like process instance monitoring, batch operations, and task management. The UI is modular and extendable, allowing developers to add custom plugins to enhance its functionality.

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/camunda-cockpit-ui.js" line="47">

---

# Cockpit UI Initialization

This section of the code is responsible for initializing the Cockpit UI. It sets up the AngularJS module for the application, configures various providers, and bootstraps the application. It also exposes certain packages to the global scope for use by plugins.

```javascript
export function init(pluginDependencies) {
  var ngDependencies = [
    'ng',
    'ngResource',
    'pascalprecht.translate',
    commons.name,
    require('./repository/main').name,
    require('./batches/main').name,
    require('./reports/main').name,
    require('./directives/main').name,
    require('./filters/main').name,
    require('./pages/main').name,
    require('./resources/main').name,
    require('./services/main').name,
    require('./navigation/main').name
  ].concat(
    pluginDependencies.map(function(el) {
      return el.ngModuleName;
    })
  );

```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/camunda-cockpit-ui.js" line="206">

---

# Cockpit UI Components

This part of the code exposes various packages that are used by the Cockpit UI. These packages include AngularJS, jQuery, Camunda Commons UI, Camunda BPM SDK JS, and others. These packages are made available in the global scope for use by plugins.

```javascript
export function exposePackages(container) {
  container.angular = angular;
  container.jquery = $;
  container['camunda-commons-ui'] = commons;
  container['camunda-bpm-sdk-js'] = sdk;
  container['angular-data-depend'] = dataDepend;
  container['moment'] = moment;
  container['events'] = events;
  container['cam-common'] = camCommon;
  container['lodash'] = lodash;
}
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/cockpitPlugins.js" line="29">

---

# Cockpit UI Plugins

This section of the code defines the AngularJS module for the Cockpit UI plugins. It includes various plugins such as base, decisionList, jobDefinition, tasks, and externalTasksTab.

```javascript
export default angular.module('cockpit.plugin.cockpitPlugins', [
  base.name,
  decisionList.name,
  jobDefinition.name,
  tasks.name,
  externalTasksTab.name
]);
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/batches/templates/cam-cockpit-batch-view.html" line="1">

---

# Cockpit UI Views

This HTML file defines the view for the batch management feature of the Cockpit UI. It includes various controls for searching, sorting, and paginating batches, as well as displaying batch details and progress.

```html
<div class="batch-wrapper">
  <div class="row">
    <div class="col-md-6">
      <h3>{{ 'BATCHES_PROGRESS_IN' | translate }}</h3>

      <div cam-widget-search
           cam-widget-search-total="ctrl.getBatchCount('runtime')"
           cam-widget-search-valid-searches="search.searches"
           cam-widget-search-translations="search.translations"
           cam-widget-search-types="search.types"
           cam-widget-search-operators="search.operators"
           cam-widget-search-storage-group="'BIP'"
           cam-widget-search-mode="filter"></div>

      <div cam-widget-loader
           loading-state="{{ ctrl.getLoadingState('runtime') }}"
           text-empty="{{ 'BATCHES_PROGRESS_NO_RUNNING' | translate }}">

        <table class="cam-table">
          <thead sortable-table-head
                 head-columns="runtimeHeadColumns"
```

---

</SwmSnippet>

# Cockpit UI Components

This section will cover the main functions of the Cockpit UI, focusing on the navigation, tasks, and dashboard components.

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/navigation/main.js" line="1">

---

## Navigation Component

The navigation component of the Cockpit UI is defined in this file. It controls the navigation bar and handles user interactions with it.

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

var angular = require('camunda-commons-ui/vendor/angular'),
  camHeaderViewsCtrl = require('./controllers/cam-header-views-ctrl');
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/tasks/app/views/dashboard/task-dashboard.js" line="1">

---

## Tasks Component

The tasks component is responsible for displaying the tasks in the Cockpit UI. It fetches the tasks data and renders them in a table format.

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

var template = require('./task-dashboard.html?raw');

```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" line="1">

---

## Dashboard Component

The dashboard component serves as the main view of the Cockpit UI. It aggregates data from various sources and displays them in a user-friendly manner.

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

var template = require('./dashboard.html?raw');
var series = require('camunda-bpm-sdk-js').utils.series;
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
