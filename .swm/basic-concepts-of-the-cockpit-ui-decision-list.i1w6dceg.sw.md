---
title: Basic Concepts of the Cockpit UI Decision List
---
The Cockpit UI Decision List in the Citi-camunda project refers to a user interface component that displays a list of decisions made by the Camunda workflow engine. This list is part of the Camunda Cockpit, a web-based administration tool for monitoring and managing workflow instances. The Decision List provides a comprehensive view of all decisions, allowing users to navigate and manage them effectively. It includes features such as pagination, sorting, and searching to enhance usability. The Decision List is implemented using AngularJS and is located in the 'webapps/frontend/ui/cockpit/plugins/decisionList' directory of the project.

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/decisionList/app/views/dashboard/controllers/decision-list.js" line="22">

---

# Decision List Controller

This is the main controller for the Decision List. It manages the state of the decision list, handles pagination and sorting, and fetches decision data from the backend.

```javascript
module.exports = [
  '$scope',
  'decisionList',
  'Views',
  'localConf',
  '$location',
  'search',
  function($scope, decisionList, Views, localConf, $location, search) {
    $scope.loadingState = 'LOADING';
    $scope.drdDashboard = Views.getProvider({
      component: 'cockpit.plugin.drd.dashboard'
    });
    $scope.isDrdDashboardAvailable = !!$scope.drdDashboard;

    var initialSearch = $location.search();

    var pages = ($scope.paginationController = {
      decisionPages: {
        size: 50,
        total: 0,
        current: initialSearch.decisionPage || 1
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/decisionList/app/views/dashboard/views/decision-list.js" line="20">

---

# Decision List View

This file defines the view for the Decision List. It specifies the template to use and the controller to bind to the view.

```javascript
var template = require('./decision-list.html?raw');

module.exports = [
  'ViewsProvider',
  function(ViewsProvider) {
    ViewsProvider.registerDefaultView('cockpit.decisions.dashboard', {
      id: 'decision-list',
      label: 'Deployed Decision Tables',
      template: template,
      controller: 'DecisionListController',
      priority: -5 // display below the process definition list
    });
  }
];

```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/decisionList/app/views/dashboard/services/decision-list.js" line="20">

---

# Decision List Service

This service is responsible for fetching decision data from the backend. It provides methods for getting decision lists, individual decisions, and DRDs (Decision Requirements Diagrams).

```javascript
module.exports = [
  '$q',
  'camAPI',
  function($q, camAPI) {
    var decisionDefinitionService = camAPI.resource('decision-definition');
    var drdService = camAPI.resource('drd');

    var drds, decisions;

    var defaultParams = {
      latestVersion: true,
      sortBy: 'name',
      sortOrder: 'asc',
      firstResult: 0,
      maxResults: 50
    };

    function getDecisions(params) {
      return decisionDefinitionService
        .list(Object.assign({}, defaultParams, params))
        .then(function(result) {
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/decisionList/app/views/dashboard/views/decision-list.html" line="1">

---

# Decision List HTML Template

This is the HTML template for the Decision List view. It defines the structure and layout of the decision list in the Camunda Cockpit UI.

```html
<!-- # CE - camunda-bpm-webapp/webapp/src/main/resources-plugin/decisionList/app/views/dashboard/decision-list.html -->
<div class="deployed-decisions"
     cam-widget-loader
     loading-state="{{ loadingState }}"
     text-error="{{ loadingError }}">

  <div decisions-table
       decisions="decisions"
       decision-count="decisionCount"
       is-drd-available="isDrdDashboardAvailable"
       pagination="paginationController">
  </div>

  <view provider="drdDashboard"
        vars="drdDashboardVars">
  </view>
</div>
<!-- / CE - camunda-bpm-webapp/webapp/src/main/resources-plugin/decisionList/app/views/dashboard/decision-list.html -->

```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/decisionList/app/views/dashboard/components/decisions-table.js" line="20">

---

# Decision Table Component

This component defines the decision table within the decision list. It handles the display of decision data in a tabular format.

```javascript
var template = require('./decisions-table.html?raw');

module.exports = function() {
  return {
    restrict: 'A',
    template: template,
    scope: {
      decisionCount: '=',
      decisions: '=',
      isDrdAvailable: '=',
      pagination: '='
    },
    controller: [
      '$scope',
      'localConf',
      '$translate',
      function($scope, localConf, $translate) {
        // prettier-ignore
        $scope.headColumns = [
          {class: 'name', request: 'name', sortable: true, content: $translate.instant('PLUGIN_DECISION_TABLE_NAME')},
          {class: 'tenant-id', request: 'tenantId', sortable: true, content: $translate.instant('PLUGIN_DECISION_TABLE_TENANT_ID')},
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
