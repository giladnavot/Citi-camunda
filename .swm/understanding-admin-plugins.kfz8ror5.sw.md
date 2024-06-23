---
title: Understanding Admin Plugins
---
Admin Plugins in Citi-camunda refer to the modular components that extend the functionality of the admin interface. They are implemented using AngularJS modules and are loaded dynamically at runtime. The plugins can provide additional views, resources, and styles to customize the admin interface according to the needs of the application.

<SwmSnippet path="/webapps/frontend/ui/admin/plugins/adminPlugins.js" line="22">

---

# Admin Plugin Structure

This is the main entry point for the admin plugins. It imports the base plugin and registers it with the AngularJS module system.

```javascript
var angular = require('angular'),
  base = require('./base/app/plugin');

export default angular.module('admin.plugin.adminPlugins', [base.name]);
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/plugins/base/app/plugin.js" line="27">

---

# Base Plugin

The base plugin is a foundational module that other plugins can build upon. It defines common resources and views that can be reused by other plugins.

```javascript
const angular = require('angular'),
  viewsModule = require('./views/main'),
  resourcesModule = require('./resources/main');

module.exports = angular.module('admin.plugin.base', [
  viewsModule.name,
  resourcesModule.name
]);
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/plugins/base/app/resources/main.js" line="23">

---

# Plugin Resources

Resources are services that provide data for the plugin. They are defined as factories in the AngularJS module system.

```javascript
const ngModule = angular.module('admin.plugin.base.resources', []);

ngModule.factory('PluginMetricsResource', metrics);
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/plugins/styles.less" line="1">

---

# Plugin Styles

Styles for the plugins are defined in separate LESS files. These styles are imported into the main application's stylesheet.

```less
// get the admin app variables (based on bootstrap)
@import "~ui/admin/client/styles/_app-variables.less";

// use `reference` to avoid duplicate bootstrap styles
// as they are already available in other compiled CSS
@import (reference) "~camunda-commons-ui/resources/less/shared/bootstrap.less";

/* add plugin styles here */
@import "~camunda-commons-ui/lib/widgets/inline-field/cam-widget-inline-field";
@import "~camunda-commons-ui/lib/widgets/search-pill/cam-widget-search-pill";
@import "~camunda-commons-ui/lib/widgets/search/cam-widget-search";
@import "~camunda-commons-ui/lib/widgets/cam-share-link/cam-share-link";
@import "~camunda-commons-ui/lib/widgets/loader/cam-widget-loader";
@import "~camunda-commons-ui/lib/widgets/password/cam-widget-password";

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
