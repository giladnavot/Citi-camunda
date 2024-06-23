---
title: Exploring the Job Definition Table
---
The Job Definition Table in the Citi-camunda project refers to a specific component that is responsible for managing and displaying job definitions. Job definitions are essentially configurations for jobs that are executed by the Camunda BPMN engine. The table provides an interface for viewing and managing these definitions, including features such as pagination and sorting. It is implemented in JavaScript and uses the AngularJS framework for dynamic data binding and UI updates.

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/jobDefinition/app/views/processDefinition/jobDefinitionTable.js" line="21">

---

# Job Definition Table Structure

The Job Definition Table is defined in this file. It includes properties such as `jobDefinitions`, `id`, and `total`, which represent the job definitions data, the table's identifier, and the total number of job definitions, respectively. The `loadJobDefinitions` function is used to fetch job definitions data from the backend.

```javascript
var searchWidgetUtils = require('../../../../../../common/scripts/util/search-widget-utils');

var template = require('./job-definition-table.html?raw');

var Controller = [
  '$scope',
  'Views',
  '$translate',
  'localConf',
  'camAPI',
  'search',
  function($scope, Views, $translate, localConf, camAPI, search) {
    // prettier-ignore
    $scope.headColumns = [
      { class: 'state',         request: 'suspended'     , sortable: true, content: $translate.instant('PLUGIN_JOBDEFINITION_STATE')},
      { class: 'activity',      request: 'activityName'     , sortable: true, content: $translate.instant('PLUGIN_JOBDEFINITION_ACTIVITY')},
      { class: 'type',          request: 'jobType'         , sortable: true, content: $translate.instant('PLUGIN_JOBDEFINITION_TYPE')},
      { class: 'configuration', request: 'jobConfiguration', sortable: true, content: $translate.instant('PLUGIN_JOBDEFINITION_CONFIGURATION')},
      { class: 'overriding-job-priority', request: 'overridingJobPriority', sortable: true, content: $translate.instant('PLUGIN_JOBDEFINITION_JOB_PRIORITY')},
      { class: 'action',        request: 'action', sortable: false, content: $translate.instant('PLUGIN_JOBDEFINITION_ACTION')}
    ];
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/jobDefinition/app/views/processDefinition/jobDefinitionTable.js" line="117">

---

# Job Definition Table Usage

The `loadJobDefinitions` function is invoked to fetch job definitions data from the backend. The fetched data is then processed and stored in the `jobDefinitions` property. The `updateView` function is used to update the table's view based on the current filter settings.

```javascript
    function loadJobDefinitions() {
      $scope.jobDefinitions = null;

      JobProvider.list({
        processDefinitionId: processDefinition.id,
        maxResults: $scope.pages.size,
        firstResult: ($scope.pages.current - 1) * $scope.pages.size
      }).then(function(res) {
        jobDefinitions = res;

        updateTaskNames();
        updateView({});
      });
    }

    $scope.$on(
      '$processDefinition.suspensionState.changed',
      loadJobDefinitions
    );

    function updateView(filter) {
```

---

</SwmSnippet>

# Job Definition Table Functions

The Job Definition Table is a key component in the Citi-camunda project. It is responsible for managing and displaying job definitions. The table is implemented in the 'jobDefinitionTable.js' file and is represented in the 'job-definition-table.html' file. The table includes several functions and properties that contribute to its functionality.

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/jobDefinition/app/views/processDefinition/jobDefinitionTable.js" line="117">

---

## loadJobDefinitions Function

The `loadJobDefinitions` function is responsible for loading job definitions. It sets the `jobDefinitions` property to null, then uses the `JobProvider` to list job definitions based on the process definition id, max results, and first result. After receiving the response, it updates the task names and view.

```javascript
    function loadJobDefinitions() {
      $scope.jobDefinitions = null;

      JobProvider.list({
        processDefinitionId: processDefinition.id,
        maxResults: $scope.pages.size,
        firstResult: ($scope.pages.current - 1) * $scope.pages.size
      }).then(function(res) {
        jobDefinitions = res;

        updateTaskNames();
        updateView({});
      });
    }
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/jobDefinition/app/views/processDefinition/jobDefinitionTable.js" line="92">

---

## updateTaskNames Function

The `updateTaskNames` function is used to update the names of tasks. It iterates over the job definitions and for each job definition, it updates the activity name based on the bpmnElement name or id.

```javascript
    var updateTaskNames = function() {
      angular.forEach(jobDefinitions, function(jobDefinition) {
        var activityId = jobDefinition.activityId,
          bpmnElement = bpmnElements[activityId];
        jobDefinition.activityName =
          (bpmnElement && (bpmnElement.name || bpmnElement.id)) || activityId;
      });
    };
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/jobDefinition/app/views/processDefinition/jobDefinitionTable.js" line="137">

---

## updateView Function

The `updateView` function is used to update the view based on the filter. If there are no activity ids, it sets the `jobDefinitions` property to the job definitions. Otherwise, it creates a new array of job definitions that match the activity ids and sets the `jobDefinitions` property to this new array.

```javascript
    function updateView(filter) {
      $scope.jobDefinitions = null;

      var activityIds = filter.activityIds;

      if (!activityIds || !activityIds.length) {
        $scope.jobDefinitions = jobDefinitions;
        return;
      }

      var jobDefinitionSelection = [];

      angular.forEach(jobDefinitions, function(jobDefinition) {
        var activityId = jobDefinition.activityId;

        if (activityIds.indexOf(activityId) != -1) {
          jobDefinitionSelection.push(jobDefinition);
        }
      });

      $scope.jobDefinitions = jobDefinitionSelection;
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
