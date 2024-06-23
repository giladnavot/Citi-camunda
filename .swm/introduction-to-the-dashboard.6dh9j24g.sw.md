---
title: Introduction to the Dashboard
---
The Dashboard in Citi-camunda is a user interface component that provides a consolidated view of various metrics and information. It is implemented in the <SwmPath>[webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js](/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js)</SwmPath> file, and it includes properties like <SwmToken path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" pos="107:1:1" line-data="      actual: {}">`actual`</SwmToken>, <SwmToken path="/spin/dataformat-xml-dom/src/test/resources/org/camunda/spin/javascript/xml/dom/XmlDomElementScriptTest.getAllAttributesAndNamesByNamespace.js" pos="3:0:0" line-data="names = xml.attrNames(namespace)">`names`</SwmToken>, <SwmToken path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" pos="262:1:1" line-data="                        assigned: true">`assigned`</SwmToken>, <SwmToken path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" pos="271:1:1" line-data="                          value: value">`value`</SwmToken>, <SwmToken path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" pos="261:1:1" line-data="                        unfinished: true,">`unfinished`</SwmToken>, <SwmToken path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" pos="125:9:9" line-data="      var treshold = valuesTreshold(values.length, total);">`values`</SwmToken>, and <SwmToken path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" pos="20:2:2" line-data="var template = require(&#39;./dashboard.html?raw&#39;);">`template`</SwmToken>. The Dashboard also includes a <SwmToken path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" pos="248:1:1" line-data="          tasks: function(next) {">`tasks`</SwmToken> function that counts tasks and prepares values for display. The Dashboard is rendered using the <SwmPath>[webapps/frontend/ui/admin/client/scripts/pages/dashboard.html](/webapps/frontend/ui/admin/client/scripts/pages/dashboard.html)</SwmPath> template, and its styles are defined in the <SwmPath>[webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.less](/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.less)</SwmPath> file.

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

The Dashboard includes a <SwmToken path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" pos="248:1:1" line-data="          tasks: function(next) {">`tasks`</SwmToken> function that fetches and processes task-related data. This data includes the total number of tasks, tasks assigned to users, tasks assigned to groups, and unassigned tasks.

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

The Dashboard includes a <SwmToken path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" pos="237:1:1" line-data="          processes: function(next) {">`processes`</SwmToken> function that observes and processes process-related data. This data includes process instances and incidents.

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

The Dashboard in the Citi-camunda project is a crucial component that provides a visual representation of the workflow and process automation. It is implemented in several files, mainly in the <SwmPath>[webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js](/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js)</SwmPath> and <SwmPath>[webapps/frontend/ui/admin/client/scripts/pages/dashboard.html](/webapps/frontend/ui/admin/client/scripts/pages/dashboard.html)</SwmPath> files. The dashboard contains several functions and properties that contribute to its functionality.

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" line="46">

---

## <SwmToken path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" pos="46:2:2" line-data="function valuesTreshold(l, t) {">`valuesTreshold`</SwmToken> Function

The <SwmToken path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" pos="46:2:2" line-data="function valuesTreshold(l, t) {">`valuesTreshold`</SwmToken> function is used to calculate a threshold value based on the length of the values and the total. It is used within the <SwmToken path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" pos="124:3:3" line-data="    function prepareValues(values, total, url) {">`prepareValues`</SwmToken> function.

```javascript
function valuesTreshold(l, t) {
  return l > 12 ? Math.floor(t / l) * 0.5 : 0;
}
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" line="124">

---

## <SwmToken path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" pos="124:3:3" line-data="    function prepareValues(values, total, url) {">`prepareValues`</SwmToken> Function

The <SwmToken path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" pos="124:3:3" line-data="    function prepareValues(values, total, url) {">`prepareValues`</SwmToken> function is used to prepare the values for the dashboard. It uses the <SwmToken path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" pos="125:7:7" line-data="      var treshold = valuesTreshold(values.length, total);">`valuesTreshold`</SwmToken> function to calculate a threshold and then filters the values based on this threshold.

```javascript
    function prepareValues(values, total, url) {
      var treshold = valuesTreshold(values.length, total);
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" line="237">

---

## processes Function

The <SwmToken path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" pos="237:1:1" line-data="          processes: function(next) {">`processes`</SwmToken> function is used to aggregate instances and incidents of process definitions. It is used in the <SwmPath>[clients/java/qa/engine-variable-test/src/main/resources/META-INF/processes.xml](/clients/java/qa/engine-variable-test/src/main/resources/META-INF/processes.xml)</SwmPath> file and the '[README.md](http://README.md)' file.

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

The <SwmToken path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" pos="248:1:1" line-data="          tasks: function(next) {">`tasks`</SwmToken> function is used to count the total tasks and categorize them into assigned to user, assigned to group, and unassigned tasks. It is used in the <SwmPath>[webapps/frontend/ui/admin/client/scripts/pages/dashboard.html](/webapps/frontend/ui/admin/client/scripts/pages/dashboard.html)</SwmPath> file.

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

## <SwmToken path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" pos="258:1:1" line-data="                  assignedToUser: function(done) {">`assignedToUser`</SwmToken> Function

The <SwmToken path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" pos="258:1:1" line-data="                  assignedToUser: function(done) {">`assignedToUser`</SwmToken> function is a part of the <SwmToken path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" pos="248:1:1" line-data="          tasks: function(next) {">`tasks`</SwmToken> function. It is used to count the tasks that are assigned to a user.

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

The <SwmToken path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" pos="295:1:1" line-data="                  unassigned: function(done) {">`unassigned`</SwmToken> function is a part of the <SwmToken path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" pos="248:1:1" line-data="          tasks: function(next) {">`tasks`</SwmToken> function. It is used to count the tasks that are unassigned.

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

## <SwmToken path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" pos="344:1:1" line-data="          processDefinitions: function(next) {">`processDefinitions`</SwmToken> Function

The <SwmToken path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" pos="344:1:1" line-data="          processDefinitions: function(next) {">`processDefinitions`</SwmToken> function is used to count the process definitions. It is used in the <SwmPath>[webapps/frontend/ui/admin/client/scripts/pages/dashboard.html](/webapps/frontend/ui/admin/client/scripts/pages/dashboard.html)</SwmPath> file.

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

## <SwmToken path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" pos="352:1:1" line-data="          decisionDefinitions: function(next) {">`decisionDefinitions`</SwmToken> Function

The <SwmToken path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" pos="352:1:1" line-data="          decisionDefinitions: function(next) {">`decisionDefinitions`</SwmToken> function is used to count the decision definitions. It is used in the <SwmPath>[webapps/frontend/ui/admin/client/scripts/pages/dashboard.html](/webapps/frontend/ui/admin/client/scripts/pages/dashboard.html)</SwmPath> file.

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

## <SwmToken path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" pos="360:1:1" line-data="          caseDefinitions: function(next) {">`caseDefinitions`</SwmToken> Function

The <SwmToken path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" pos="360:1:1" line-data="          caseDefinitions: function(next) {">`caseDefinitions`</SwmToken> function is used to count the case definitions. It is used in the <SwmPath>[webapps/frontend/ui/admin/client/scripts/pages/dashboard.html](/webapps/frontend/ui/admin/client/scripts/pages/dashboard.html)</SwmPath> file.

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

## <SwmToken path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" pos="368:1:1" line-data="          deploymentDefinitions: function(next) {">`deploymentDefinitions`</SwmToken> Function

The <SwmToken path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" pos="368:1:1" line-data="          deploymentDefinitions: function(next) {">`deploymentDefinitions`</SwmToken> function is used to count the deployment definitions. It is used in the <SwmPath>[webapps/frontend/ui/admin/client/scripts/pages/dashboard.html](/webapps/frontend/ui/admin/client/scripts/pages/dashboard.html)</SwmPath> file.

```javascript
          deploymentDefinitions: function(next) {
            deploymentResource.count({}, next);
          }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda"><sup>Powered by [Swimm](https://app.swimm.io/)</sup></SwmMeta>
