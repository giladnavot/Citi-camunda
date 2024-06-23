---
title: Introduction to Tasklist Controller
---
The Tasklist Controller in Citi-camunda is a crucial component that manages the tasks within the application. It is responsible for creating a new tasklist app, setting up the app's vendor and name, and managing user profiles. It also handles app-wide refresh events and manages the lifecycle of these events.

The Tasklist Controller also interacts with the Camunda API to fetch user profiles and handle authentication changes. It provides the functionality to broadcast refresh events at a set interval, ensuring that the tasklist is always up-to-date.

In addition, the Tasklist Controller manages the tasklist data, which includes the current filter, search query, task list query, and task list. It also provides the current task id and the current task. The controller observes changes in the current filter and the task list query, and updates the task list accordingly.

Lastly, the Tasklist Controller listens for route changes and updates the task id and current filter when a route change occurs. This ensures that the displayed tasks are always relevant to the current route.

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/controller/cam-tasklist-app-ctrl.js" line="20">

---

# Tasklist Controller Initialization

The Tasklist Controller is initialized here as `TasklistApp`. It has a property `refreshProvider` which is initially set to null.

```javascript
var TasklistApp = (function() {
  function TasklistApp() {
    this.refreshProvider = null;
  }
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/controller/cam-tasklist-app-ctrl.js" line="34">

---

# Tasklist Controller Usage

The Tasklist Controller is used in the application here. It fetches the user profile and sets up a refresh interval to broadcast a 'refresh' event every 10 seconds.

```javascript
  function(camAPI, configuration, $window, $interval, $scope) {
    // create a new tasklistApp
    $scope.tasklistApp = new TasklistApp();
    $scope.appVendor = configuration.getAppVendor();
    $scope.appName = configuration.getAppName();

    // doing so, there's no `{{ appVendor }} {{ appName }}`
    // visible in the title tag as the app loads
    var htmlTitle = document.querySelector('head > title');
    htmlTitle.textContent = $scope.appVendor + ' ' + $scope.appName;

    function getUserProfile(auth) {
      if (!auth || !auth.name) {
        $scope.userFullName = null;
        return;
      }

      var userService = camAPI.resource('user');
      userService.profile(auth.name, function(err, info) {
        if (err) {
          $scope.userFullName = null;
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/controller/cam-tasklist-view-ctrl.js" line="47">

---

# Tasklist Controller Interaction with Camunda API

The Tasklist Controller interacts with the Camunda API here. It uses the `camAPI` to get resources for 'filter' and 'task'.

```javascript
    var Filter = camAPI.resource('filter');
    var Task = camAPI.resource('task');

```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/controller/cam-tasklist-view-ctrl.js" line="273">

---

# Tasklist Controller Handling Route Changes

The Tasklist Controller handles route changes here. When the route changes, it updates the task id and resets the current filter.

```javascript
    /**
     * Update task if location changes
     */
    $scope.$on('$routeChanged', function() {
      var oldTaskId = taskId;
      var oldDetailsTab = detailsTab;

      taskId = getPropertyFromLocation('task');
      detailsTab = getPropertyFromLocation('detailsTab');

      if (oldTaskId !== taskId || oldDetailsTab === detailsTab) {
        tasklistData.set('taskId', {taskId: taskId});
      }

      currentFilter = null;
      tasklistData.changed('currentFilter');
    });
```

---

</SwmSnippet>

# Tasklist Controller Functions

Let's delve into the key functions of the Tasklist Controller.

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/controller/cam-tasklist-view-ctrl.js" line="45">

---

## getUserProfile Function

The `getUserProfile` function retrieves the user's profile using the `camAPI` resource. It takes the `auth` object as an argument, checks if it exists and if it has a `name` property. If it does, it calls the `userService.profile` method with `auth.name` as an argument to get the user's profile information.

```javascript

    // resources
    var Filter = camAPI.resource('filter');
    var Task = camAPI.resource('task');

    // current selected filter
    var currentFilter;

    // provide /////////////////////////////////////////////////////////////////////////////////

    /**
     * Provides the list of filters
     */
    tasklistData.provide('filters', function() {
      var deferred = $q.defer();
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/controller/cam-tasklist-view-ctrl.js" line="68">

---

## refreshInterval Function

The `refreshInterval` function triggers a refresh event every 10 seconds. This is used to keep the task list up-to-date in real-time. The `$interval` service is used to schedule the refresh event.

```javascript
          var pages = Math.ceil(count / paginationSize);
          var requests = [];
          for (var i = 0; i < pages; i++) {
            requests.push(
              Filter.list({
                firstResult: i * paginationSize,
                maxResults: paginationSize,
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/controller/cam-tasklist-view-ctrl.js" line="58">

---

## tasklistData.provide Function

The `tasklistData.provide` function is used to provide data for the task list. It uses the `Filter` resource from `camAPI` to get the list of filters. It also handles errors and returns a promise.

```javascript
    tasklistData.provide('filters', function() {
      var deferred = $q.defer();

      Filter.count({
        itemCount: false,
        resourceType: 'Task'
      })
        .then(function(count) {
          var paginationSize = 2000;

          var pages = Math.ceil(count / paginationSize);
          var requests = [];
          for (var i = 0; i < pages; i++) {
            requests.push(
              Filter.list({
                firstResult: i * paginationSize,
                maxResults: paginationSize,
                itemCount: false,
                resourceType: 'Task'
              })
            );
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
