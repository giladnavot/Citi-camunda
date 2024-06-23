---
title: Introduction to the Dashboard
---
The Dashboard in Citi-camunda is a user interface component that provides a consolidated view of various metrics and information. It is implemented in the `dashboard.js` file, and it includes properties like `actual`, `names`, `assigned`, `value`, `unfinished`, `values`, and `template`. The Dashboard also includes a `tasks` function that counts tasks and prepares values for display. The Dashboard is rendered using the `dashboard.html` template, and its styles are defined in the `dashboard.less` file.

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" line="20">

---

# Dashboard Structure

The Dashboard is implemented as a module in the Cockpit client. It is required and used in the main script of the application.

```javascript
var template = require('./dashboard.html?raw');
var series = require('camunda-bpm-sdk-js').utils.series;

```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" line="106">

---

# Dashboard Data

The Dashboard maintains a data object that holds the actual data to be displayed. This data is fetched and processed from various sources.

```javascript
    $scope.data = {
      actual: {}
    };
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" line="248">

---

# Dashboard Tasks

The Dashboard includes a `tasks` function that fetches and processes task-related data. This data includes the total number of tasks, tasks assigned to users, tasks assigned to groups, and unassigned tasks.

```javascript
          tasks: function(next) {
            taskResource.count({}, function(err, total) {
              if (err) {
                return next();
              }

              $scope.data.actual.tasks = total;

              series(
                {
                  assignedToUser: function(done) {
                    taskResource.count(
                      {
                        unfinished: true,
                        assigned: true
                      },
                      function(err, value) {
                        done(err, {
                          label: $translate.instant(
                            'DASHBOARD_ASSIGNED_TO_USER'
                          ),
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" line="237">

---

# Dashboard Processes

The Dashboard includes a `processes` function that observes and processes process-related data. This data includes process instances and incidents.

```javascript
          processes: function(next) {
            processData.observe(
              'processDefinitionWithRootIncidentsStatistics',
              function(processDefinitionStatistics) {
                aggregateInstances(processDefinitionStatistics);
                aggregateIncidents(processDefinitionStatistics);
              }
            );

            next();
          },
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" line="424">

---

# Dashboard Route

The Dashboard is accessed through the '/dashboard' route in the application. This route is associated with the Dashboard's template and controller, and requires authentication.

```javascript
    $routeProvider.when('/dashboard', {
      template: template,
      controller: Controller,
      authentication: 'required',
      reloadOnSearch: false
```

---

</SwmSnippet>

# Dashboard Functions

The Dashboard in the Citi-camunda project is a crucial component that provides a visual representation of the workflow and process automation. It is implemented in several files, mainly in the 'dashboard.js' and 'dashboard.html' files. The dashboard contains several functions and properties that contribute to its functionality.

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" line="46">

---

## valuesTreshold Function

The `valuesTreshold` function is used to calculate a threshold value based on the length of the values and the total. It is used within the `prepareValues` function.

```javascript
function valuesTreshold(l, t) {
  return l > 12 ? Math.floor(t / l) * 0.5 : 0;
}
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" line="124">

---

## prepareValues Function

The `prepareValues` function is used to prepare the values for the dashboard. It uses the `valuesTreshold` function to calculate a threshold and then filters the values based on this threshold.

```javascript
    function prepareValues(values, total, url) {
      var treshold = valuesTreshold(values.length, total);
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" line="237">

---

## processes Function

The `processes` function is used to aggregate instances and incidents of process definitions. It is used in the 'processes.xml' file and the '[README.md](http://README.md)' file.

```javascript
          processes: function(next) {
            processData.observe(
              'processDefinitionWithRootIncidentsStatistics',
              function(processDefinitionStatistics) {
                aggregateInstances(processDefinitionStatistics);
                aggregateIncidents(processDefinitionStatistics);
              }
            );

            next();
          },
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" line="248">

---

## tasks Function

The `tasks` function is used to count the total tasks and categorize them into assigned to user, assigned to group, and unassigned tasks. It is used in the 'dashboard.html' file.

```javascript
          tasks: function(next) {
            taskResource.count({}, function(err, total) {
              if (err) {
                return next();
              }

              $scope.data.actual.tasks = total;

              series(
                {
                  assignedToUser: function(done) {
                    taskResource.count(
                      {
                        unfinished: true,
                        assigned: true
                      },
                      function(err, value) {
                        done(err, {
                          label: $translate.instant(
                            'DASHBOARD_ASSIGNED_TO_USER'
                          ),
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" line="258">

---

## assignedToUser Function

The `assignedToUser` function is a part of the `tasks` function. It is used to count the tasks that are assigned to a user.

```javascript
                  assignedToUser: function(done) {
                    taskResource.count(
                      {
                        unfinished: true,
                        assigned: true
                      },
                      function(err, value) {
                        done(err, {
                          label: $translate.instant(
                            'DASHBOARD_ASSIGNED_TO_USER'
                          ),
                          url:
                            '/tasks?searchQuery=%5B%7B%22type%22:%22unfinished%22,%22operator%22:%22eq%22,%22value%22:%22%22,%22name%22:%22%22%7D,%7B%22type%22:%22assigned%22,%22operator%22:%22eq%22,%22value%22:%22%22,%22name%22:%22%22%7D%5D',
                          value: value
                        });
                      }
                    );
                  },
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" line="295">

---

## unassigned Function

The `unassigned` function is a part of the `tasks` function. It is used to count the tasks that are unassigned.

```javascript
                  unassigned: function(done) {
                    taskResource.count(
                      {
                        unfinished: true,
                        unassigned: true,
                        withoutCandidateGroups: true
                      },
                      function(err, value) {
                        done(err, {
                          label: $translate.instant('DASHBOARD_UNASSIGNED'),
                          url:
                            '/tasks?searchQuery=%5B%7B%22type%22:%22unfinished%22,%22operator%22:%22eq%22,%22value%22:%22%22,%22name%22:%22%22%7D,%7B%22type%22:%22withoutCandidateGroups%22,%22operator%22:%22eq%22,%22value%22:%22%22,%22name%22:%22%22%7D,%7B%22type%22:%22unassigned%22,%22operator%22:%22eq%22,%22value%22:%22%22,%22name%22:%22%22%7D%5D',
                          value: value
                        });
                      }
                    );
                  }
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" line="344">

---

## processDefinitions Function

The `processDefinitions` function is used to count the process definitions. It is used in the 'dashboard.html' file.

```javascript
          processDefinitions: function(next) {
            processDefinitionService.count(
              {
                latestVersion: true
              },
              next
            );
          },
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" line="352">

---

## decisionDefinitions Function

The `decisionDefinitions` function is used to count the decision definitions. It is used in the 'dashboard.html' file.

```javascript
          decisionDefinitions: function(next) {
            decisionDefResource.count(
              {
                latestVersion: true
              },
              next
            );
          },
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" line="360">

---

## caseDefinitions Function

The `caseDefinitions` function is used to count the case definitions. It is used in the 'dashboard.html' file.

```javascript
          caseDefinitions: function(next) {
            caseDefResource.count(
              {
                latestVersion: true
              },
              next
            );
          },
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" line="368">

---

## deploymentDefinitions Function

The `deploymentDefinitions` function is used to count the deployment definitions. It is used in the 'dashboard.html' file.

```javascript
          deploymentDefinitions: function(next) {
            deploymentResource.count({}, next);
          }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
