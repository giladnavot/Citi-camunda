---
title: Understanding the Job Definition Suspension Overlay
---
The Job Definition Suspension Overlay in the Citi-camunda project refers to a visual overlay that indicates the suspension state of job definitions in a process definition diagram. It is implemented in the 'jobDefinitionSuspensionOverlay.js' file, which uses a template defined in 'job-definition-suspension-overlay.html'. The overlay is controlled by a Controller and has a priority level of 10, which may determine its order of appearance or precedence among other overlays. The 'isSuspended' function is used to check if the job definitions for an element are suspended. Changes in the suspension state of the process definition trigger an update in the job definitions data.

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/jobDefinition/app/views/processDefinition/jobDefinitionSuspensionOverlay.js" line="18">

---

## Job Definition Suspension Overlay Structure

The Job Definition Suspension Overlay is defined in this file. It is an object with properties such as `id`, `template`, `controller`, and `priority`. The `id` is a unique identifier for the overlay, the `template` is the HTML structure of the overlay, the `controller` is the function that controls the overlay's behavior, and the `priority` determines the order of the overlays if there are multiple overlays.

```javascript
'use strict';

var template = require('./job-definition-suspension-overlay.html?raw');

var Controller = [
  '$scope',
  function($scope) {
    var bpmnElement = $scope.bpmnElement,
      processData = $scope.processData.newChild($scope);

    processData.provide('jobDefinitionsForElement', [
      'jobDefinitions',
      function(jobDefinitions) {
        var matchedDefinitions = [];
        for (var i = 0; i < jobDefinitions.length; i++) {
          var jobDefinition = jobDefinitions[i];
          if (jobDefinition.activityId === bpmnElement.id) {
            matchedDefinitions.push(jobDefinition);
          }
        }
        return matchedDefinitions;
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/jobDefinition/app/views/processDefinition/job-definition-suspension-overlay.html" line="1">

---

## Suspension State Indicator

This is the HTML structure of the overlay. It uses a badge with a tooltip to indicate the suspension state. The badge is shown when the `isSuspended` function returns true.

```html
<!-- # CE - camunda-bpm-webapp/webapp/src/main/resources-plugin/jobDefinition/app/views/processDefinition/job-definition-suspension-overlay.html -->
<span class="badge badge-warning activity-top-right-position"
      uib-tooltip="{{ 'PLUGIN_JOBDEFINITION_TOOLTIP_SUSPENSION' | translate }}"
      tooltip-placement="top"
      ng-show="isSuspended()">
  <span class="glyphicon glyphicon-pause"></span>
</span>
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/jobDefinition/app/views/processDefinition/jobDefinitionSuspensionOverlay.js" line="56">

---

## Suspension State Determination

The `isSuspended` function is used to determine whether the badge should be shown. It returns true when there is at least one suspended job definition for the element.

```javascript
    $scope.isSuspended = function() {
      return (
        $scope.jobDefinitionsForElement.filter &&
        $scope.jobDefinitionsForElement.filter(function(jobDefinition) {
          return jobDefinition.suspended;
        }).length > 0
      );
    };
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/jobDefinition/app/views/processDefinition/jobDefinitionSuspensionOverlay.js" line="42">

---

## Suspension State Change Handler

This is the handler for the `$processDefinition.suspensionState.changed` event. When the suspension state of the process definition changes, it triggers the `processData.changed` function with 'jobDefinitions' as the argument, which would cause the overlay to update.

```javascript
    $scope.$on('$processDefinition.suspensionState.changed', function() {
      processData.changed('jobDefinitions');
    });
```

---

</SwmSnippet>

# Job Definition Suspension Overlay Functions

This section will cover the main functions of the Job Definition Suspension Overlay.

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/jobDefinition/app/views/processDefinition/jobDefinitionSuspensionOverlay.js" line="56">

---

## isSuspended Function

The `isSuspended` function checks if a job definition is suspended. It filters the job definitions for the element and checks if any of them are suspended. If at least one job definition is suspended, it returns true.

```javascript
    $scope.isSuspended = function() {
      return (
        $scope.jobDefinitionsForElement.filter &&
        $scope.jobDefinitionsForElement.filter(function(jobDefinition) {
          return jobDefinition.suspended;
        }).length > 0
      );
    };
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/jobDefinition/app/views/processDefinition/jobDefinitionSuspensionState.js" line="67">

---

## updateSuspensionState Function

The `updateSuspensionState` function is responsible for updating the suspension state of a job definition. It sends a PUT request to the server with the new suspension state and handles the server response. If the update is successful, it broadcasts a change event and displays a success message. If the update fails, it displays an error message.

```javascript
    $scope.updateSuspensionState = function() {
      $scope.status = PERFORM_UPDATE;

      var data = {};
      data.suspended = !jobDefinition.suspended;
      data.includeJobs = $scope.data.includeJobs;
      data.executionDate = !$scope.data.executeImmediately
        ? fixDate($scope.data.executionDate)
        : null;

      $http
        .put(
          Uri.appUri(
            'engine://engine/:engine/job-definition/' +
              jobDefinition.id +
              '/suspended/'
          ),
          data
        )
        .then(function() {
          $scope.status = UPDATE_SUCCESS;
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/jobDefinition/app/views/processDefinition/diagramPlugins/jobSuspension.js" line="53">

---

## loadJobDefinitions Function

The `loadJobDefinitions` function loads job definitions for a given process definition. It sends a request to the server to get a list of job definitions for the process definition. Then, it iterates over the elements in the process diagram and checks if there are any job definitions for each element. If there are job definitions for an element, it marks the element as selectable and watches for changes in the suspension state of the job definitions.

```javascript
            var loadJobDefinitions = function(_processDefinition) {
              processDefinition = _processDefinition || processDefinition;

              if (!processDefinition) return;

              camAPI
                .resource('job-definition')
                .list({
                  processDefinitionId: processDefinition.id,
                  firstResult: 0,
                  maxResults: 2000
                })
                .then(function(jobDefinitions) {
                  elementRegistry.forEach(function(shape) {
                    var element =
                      processDiagram.bpmnElements[shape.businessObject.id];
                    var definitionsForElement = getElementDefinitions(
                      element,
                      jobDefinitions
                    );

```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/jobDefinition/app/views/processDefinition/diagramPlugins/jobSuspension.js" line="124">

---

## getElementDefinitions Function

The `getElementDefinitions` function filters job definitions for a given element. It returns an array of job definitions that match the ID of the element.

```javascript
            function getElementDefinitions(element, jobDefinitions) {
              return jobDefinitions.filter(function(definition) {
                return definition.activityId === element.id;
              });
            }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
