---
title: Exploring the Tasklist Client
---
The Tasklist Client in the Citi-camunda project refers to the client-side implementation of the tasklist feature. It is responsible for managing and displaying tasks to the user. The client is structured into different directories, each serving a specific purpose. The 'controller' directory contains the logic for handling user interactions and updating the view accordingly. The 'plugins' directory contains additional features that can be added to the tasklist. The 'directives' directory contains AngularJS directives which encapsulate reusable components or modify the behavior of existing components. The 'index.js' file is the entry point for the tasklist client.

The Tasklist Client uses properties such as 'tasklistData' and 'tasklistForm' to manage the state of the tasklist. These properties are bound to the scope of the directives and can be used to pass data between different components of the application.

The Tasklist Client also uses classes like 'task-card' and 'task' to style and structure the tasklist. These classes are used in the HTML templates of the directives and are defined in the associated CSS files.

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/tasklist/index.js" line="1">

---

# Tasklist Client Structure

This is the entry point for the Tasklist Client. It is responsible for initializing the client and loading the necessary modules.

```javascript
/*
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/form/directives/cam-tasklist-form.js" line="307">

---

# Tasklist Form

The `getTasklistForm` function is used to retrieve the current state of the tasklist form. This is used in various parts of the Tasklist Client to interact with the form.

```javascript
        this.getTasklistForm = function() {
          return $scope.tasklistForm;
        };
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/tasklist/directives/cam-tasklist-tasks.js" line="226">

---

# Tasklist Tasks

The `selectNextTask` function is used to select the next task in the tasklist. This is used for navigating through tasks using keyboard shortcuts.

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

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
