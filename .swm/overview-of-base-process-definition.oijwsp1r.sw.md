---
title: Overview of Base Process Definition
---
The Base Process Definition in the Citi-camunda project refers to the fundamental structure of a process that is defined and executed by the Camunda BPMN engine. It is a blueprint for a sequence of activities and tasks that need to be performed to achieve a specific business goal. The Base Process Definition is used to create process instances, which are individual executions of the process. It is defined in the BPMN 2.0 XML format and can be visually represented using the Camunda Modeler. The Base Process Definition includes details about the tasks, their order, and the conditions under which they are executed.

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/base/app/views/processDefinition/calledProcessDefinitionTable.js" line="28">

---

# Base Process Definition in Code

This file contains the implementation of the Base Process Definition in the Camunda cockpit. It defines a view for displaying the process definitions that are called by a given process definition. The controller function contains the logic for fetching and manipulating the process definitions.

```javascript
    ViewsProvider.registerDefaultView('cockpit.processDefinition.runtime.tab', {
      id: 'call-process-definitions-table',
      label: 'PLUGIN_CALLED_PROCESS_DEFINITIONS_LABEL',
      template: template,
      controller: [
        '$scope',
        '$location',
        '$q',
        'PluginProcessDefinitionResource',
        '$translate',
        'localConf',
        function(
          $scope,
          $location,
          $q,
          PluginProcessDefinitionResource,
          $translate,
          localConf
        ) {
          var filter;
          var processData = $scope.processData.newChild($scope);
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/base/app/views/processDefinition/called-process-definition-table.html" line="1">

---

# Base Process Definition in HTML

This HTML file provides the user interface for the Base Process Definition view in the Camunda cockpit. It uses AngularJS directives to bind the process definition data to the HTML elements.

```html
<!-- # CE - camunda-bpm-webapp/webapp/src/main/resources-plugin/base/app/views/processDefinition/called-process-definition-table.html -->
<div cam-widget-loader
     loading-state="{{ loadingState }}"
     text-empty="{{'PLUGIN_CALLED_PROCESS_EMPTY' | translate}}">
  <table class="called-process-definition cam-table">
    <thead sortable-table-head
           head-columns="headColumns"
           on-sort-change="onSortChange(sortObj)"
           default-sort="sortObj">
    </thead>
    <tbody>
      <tr ng-repeat="calledProcessDefinition in calledProcessDefinitions | orderBy:sortObj.sortBy:sortObj.sortReverse">
        <td class="process-definition"
            cam-widget-clipboard="calledProcessDefinition.id">
          <a ng-href="#/process-definition/{{ calledProcessDefinition.id }}/runtime?parentProcessDefinitionId={{ processDefinition.id }}">
            {{ calledProcessDefinition.label }}
          </a>
        </td>

        <td class="called-process-state" >
          <span>{{ calledProcessDefinition.state | translate }}</span>
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/base/app/views/processDefinition/called-process-definition-table.less" line="1">

---

# Base Process Definition in CSS

This LESS file defines the styles for the Base Process Definition view in the Camunda cockpit. It uses CSS classes to style the HTML elements.

```less
.call-activity-list {
  list-style: none;
  padding-left: 0;
  margin-bottom: 0;
  li {
    display: block;
  }
}

```

---

</SwmSnippet>

# Base Process Definition Functions

This section will cover the main functions of the Base Process Definition in the Citi-camunda repository.

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/base/app/views/processDefinition/calledProcessDefinitionTable.js" line="137">

---

## mergeInstanceAndDefinitionDtos

The `mergeInstanceAndDefinitionDtos` function merges Dtos for currently running and statically linked called processes by their id. It takes two parameters: runningProcessDefinitions and staticCalledProcesses. It creates a new map and populates it with the running process definitions. Then, it iterates over the static called processes and merges them into the map. If a process definition is both running and statically called, it is marked as such.

```javascript
          /**
           * Merges Dtos for currently running and statically linked called processes by their id.
           * @param runningProcessDefinitions
           * @param staticCalledProcesses
           * @returns {array}
           */
          function mergeInstanceAndDefinitionDtos(
            runningProcessDefinitions,
            staticCalledProcesses
          ) {
            const map = {};
            runningProcessDefinitions.forEach(dto => {
              const newDto = angular.copy(dto);
              newDto.state = 'PLUGIN_CALLED_PROCESS_DEFINITIONS_RUNNING_LABEL';
              map[newDto.id] = newDto;
            });

            staticCalledProcesses.forEach(dto => {
              const newDto = angular.copy(dto);
              if (map[dto.id]) {
                const merged = new Set([
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/base/app/views/processDefinition/calledProcessDefinitionTable.js" line="174">

---

## applyFilterToStaticCalled

The `applyFilterToStaticCalled` function applies a filter to the static called definitions. If a filter is set, it creates a new set of selected IDs and filters the static called definitions based on whether their activity IDs intersect with the selected IDs. The function returns the filtered static called definitions.

```javascript
          function applyFilterToStaticCalled(staticCalledDefinitions) {
            if (filter.activityIdIn && filter.activityIdIn.length) {
              const selectedIds = new Set(filter.activityIdIn);
              return staticCalledDefinitions
                .map(dto => {
                  const newDto = angular.copy(dto);
                  const intersection = dto.calledFromActivityIds.filter(e =>
                    selectedIds.has(e)
                  );
                  if (intersection.length) {
                    newDto.calledFromActivityIds = intersection;
                    return newDto;
                  }
                })
                .filter(dto => dto !== undefined);
            }
            return staticCalledDefinitions;
          }
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/base/app/views/processDefinition/calledProcessDefinitionTable.js" line="193">

---

## createTableEntries

The `createTableEntries` function creates table entries for the process definitions. It first merges the running and static process definitions using the `mergeInstanceAndDefinitionDtos` function. Then, it maps each merged definition to a table entry, which includes the called from activities and a label. If multiple entries have the same name, the function appends the version to the label to distinguish them.

```javascript
          function createTableEntries(
            runningProcessDefinitions,
            staticCalledProcesses,
            bpmnElements
          ) {
            const mergedDefinitions = mergeInstanceAndDefinitionDtos(
              runningProcessDefinitions,
              staticCalledProcesses
            );

            const tableEntries = mergedDefinitions.map(dto => {
              const calledFromActivities = dto.calledFromActivityIds.map(id =>
                extractActivityFromDiagram(bpmnElements, id)
              );

              return angular.extend({}, dto, {
                calledFromActivities: calledFromActivities,
                label: dto.name || dto.key
              });
            });

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
