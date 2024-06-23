---
title: Introduction to Tasklist Sorting
---
Tasklist Sorting refers to the functionality that allows users to sort tasks in the tasklist based on different criteria. This is achieved through the 'tasklist-sorting' plugin, which provides a dropdown and inputs for users to select their sorting preferences. The sorting choices are then passed as 'tasklistData' to the 'cam-sorting-choices' component. The sorting order and criteria, represented by 'sortOrder' and 'sortBy' respectively, are used to sort the tasks.

<SwmSnippet path="/webapps/frontend/ui/tasklist/plugins/tasklistSorting/app/tasklistHeader/main.js" line="24">

---

## Tasklist Sorting Plugin

The tasklistSortingPlugin is required in the main.js file. This plugin is responsible for providing the tasklist sorting functionality.

```javascript
  tasklistSortingPlugin = require('./tasklist-sorting');
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/plugins/tasklistSorting/app/tasklistHeader/cam-tasklist-sorting-choices.js" line="29">

---

## Sorting Criteria

The 'sortBy' and 'sortOrder' properties are used to specify the sorting criteria. 'sortBy' determines the attribute by which the tasks are sorted, while 'sortOrder' determines the order (ascending or descending) of the sort.

```javascript
        sortBy: sorting.by,
        sortOrder: sorting.order
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/plugins/tasklistSorting/app/tasklistHeader/tasklist-sorting.js" line="20">

---

## Tasklist Sorting Configuration

The Configuration function registers the 'tasklist-sorting' view with the ViewsProvider. The 'template' property specifies the HTML template to be used for the sorting choices, and the 'priority' property determines the order in which the views are rendered.

```javascript
var Configuration = function PluginConfiguration(ViewsProvider) {
  ViewsProvider.registerDefaultView('tasklist.header', {
    id: 'tasklist-sorting',
    template: '<div cam-sorting-choices tasklist-data="tasklistData"></div>',
    controller: function() {},
    priority: 200
  });
```

---

</SwmSnippet>

# Tasklist Sorting Functions

This section provides an overview of the key functions involved in the Tasklist Sorting functionality.

<SwmSnippet path="/webapps/frontend/ui/tasklist/plugins/tasklistSorting/app/tasklistHeader/cam-tasklist-sorting-choices.js" line="25">

---

## Function: stringifySortings

The `stringifySortings` function is used to convert the sorting query into a JSON string. It maps through each sorting object, checks if the 'by' property contains 'Variable', and if so, ensures that sorting parameters are provided. The function is used within the `updateSortings` function to update the sorting silently.

```javascript
function stringifySortings(sortingQuery) {
  return JSON.stringify(
    sortingQuery.map(function(sorting) {
      var obj = {
        sortBy: sorting.by,
        sortOrder: sorting.order
      };

      if (sorting.by.indexOf('Variable') > -1) {
        if (!sorting.parameters) {
          throw new Error('Variable sorting needs parameters');
        }
        obj.parameters = sorting.parameters;
      }

      return obj;
    })
  );
}
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/plugins/tasklistSorting/app/tasklistHeader/cam-tasklist-sorting-choices.js" line="314">

---

## Function: removeSorting

The `removeSorting` function is invoked when a sorting object needs to be removed. It removes the sorting object at a given index and updates the sortings. It also sets the focus on the appropriate element after the sorting object is removed.

```javascript
        /**
         * Invoked when removing a sorting object
         */
        scope.removeSorting = function(index) {
          scope.sortings.splice(index, 1);
          scope.updateSortings();

          $timeout(function() {
            var element;
            if (scope.sortings.length !== index) {
              element = document.querySelector(
                '[cam-sorting-choices] li.sorting-choice:nth-child(0n+' +
                  (index + 1) +
                  ') a:first-child'
              );
            } else {
              element = document.querySelector(
                '[cam-sorting-choices] li.sorting-choice:nth-last-child(0n+2) a:first-child'
              );
            }
            if (element) {
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/plugins/tasklistSorting/app/tasklistHeader/cam-tasklist-sorting-choices.js" line="267">

---

## Function: updateSortings

The `updateSortings` function is used to update the sortings. It resets the `openDropdowns` array and updates the `sortedOn` array with the 'by' property of each sorting. It then updates the sorting silently using the `stringifySortings` function and triggers the 'taskListQuery' change in `tasklistData`.

```javascript
        // should NOT manipulate the `scope.sortings`!
        scope.updateSortings = function() {
          scope.openDropdowns = [];
          scope.sortedOn = scope.sortings.map(function(sorting) {
            scope.openDropdowns.push(false);
            return sorting.by;
          });

          search.updateSilently({
            sorting: stringifySortings(scope.sortings)
          });

          tasklistData.changed('taskListQuery');

          updateColumns();
        };
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
