---
title: Basic Concepts of Plugins
---
Plugins in Citi-camunda are modular pieces of code that add specific functionalities to the application. They are used to extend the capabilities of the base application without modifying the core codebase. Plugins can be found in various parts of the application, such as the cockpit, tasks, decision list, and job definition. They are typically structured as Angular modules and may include views, resources, and data modules. For example, the base plugin includes views, resources, and data modules, while the tasks plugin only includes a views module. Diagram plugins are a specific type of plugin used to add functionality to the process diagrams.

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/base/app/plugin.js" line="1">

---

# Plugin Structure

This is an example of a plugin file. It starts with some metadata and licensing information, followed by the definition of the plugin. The plugin is an AngularJS module that requires other modules to function. In this case, it requires the 'views', 'resources', and 'data' modules.

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

/**
 * @namespace cam.cockpit.plugin
 */

```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/cockpitPlugins.js" line="18">

---

# Plugin Usage

This is an example of how plugins are used. The required plugins are added to the 'cockpit.plugin.cockpitPlugins' AngularJS module. This makes the functionality of the plugins available to the rest of the application.

```javascript
'use strict';

import 'ui/cockpit/plugins/styles.less';

var angular = require('angular'),
  base = require('./base/app/plugin'),
  decisionList = require('./decisionList/app/plugin'),
  jobDefinition = require('./jobDefinition/app/plugin'),
  tasks = require('./tasks/app/plugin'),
  externalTasksTab = require('./external-tasks-process-instance-runtime-tab');

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

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/base/app/views/main.js" line="23">

---

# Plugin Types

There are different types of plugins, each providing specific functionality. For example, 'diagramInstancePlugins' and 'diagramDefinitionPlugins' are used for handling diagrams in process instances and process definitions respectively.

```javascript
var angular = require('angular'),
  camCommon = require('ui/common/scripts/module/index'),
  diagramInstancePlugins = require('./processInstance/diagramPlugins'),
  diagramDefinitionPlugins = require('./processDefinition/diagramPlugins'),
  // dashboard
```

---

</SwmSnippet>

# Plugin Functions

This section will cover the main functions related to plugins in the Citi-camunda project.

<SwmSnippet path="/webapps/frontend/camunda-commons-ui/lib/plugin/service.js" line="140">

---

## registerDefaultView Function

The 'registerDefaultView' function is used to register a view provider for a specified view. It takes two parameters: a key and a viewProvider object. The viewProvider object includes properties such as 'id', 'label', 'url', 'controller', and 'priority'. This function is crucial for the functioning of plugins as it helps in registering and managing the views associated with each plugin.

```javascript
      /**
       * Registers the given viewProvider for the specified view
       *
       * View provider is an object like the following:
       *
       * <pre>
       *   {
       *     id: String, // id if the view
       *     label: String, // label of the view
       *     url: String, // url to the provided view; may be prefixed with plugin://
       *     controller: Function || String, // controller reference or name
       *     priority: number// priority of the view (default 0)
       *   }
       * </pre>
       *
       * @param {string} key
       * @param {Object} viewProvider
       */
      this.registerDefaultView = function(key, viewProvider) {
        // test if the plugin is excluded
        if (excludeExp && excludeExp.test(key + ':' + viewProvider.id)) {
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/base/app/views/processInstance/incidentsTab.js" line="22">

---

## Configuration Function

The 'Configuration' function is used to configure the views for a plugin. It uses the 'registerDefaultView' function to register a default view for a plugin. The function takes a 'ViewsProvider' as a parameter and registers a default view with an 'id', 'label', 'template', and 'priority'. This function is important for setting up the views for each plugin.

```javascript
var Configuration = function PluginConfiguration(ViewsProvider) {
  ViewsProvider.registerDefaultView('cockpit.processInstance.runtime.tab', {
    id: 'incidents-tab',
    label: 'PLUGIN_INCIDENTS_LABEL',
    template: incidentsTemplate,
    priority: 15
  });
};
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
