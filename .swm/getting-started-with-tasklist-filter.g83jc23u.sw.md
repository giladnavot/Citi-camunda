---
title: Getting Started with Tasklist Filter
---
The Tasklist Filter in Citi-camunda refers to a feature that allows users to sort and categorize tasks based on certain criteria. It is a key component in the tasklist module, which is responsible for managing and displaying tasks. The filter property is used to update the tasklist silently with the filter id. The filtersData property is used to bind data to the filter directive. The description property provides a brief explanation of the filter, while the query property is used to specify the filter criteria. The resourceType property indicates the type of resource the filter is applied to, in this case, 'Task'. The item class is used in various contexts, mainly to style and manipulate filter items. The $scope field is used to bind data and functions to the view and the controller. The total property is used to keep track of the total number of items in a page. The priority property is used to determine the order of filters.

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/filter/directives/cam-tasklist-filters.js" line="125">

---

## Using the Tasklist Filter

Here, the `filter` property is used to update the tasklist silently with the selected filter id. This is how the filter is applied to the tasklist.

```javascript
            search.updateSilently({
              filter: filter.id
            });
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/filter/directives/cam-tasklist-filters.html" line="29">

---

## Displaying the Filtered Tasks

This code snippet shows how the filtered tasks are displayed. The `filter` object is used in a `ng-repeat` directive to iterate over the filtered tasks and display each one.

```html
  <div ng-show="totalItems"
       ng-repeat="(delta, filter) in filters"
       class="item task-filter cells-wrapper"
       ng-class="{active: isFocused(filter)}"
       ng-style="filter.style"
       ng-click="focus(filter)">

    <h4 class="name"
        uib-tooltip="{{ filter.properties.description }}"
        tooltip-placement="top">
      <a href
         ng-style="{color: filter.properties.color}">
        {{ filter.name }}

        <span ng-show="isFocused(filter)"
              class="counter">{{ filterCount }}</span>
      </a>
    </h4>
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/filter/directives/cam-tasklist-filters.js" line="146">

---

## Creating a New Filter

This code snippet shows how a new filter is created. The `name`, `resourceType`, `query`, and `properties` fields are set for the new filter.

```javascript
                var payload = {
                  name: translated,
                  resourceType: 'Task',
                  query: {},
                  properties: {
                    description: 'Unfiltered Tasks',
```

---

</SwmSnippet>

# Tasklist Filter Functions

Let's delve into the main functions of the Tasklist Filter.

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/filter/directives/cam-tasklist-filters.js" line="54">

---

## updateView Function

The `updateView` function is used to update the view of the filters. It slices the filters based on the current page and page size, and then silently updates the search filter page.

```javascript
          function updateView() {
            $scope.filters = $scope.allFilters.slice(
              (page.current - 1) * page.size,
              page.current * page.size
            );
            search.updateSilently({
              filterPage: page.current === 1 ? null : page.current
            });
          }
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/filter/directives/cam-tasklist-filters.js" line="122">

---

## focus Function

The `focus` function is used to select a filter. It sets the filter count to undefined and silently updates the search filter with the selected filter's id.

```javascript
          $scope.focus = function(filter) {
            $scope.filterCount = undefined;

            search.updateSilently({
              filter: filter.id
            });

            filtersData.changed('currentFilter');
          };
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/filter/directives/cam-tasklist-filters.js" line="135">

---

## isFocused Function

The `isFocused` function checks if the provided filter is the currently focused filter. It returns true if the id of the provided filter matches the id of the current filter.

```javascript
          $scope.isFocused = function(filter) {
            return filter.id === $scope.currentFilter.id;
          };
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/filter/directives/cam-tasklist-filters.js" line="143">

---

## addAllFilter Function

The `addAllFilter` function is used to add an initial 'All' filter. It creates a payload with the filter properties and then creates a filter resource with the payload. If there's an error, it adds an error notification.

```javascript
          $scope.addAllFilter = function() {
            return $translate('ALL_TASKS')
              .then(function(translated) {
                var payload = {
                  name: translated,
                  resourceType: 'Task',
                  query: {},
                  properties: {
                    description: 'Unfiltered Tasks',
                    priority: 1,
                    color: '#555555',
                    refresh: false,
                    howUndefinedVariable: false
                  }
                };
                return filterResource.create(payload);
              })
              .then(function() {
                $scope.filtersData.changed('filters');
              })
              .catch(function(err) {
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
