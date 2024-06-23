---
title: Understanding the Tasklist Task Component
---
A Tasklist Task in the Citi-camunda project refers to a specific task within the tasklist. It is a key component in the tasklist module, which is part of the frontend UI. The Tasklist Task is defined and manipulated in various JavaScript and HTML files within the tasklist directory. It has properties such as 'tasklistData', 'component', and 'resource', which are used to manage and display task data. The 'task' property is particularly important as it holds the actual task data and is used extensively throughout the codebase. The 'task-card' class in the HTML files is used to style and format the task display on the frontend.

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/task/directives/cam-tasklist-task.js" line="299">

---

## Tasklist Task Directive

The 'cam-tasklist-task' directive is where the Tasklist Task is primarily managed. It defines the scope for the task variables and details. The 'component' property is used to specify the detail view of the task.

```javascript
          $scope.taskVars = {read: ['task', 'taskData', 'errorHandler']};
          $scope.taskDetailTabs = Views.getProviders({
            component: 'tasklist.task.detail'
          });
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/task/directives/cam-tasklist-task.html" line="27">

---

## Tasklist Task Detail View

The HTML template for the Tasklist Task provides the user interface for interacting with the task. It displays the task name, process definition, and case definition, among other details.

```html
          <h2 class="task">{{ task.name || task.taskDefinitionKey || task.id }} </h2>
          <div class="definition-name">
          <h4 class="process-definition"
              ng-if="task.processDefinitionId">
            {{ task._embedded.processDefinition[0].name || task._embedded.processDefinition[0].key }}
              <span ng-if="task._embedded.processDefinition[0].versionTag">(v. {{ task._embedded.processDefinition[0].versionTag }})</span>
            </h4>
          <h4 class="case-definition"
              ng-if="task.caseDefinitionId">
            {{ task._embedded.caseDefinition[0].name || task._embedded.caseDefinition[0].key }}
          </h4>
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/task/directives/cam-tasklist-task-meta.js" line="51">

---

## Tasklist Task Meta

The 'cam-tasklist-task-meta' directive observes changes to the task and updates the scope accordingly. This allows for real-time updates to the task details in the user interface.

```javascript
        taskMetaData.observe('task', function(task) {
          $scope.task = angular.copy(task);
```

---

</SwmSnippet>

# Tasklist Task Functions

This section will provide an overview of the main functions of Tasklist Task, including setLink, setDefaultTaskDetailTab, and dismissTask.

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/task/directives/cam-tasklist-task.js" line="65">

---

## setLink Function

The `setLink` function is used to set the instance link for a task. It checks if the task has a process instance ID or a case instance ID and sets the resource and resource ID accordingly. If the task is standalone, the instance link is set to undefined.

```javascript
          function setLink(task) {
            if (!task) {
              $scope.instanceLink = undefined;
              return;
            }

            var resource = '';
            var resourceId = '';
            var rootElement = $location.search()?.rootElement;

            if (task.processInstanceId) {
              resource = 'process-instance';
              resourceId = task.processInstanceId;
            } else if (task.caseInstanceId) {
              resource = 'case-instance';
              resourceId = task.caseInstanceId;
            } else {
              // standalone task
              $scope.instanceLink = undefined;
              return;
            }
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/task/directives/cam-tasklist-task.js" line="315">

---

## setDefaultTaskDetailTab Function

The `setDefaultTaskDetailTab` function is used to set the default task detail tab. It checks if a tab is selected and if the provider for the tab exists. If not, it sets the selected tab to the first tab in the list.

```javascript
          function setDefaultTaskDetailTab(tabs) {
            var selectedTabId = search().detailsTab;

            if (!tabs || !tabs.length) {
              return;
            }

            if (selectedTabId) {
              var provider = Views.getProvider({
                component: 'tasklist.task.detail',
                id: selectedTabId
              });
              if (provider && tabs.indexOf(provider) != -1) {
                $scope.selectedTaskDetailTab = provider;
                return;
              }
            }

            search.updateSilently({
              detailsTab: null
            });
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/task/directives/cam-tasklist-task.js" line="355">

---

## dismissTask Function

The `dismissTask` function is used to clear the current task. It calls the `clearTask` function with a parameter indicating whether to update the location.

```javascript
          $scope.dismissTask = function() {
            clearTask(true);
          };
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
