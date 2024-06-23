---
title: Getting Started with Tasklist Plugins
---
Tasklist Plugins in Citi-camunda refer to modular components that extend the functionality of the tasklist. They are implemented as Angular modules and are imported into the main tasklist application. Examples of these plugins include 'standaloneTask', 'tasklistCard', and 'tasklistSorting'. Each plugin is organized in its own directory and includes an Angular module definition in a 'plugin.js' file. The 'tasklistPlugins.js' file serves as the entry point where all these plugins are imported and registered with the main Angular module of the tasklist.

<SwmSnippet path="/webapps/frontend/ui/tasklist/plugins/tasklistPlugins.js" line="22">

---

# Tasklist Plugins Structure

This is the main tasklist plugin module. It imports individual plugin modules such as `standaloneTask`, `tasklistCard`, and `tasklistSorting`, and includes them in the exported AngularJS module.

```javascript
var angular = require('angular'),
  standaloneTask = require('./standaloneTask/app/plugin'),
  tasklistCard = require('./tasklistCard/app/plugin'),
  tasklistSorting = require('./tasklistSorting/app/plugin');

export default angular.module('tasklist.plugin.tasklistPlugins', [
  standaloneTask.name,
  tasklistCard.name,
  tasklistSorting.name
]);
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/plugins/standaloneTask/app/plugin.js" line="20">

---

# Standalone Task Plugin

This is an example of a standalone task plugin. It exports an AngularJS module which is included in the main tasklist plugin module.

```javascript
var angular = require('angular');
var navbarModule = require('./navbar/main');

module.exports = angular.module('tasklist.plugin.standaloneTask', [
  navbarModule.name
]);
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/plugins/tasklistCard/app/plugin.js" line="20">

---

# Tasklist Card Plugin

This is an example of a tasklist card plugin. It exports an AngularJS module which is included in the main tasklist plugin module.

```javascript
var angular = require('angular');
var variablePluginModule = require('./variables/main');

module.exports = angular.module('tasklist.plugin.tasklistCard', [
  variablePluginModule.name
]);
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/plugins/tasklistSorting/app/plugin.js" line="20">

---

# Tasklist Sorting Plugin

This is an example of a tasklist sorting plugin. It exports an AngularJS module which is included in the main tasklist plugin module.

```javascript
var angular = require('angular');
var pluginModule = require('./tasklistHeader/main');

module.exports = angular.module('tasklist.plugin.tasklistSorting', [
  pluginModule.name
]);
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
