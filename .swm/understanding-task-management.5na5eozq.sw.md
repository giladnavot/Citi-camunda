---
title: Understanding Task Management
---
Task Management in Citi-camunda refers to the functionality of managing and monitoring tasks within the workflow process. It involves tracking task assignment, status, and completion. The task dashboard provides a visual representation of task statistics, including the number of tasks assigned to users, groups, and unassigned tasks. It also provides the ability to search for tasks based on different criteria.

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/tasks/app/views/dashboard/task-dashboard.js" line="20">

---

## Task Dashboard Module

This is the main module for task management. It registers a view for the task dashboard, defines the data to be displayed, and provides the functionality for fetching and observing task data.

```javascript
var template = require('./task-dashboard.html?raw');

module.exports = [
  'ViewsProvider',
  function(ViewsProvider) {
    ViewsProvider.registerDefaultView('cockpit.tasks.dashboard', {
      id: 'task-dashboard',
      label: 'PLUGIN_TASK_DASHBOARD_TITLE',
      template: template,
      controller: [
        '$scope',
        '$q',
        'Views',
        'camAPI',
        'dataDepend',
        'search',
        'Notifications',
        '$translate',
        function(
          $scope,
          $q,
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/tasks/app/views/dashboard/task-dashboard.js" line="53">

---

## Task Statistics

This section of the code defines the task statistics to be displayed on the dashboard. It includes the count of tasks assigned to users, groups, and unassigned tasks.

```javascript
          $scope.taskStatistics = [
            {
              // assigned to users
              state: undefined,
              label: $translate.instant('PLUGIN_TASK_ASSIGNED_TO_USER'),
              count: 0,
              search: 'openAssignedTasks'
            },
            {
              // assigned to groups
              state: undefined,
              label: $translate.instant('PLUGIN_TASK_ASSIGNED_TO_ONE'),
              count: 0,
              search: 'openGroupTasks'
            },
            {
              // assigned neither to groups nor to users
              state: undefined,
              label: $translate.instant('PLUGIN_TASK_ASSIGNED_UNASSIGNED'),
              count: 0,
              search: 'openUnassignedTasks'
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/tasks/app/views/dashboard/task-dashboard.js" line="126">

---

## Task Data Providers

This section of the code defines the data providers for the task statistics. It fetches the count of tasks based on different criteria such as 'openTaskCount', 'assignedToUserCount', 'assignedToGroupCount', and 'notAssignedCount'.

```javascript
          tasksPluginData.provide('openTaskCount', function() {
            return provideResourceData(
              $translate.instant('PLUGIN_TASK_ERROR_OPEN_TASKS'),
              HistoryResource,
              'taskCount',
              defaultParameter()
            );
          });

          tasksPluginData.provide('assignedToUserCount', function() {
            var params = defaultParameter();
            params.assigned = true;
            return provideResourceData(
              $translate.instant('PLUGIN_TASK_ERROR_ASSIGNED_TO_USERS'),
              HistoryResource,
              'taskCount',
              params
            );
          });

          tasksPluginData.provide('assignedToGroupCount', function() {
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/tasks/app/views/dashboard/task-dashboard.js" line="216">

---

## Task Data Observers

This section of the code sets up observers for the task data. These observers update the task statistics on the dashboard whenever the task data changes.

```javascript
          $scope.openTasksState = tasksPluginData.observe(
            ['openTaskCount'],
            function(_count) {
              $scope.openTasksCount = _count.count || 0;
            }
          );

          $scope.taskStatistics[0].state = tasksPluginData.observe(
            ['assignedToUserCount'],
            function(_userCount) {
              $scope.taskStatistics[0].count = _userCount.count || 0;
            }
          );

          $scope.taskStatistics[1].state = tasksPluginData.observe(
            ['assignedToGroupCount'],
            function(_groupCount) {
              $scope.taskStatistics[1].count = _groupCount.count || 0;
            }
          );

```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/tasks/app/views/dashboard/task-dashboard.html" line="2">

---

## Task Dashboard View

This is the HTML template for the task dashboard. It displays the task statistics and provides links for filtering tasks based on specific criteria.

```html
<div class="dashboard-row">
  <section class="col-xs-12 col-md-6">
    <div class="inner">
      <header>
        <h1 class="section-title">{{ 'PLUGIN_TASK_ASSIGNMENT_BY_TYPE' | translate }}</h1>
      </header>
      <table class="cam-table values-left" id="open-task-statistics">
        <thead>
          <tr>
            <th>{{ 'PLUGIN_TASK_TASKS' | translate }}</th>
            <th>{{ 'PLUGIN_TASK_TYPES' | translate }}</th>
          </tr>
        </thead>

        <tfoot>
          <tr>
            <th>
              <span ng-if="!openTasksState.$loaded" class="glyphicon glyphicon-refresh animate-spin"></span>
              <span ng-if="openTasksState.$loaded && !hasSearchPlugin">{{ openTasksCount }}</span>
              <span ng-if="openTasksState.$loaded && hasSearchPlugin">
                <a class="search-link" ng-click="createSearch('allOpenTasks', 'statistics')">{{ openTasksCount }}</a>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
