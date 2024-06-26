---
title: Understanding the Role of Plugins
---
Plugins in the Citi-camunda project are modular pieces of code that add specific functionality to the Camunda Cockpit, a web application for monitoring and managing workflows. They are implemented as AngularJS modules and are organized in a hierarchical directory structure. Each plugin has a main entry point, typically named `plugin.js`, which exports the AngularJS module. The module usually requires other modules, such as views or resources, to provide its functionality. Some plugins also provide diagram plugins, which are used to enhance the BPMN diagrams displayed in the Cockpit with additional information or interactive elements.

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/base/app/plugin.js" line="1">

---

# Plugin Structure

Each plugin is structured as an AngularJS module. The `plugin.js` file exports the module, which includes other modules as dependencies. For instance, the <SwmToken path="/webapps/frontend/ui/cockpit/plugins/base/app/views/processDefinition/diagramPlugins/index.js" pos="27:2:6" line-data="  &#39;cockpit.plugin.base.views.definition.diagram-plugins&#39;,">`cockpit.plugin.base`</SwmToken> module includes <SwmToken path="/webapps/frontend/ui/cockpit/plugins/base/app/plugin.js" pos="28:1:1" line-data="  viewsModule = require(&#39;./views/main&#39;),">`viewsModule`</SwmToken>, <SwmToken path="/webapps/frontend/ui/admin/plugins/base/app/plugin.js" pos="29:1:1" line-data="  resourcesModule = require(&#39;./resources/main&#39;);">`resourcesModule`</SwmToken>, and <SwmToken path="/webapps/frontend/ui/cockpit/plugins/base/app/plugin.js" pos="30:1:1" line-data="  dataModule = require(&#39;./data/main&#39;);">`dataModule`</SwmToken> as dependencies.

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

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/cockpitPlugins.js" line="20">

---

# Plugin Usage

Plugins are used by requiring them and including them in the module dependencies. In this file, various plugins are required and included in the <SwmToken path="/webapps/frontend/ui/cockpit/plugins/cockpitPlugins.js" pos="29:9:13" line-data="export default angular.module(&#39;cockpit.plugin.cockpitPlugins&#39;, [">`cockpit.plugin.cockpitPlugins`</SwmToken> module.

```javascript
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

# Diagram Plugins

Diagram plugins are a specific type of plugins used to extend the functionality of diagrams. They are required and included in the module dependencies just like other plugins.

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

The plugins in the Citi-camunda project are used to extend the functionality of the Camunda platform. They are implemented in various JavaScript files and are loaded when the platform starts. The main functions of these plugins include registering default views, counting instances, and handling call activities.

<SwmSnippet path="/webapps/frontend/camunda-commons-ui/lib/plugin/service.js" line="140">

---

## <SwmToken path="/webapps/frontend/camunda-commons-ui/lib/plugin/service.js" pos="158:3:3" line-data="      this.registerDefaultView = function(key, viewProvider) {">`registerDefaultView`</SwmToken>

The <SwmToken path="/webapps/frontend/camunda-commons-ui/lib/plugin/service.js" pos="158:3:3" line-data="      this.registerDefaultView = function(key, viewProvider) {">`registerDefaultView`</SwmToken> function is used to register a default view for a specified key. It takes a key and a <SwmToken path="/webapps/frontend/camunda-commons-ui/lib/plugin/service.js" pos="158:12:12" line-data="      this.registerDefaultView = function(key, viewProvider) {">`viewProvider`</SwmToken> object as parameters. The <SwmToken path="/webapps/frontend/camunda-commons-ui/lib/plugin/service.js" pos="158:12:12" line-data="      this.registerDefaultView = function(key, viewProvider) {">`viewProvider`</SwmToken> object includes properties like id, label, url, controller, and priority. This function is used in various plugins to register their views.

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

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/base/app/views/processDefinition/diagramPlugins/index.js" line="23">

---

## <SwmToken path="/webapps/frontend/ui/cockpit/plugins/base/app/views/processDefinition/diagramPlugins/index.js" pos="23:2:2" line-data="var instanceCount = require(&#39;./instanceCount&#39;);">`instanceCount`</SwmToken>

The <SwmToken path="/webapps/frontend/ui/cockpit/plugins/base/app/views/processDefinition/diagramPlugins/index.js" pos="23:2:2" line-data="var instanceCount = require(&#39;./instanceCount&#39;);">`instanceCount`</SwmToken> function is used to configure the instance count for a plugin. It is used in the diagram plugins of the base plugin.

```javascript
var instanceCount = require('./instanceCount');
var callActivity = require('./callActivity');

var ngModule = angular.module(
  'cockpit.plugin.base.views.definition.diagram-plugins',
  [camCommon.name]
);

ngModule.config(instanceCount);
ngModule.config(callActivity);
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/base/app/views/processDefinition/diagramPlugins/index.js" line="24">

---

## <SwmToken path="/webapps/frontend/ui/cockpit/plugins/base/app/views/processDefinition/diagramPlugins/index.js" pos="24:2:2" line-data="var callActivity = require(&#39;./callActivity&#39;);">`callActivity`</SwmToken>

The <SwmToken path="/webapps/frontend/ui/cockpit/plugins/base/app/views/processDefinition/diagramPlugins/index.js" pos="24:2:2" line-data="var callActivity = require(&#39;./callActivity&#39;);">`callActivity`</SwmToken> function is used to configure the call activity for a plugin. It is used in the diagram plugins of the base plugin.

```javascript
var callActivity = require('./callActivity');

var ngModule = angular.module(
  'cockpit.plugin.base.views.definition.diagram-plugins',
  [camCommon.name]
);

ngModule.config(instanceCount);
ngModule.config(callActivity);
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda"><sup>Powered by [Swimm](https://app.swimm.io/)</sup></SwmMeta>
