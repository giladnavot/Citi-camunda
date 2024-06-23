---
title: Exploration of Cockpit UI Components
---
Cockpit UI Components in Citi-camunda refer to the visual elements that make up the user interface of the Cockpit application. These components are primarily built using AngularJS and are organized in a modular fashion. They include various views, such as task dashboards, which are defined in JavaScript files and associated with HTML templates for rendering the UI. The components are registered and configured using Angular's module system, allowing them to be reused and combined to create complex UI structures.

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/tasks/app/views/dashboard/task-dashboard.js" line="257">

---

# Task Dashboard Component

Here, the `taskDashboard` component is defined. It is registered under the name 'cockpit.tasks.dashboard'.

```javascript
          var taskDashboardPlugins = Views.getProviders({
            component: 'cockpit.tasks.dashboard'
          });
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/tasks/app/views/dashboard/task-dashboard.html" line="1">

---

# Task Dashboard HTML Template

This is the HTML template for the `taskDashboard` component. It uses AngularJS directives to bind data to the UI and display task statistics.

```html
<!-- # CE - ui/cockpit/plugins/tasks/app/views/dashboard/task-dashboard.html -->
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
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/tasks/app/views/main.js" line="22">

---

# Registering the Task Dashboard Component

The `taskDashboard` component is registered using the `ngModule` object. This makes the component available for use within the Cockpit application.

```javascript
  taskDashboard = require('./dashboard/task-dashboard'),
  ngModule = angular.module('cockpit.plugin.tasks.views', []);

ngModule.config(taskDashboard);
```

---

</SwmSnippet>

# Cockpit UI Components Functions

The Cockpit UI components in the Citi-camunda project provide a user interface for managing tasks. The task-dashboard component is a key part of this, providing a visual representation of tasks and their status.

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/tasks/app/views/dashboard/task-dashboard.js" line="23">

---

## ViewsProvider

The `ViewsProvider` is used to register the default view for the task dashboard. It defines the ID and label for the view.

```javascript
  'ViewsProvider',
  function(ViewsProvider) {
    ViewsProvider.registerDefaultView('cockpit.tasks.dashboard', {
      id: 'task-dashboard',
      label: 'PLUGIN_TASK_DASHBOARD_TITLE',
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/tasks/app/views/dashboard/task-dashboard.js" line="257">

---

## Component

The `component` property is used to get the providers for the task dashboard. It is used in conjunction with the `Views` object to retrieve the plugins for the task dashboard.

```javascript
          var taskDashboardPlugins = Views.getProviders({
            component: 'cockpit.tasks.dashboard'
          });
          var hasSearchPlugin = ($scope.hasSearchPlugin =
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/tasks/app/views/main.js" line="21">

---

## ngModule

The `ngModule` is an Angular module that is used to configure the task dashboard. It requires the task dashboard and configures it using the `taskDashboard` function.

```javascript
  // dashboard
  taskDashboard = require('./dashboard/task-dashboard'),
  ngModule = angular.module('cockpit.plugin.tasks.views', []);

ngModule.config(taskDashboard);
```

---

</SwmSnippet>

# Task Dashboard Endpoints

Understanding Task Dashboard Endpoints

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/tasks/app/views/dashboard/task-dashboard.js" line="126">

---

## openTaskCount Endpoint

The `openTaskCount` endpoint is used to fetch the count of open tasks. It uses the `provideResourceData` function to interact with the Camunda API and fetch the required data.

```javascript
          tasksPluginData.provide('openTaskCount', function() {
            return provideResourceData(
              $translate.instant('PLUGIN_TASK_ERROR_OPEN_TASKS'),
              HistoryResource,
              'taskCount',
              defaultParameter()
            );
          });
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/tasks/app/views/dashboard/task-dashboard.js" line="135">

---

## assignedToUserCount Endpoint

The `assignedToUserCount` endpoint is used to fetch the count of tasks assigned to users. It also uses the `provideResourceData` function to interact with the Camunda API and fetch the required data.

```javascript
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
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
