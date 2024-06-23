---
title: Introduction to the Tasklist Feature
---
Tasklist in Citi-camunda refers to a feature that manages and displays tasks. It is a crucial part of the workflow and process automation, allowing users to view, navigate, and interact with tasks. The tasklist is implemented using AngularJS directives and services, and it includes functionalities such as task selection, pagination, and focus management. It also interacts with the task data and form data, which are encapsulated in properties like 'tasklistData' and 'tasklistForm'.

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/form/directives/cam-tasklist-form.js" line="44">

---

## Tasklist Form

The `tasklistForm` property is used to bind data to the form. It is used in conjunction with the `getTasklistForm` function to retrieve the current form data.

```javascript
    scope: {
      tasklistForm: '=',

      /*
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/tasklist/directives/cam-tasklist-tasks.js" line="28">

---

## Tasklist Data

The `tasklistData` property is used to bind data to the tasklist. It is used in various functions to manipulate and update task data.

```javascript
      restrict: 'A',
      scope: {
        tasklistData: '='
      },
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/tasklist/directives/cam-tasklist-tasks.js" line="226">

---

## Task Selection and Navigation

The `selectNextTask` function is used to navigate through tasks. It selects the next task in the list and focuses on it. If the end of the list is reached, it triggers a page change to load the next set of tasks.

```javascript
          var selectNextTask = function() {
            for (var i = 0; i < $scope.tasks.length - 1; i++) {
              if ($scope.tasks[i].id === $scope.currentTaskId) {
                return $scope.focus(null, $scope.tasks[i + 1]);
              }
            }
            if (
              $scope.pageNum < Math.ceil($scope.totalItems / $scope.pageSize)
            ) {
              $scope.pageNum++;
              $scope.pageChange();
              postLoadingJobs.push(function() {
                // wait until the html is applied so you can focus the html element
                $timeout(function() {
                  $scope.focus(null, $scope.tasks[0]);
                });
              });
            }
          };
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/tasklist/directives/cam-tasklist-tasks.js" line="205">

---

## Task Focus

The `focus` function is used to focus on a specific task. It updates the current task ID and updates the URL to reflect the selected task.

```javascript
          $scope.focus = function($event, task) {
            if ($event) {
              $event.preventDefault();
            }

            var taskId = task.id;
            tasksData.set('taskId', {taskId: taskId});
            $scope.currentTaskId = taskId;

            var searchParams = $location.search() || {};
            searchParams.task = taskId;
            updateSilently(searchParams);

            var el = document.querySelector(
              '[cam-tasks] .tasks-list .task [href*="#/?task=' + taskId + '"]'
            );
            if (el) {
              el.focus();
            }
          };
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/tasklist/directives/cam-tasklist-tasks.js" line="296">

---

## Task Pagination

The `pageChange` function is used to handle pagination. It updates the query and triggers a change in the task list query.

```javascript
          /**
           * invoked when pagination is changed
           */
          $scope.pageChange = function() {
            // update query
            updateSilently({
              page: $scope.pageNum
            });
            tasksData.changed('taskListQuery');
          };
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
