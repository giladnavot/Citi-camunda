---
title: Understanding Cockpit UI Tasks
---
Cockpit UI Tasks in Citi-camunda refers to the tasks dashboard in the Cockpit user interface. This dashboard is a part of the Camunda Platform's Cockpit application, which provides a visual interface for workflow and process automation. The tasks dashboard provides a comprehensive view of all tasks, their types, and their assignment groups. It is implemented using AngularJS and is located in the 'webapps/frontend/ui/cockpit/plugins/tasks/app/views/dashboard' directory of the repository. The dashboard is registered as a default view with the id 'task-dashboard' and is configured in the 'main.js' file.

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/tasks/app/views/dashboard/task-dashboard.js" line="24">

---

# Task Dashboard

The task dashboard is registered as a default view in the Cockpit UI. It is identified by the id 'task-dashboard' and is associated with a template and a controller for managing its behavior.

```javascript
  function(ViewsProvider) {
    ViewsProvider.registerDefaultView('cockpit.tasks.dashboard', {
      id: 'task-dashboard',
      label: 'PLUGIN_TASK_DASHBOARD_TITLE',
      template: template,
      controller: [
        '$scope',
        '$q',
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/tasks/app/views/dashboard/task-dashboard.js" line="257">

---

# Task Dashboard Plugins

The task dashboard uses plugins to extend its functionality. These plugins are identified by the component 'cockpit.tasks.dashboard'.

```javascript
          var taskDashboardPlugins = Views.getProviders({
            component: 'cockpit.tasks.dashboard'
          });
          var hasSearchPlugin = ($scope.hasSearchPlugin =
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/tasks/app/views/dashboard/task-dashboard.html" line="1">

---

# Task Dashboard HTML

This is the HTML template for the task dashboard. It defines the structure and layout of the dashboard, including sections for task statistics and task group counts.

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

# Task Dashboard Configuration

The task dashboard is configured as part of the 'cockpit.plugin.tasks.views' module. The configuration includes the task dashboard and its dependencies.

```javascript
  taskDashboard = require('./dashboard/task-dashboard'),
  ngModule = angular.module('cockpit.plugin.tasks.views', []);

ngModule.config(taskDashboard);
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
