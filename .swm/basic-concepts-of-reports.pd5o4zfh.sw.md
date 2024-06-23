---
title: Basic Concepts of Reports
---
Reports in Citi-camunda refer to the visual representation of data processed by the Camunda Platform. They are implemented using AngularJS directives and controllers. The 'reports' directory contains scripts for handling the creation, display, and management of reports. The 'reportData' property is used to store and manipulate the data that is to be displayed in the report. The 'getDefaultReport' function is used to fetch the default report if no specific report is selected. The 'getPluginProviders' function is used to fetch the providers for the report plugins. The 'reportsType' property is used to define the type of report to be displayed.

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/reports/directives/reports-type.js" line="25">

---

# Report Directives

This is the definition of the 'reportData' property in the 'reports-type' directive. This property is used to pass the data that will be displayed in the report.

```javascript
      restrict: 'A',
      scope: {
        reportData: '=',
        getPluginProviders: '&'
      },
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/reports/controllers/reports-view-ctrl.js" line="42">

---

# Report Controllers

This is the 'getDefaultReport' function in the 'reports-view' controller. It is used to get the default report if no specific report is selected.

```javascript
    var getDefaultReport = function(reports) {
      if (!reports || !$scope.selectedReportId) {
        return;
      }

      if ($scope.selectedReportId) {
        return (getPluginProviders({id: $scope.selectedReportId}) || [])[0];
      }
    };
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/reports/controllers/reports-view-ctrl.js" line="20">

---

# Report Templates

This is the definition of the 'template' variable in the 'reports-view' controller. It is used to specify the HTML template for the report view.

```javascript
var template = require('./reports-view.html?raw');
var angular = require('camunda-commons-ui/vendor/angular');
var extend = angular.extend;
```

---

</SwmSnippet>

# Report Functions

This section will cover the main functions related to the Reports feature in the Citi-camunda project.

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/reports/controllers/reports-view-ctrl.js" line="42">

---

## getDefaultReport Function

The `getDefaultReport` function is used to get the default report based on the selected report ID. If no report ID is selected, it returns undefined. If a report ID is selected, it calls the `getPluginProviders` function with the selected report ID as a parameter.

```javascript
    var getDefaultReport = function(reports) {
      if (!reports || !$scope.selectedReportId) {
        return;
      }

      if ($scope.selectedReportId) {
        return (getPluginProviders({id: $scope.selectedReportId}) || [])[0];
      }
    };
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/reports/controllers/reports-view-ctrl.js" line="37">

---

## getPluginProviders Function

The `getPluginProviders` function is used to get the providers for the plugin components of the cockpit report. It takes an options object as a parameter, which includes the component and ID of the report. It then calls the `Views.getProviders` function with these options.

```javascript
    function getPluginProviders(options) {
      var _options = extend({}, options || {}, {component: 'cockpit.report'});
      return Views.getProviders(_options);
    }
```

---

</SwmSnippet>

# Reports Module

Reports View Controller and Directives

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/reports/controllers/reports-view-ctrl.js" line="20">

---

## Reports View Controller

This file defines the controller for the reports view. It handles the logic for displaying the reports, including fetching the data for the selected report and updating the view when the selected report changes. The `getPluginProviders` function is used to get the providers for the selected report, and the `getDefaultReport` function is used to get the default report if no report is selected.

```javascript
var template = require('./reports-view.html?raw');
var angular = require('camunda-commons-ui/vendor/angular');
var extend = angular.extend;

var Controller = [
  '$scope',
  '$route',
  'page',
  'dataDepend',
  'Views',
  '$translate',
  function($scope, $route, page, dataDepend, Views, $translate) {
    $scope.selectedReportId =
      (($route.current || {}).params || {}).reportType || null;

    // utilities ///////////////////////////////////////////////////////////////////

    function getPluginProviders(options) {
      var _options = extend({}, options || {}, {component: 'cockpit.report'});
      return Views.getProviders(_options);
    }
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/reports/directives/reports-type.js" line="18">

---

## Reports Type Directive

This file defines a directive for the reports type. It observes changes in the selected report and updates the view accordingly. The `getPluginProviders` function is used here to get the providers for the selected report.

```javascript
'use strict';

var template = require('./reports-type.html?raw');

module.exports = [
  function() {
    return {
      restrict: 'A',
      scope: {
        reportData: '=',
        getPluginProviders: '&'
      },

      template: template,

      controller: [
        '$scope',
        '$route',
        function($scope, $route) {
          var getPluginProviders = $scope.getPluginProviders();

```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/reports/directives/reports-plugin.js" line="18">

---

## Reports Plugin Directive

This file defines a directive for the reports plugin. It observes changes in the selected report and updates the view accordingly.

```javascript
'use strict';

var template = require('./reports-plugin.html?raw');

module.exports = [
  function() {
    return {
      restrict: 'A',
      scope: {
        reportData: '='
      },

      template: template,

      controller: [
        '$scope',
        function($scope) {
          var reportPluginData = ($scope.reportPluginData = $scope.reportData.newChild(
            $scope
          ));

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
