---
title: Introduction to Cockpit UI Dashboard
---
The Cockpit UI Dashboard in Citi-camunda is a central interface that provides an overview of various aspects of the system. It is designed to be modular and extensible, with different components providing different views or reports. For example, the 'cockpit.plugin.drd.dashboard' component provides a view of the Decision Requirement Diagrams (DRDs), while the 'cockpit.report' component provides various reports. The dashboard also includes tasks and batch operations, among other features. Each component is registered with the ViewsProvider, which manages the display of these components on the dashboard.

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/decisionList/app/views/dashboard/controllers/decision-list.js" line="30">

---

# Dashboard Components

Here, we see a component being registered with the dashboard. The `component` property specifies the identifier of the component, which is used to retrieve it later. The `Views.getProvider` function is used to retrieve the component provider, which is used to create instances of the component.

```javascript
    $scope.loadingState = 'LOADING';
    $scope.drdDashboard = Views.getProvider({
      component: 'cockpit.plugin.drd.dashboard'
    });
    $scope.isDrdDashboardAvailable = !!$scope.drdDashboard;
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/base/app/views/dashboard/tasks.js" line="18">

---

# Dashboard Navigation

This code registers a navigation item with the dashboard. The `ViewsProvider.registerDefaultView` function is used to register the navigation item, which is identified by the `id` property. The `label` property specifies the display name of the navigation item, and the `pagePath` property specifies the URL path of the page associated with the navigation item.

```javascript
'use strict';
module.exports = [
  'ViewsProvider',
  function(ViewsProvider) {
    ViewsProvider.registerDefaultView('cockpit.navigation', {
      id: 'tasks',
      label: 'COCKPIT_HUMAN_TASKS',
      template: '<!-- nothing to show, but needed -->',
      pagePath: '#/tasks',
      checkActive: function(path) {
        return path.indexOf('#/tasks') > -1;
      },
      controller: function() {},

      priority: 20
    });
  }
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/decisionList/app/views/dashboard/index.js" line="18">

---

# Dashboard Plugins

This code shows how a plugin can extend the dashboard. The plugin defines a module that provides additional views and components for the dashboard. The `angular.module` function is used to create the module, and the `require` function is used to import the necessary dependencies.

```javascript
'use strict';

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

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
