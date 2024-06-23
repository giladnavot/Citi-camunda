---
title: Overview of the Admin Client
---
The Admin Client in Citi-camunda refers to the administrative interface of the Camunda Platform. It is primarily used for managing users, groups, authorizations, and system settings. The Admin Client is implemented in JavaScript and is located in the 'webapps/frontend/ui/admin/client' directory. It includes several modules such as pages, services, resources, filters, and directives, each serving a specific purpose in the application. The main entry point of the Admin Client is the 'camunda-admin-ui.js' file, which initializes the application and sets up the necessary dependencies.

<SwmSnippet path="/webapps/frontend/ui/admin/client/scripts/camunda-admin-ui.js" line="41">

---

# Admin Client Initialization

The Admin Client is initialized in the 'camunda-admin-ui.js' file. The `init` function is exported which takes plugin dependencies as an argument and initializes the AngularJS modules required by the Admin Client.

```javascript
var APP_NAME = 'cam.admin';

export function init(pluginDependencies) {
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/client/scripts/camunda-admin-bootstrap.js" line="57">

---

# Admin Client Bootstrapping

The 'camunda-admin-bootstrap.js' file is responsible for bootstrapping the Admin Client. It requires the 'camunda-admin-ui.js' file and calls the `exposePackages` function on the `window` object.

```javascript
    var camundaAdminUi = require('./camunda-admin-ui');
    camundaAdminUi.exposePackages(window);
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/client/scripts/camunda-admin-ui.js" line="27">

---

# Admin Client Modules

The Admin Client is organized into different modules such as services, pages, resources, filters, and directives. These modules are required at the beginning of the 'camunda-admin-ui.js' file.

```javascript
var $ = (window.jQuery = window.$ = require('jquery')),
  pagesModule = require('./pages/main'),
  directivesModule = require('./directives/main'),
  filtersModule = require('./filters/main'),
  servicesModule = require('./services/main'),
  resourcesModule = require('./resources/main'),
  camCommonsUi = require('camunda-commons-ui/lib'),
  sdk = require('camunda-bpm-sdk-js/lib/angularjs/index'),
  angular = require('camunda-commons-ui/vendor/angular'),
  camCommon = require('../../../common/scripts/module'),
  lodash = require('camunda-commons-ui/vendor/lodash'),
  moment = require('camunda-commons-ui/vendor/moment');
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/client/scripts/pages/system.js" line="54">

---

# Admin Client System Settings

The 'system.js' file in the 'pages' module of the Admin Client is responsible for handling system settings. It uses the `Views.getProviders` function to get the providers for the 'admin.system' component.

```javascript
    $scope.systemSettingsProviders = Views.getProviders({
      component: 'admin.system'
    }).map(function(plugin) {
      if (angular.isArray(plugin.access)) {
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
