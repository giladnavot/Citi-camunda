---
title: Introduction to Cockpit UI Process Definition
---
The Cockpit UI Process Definition in the Citi-camunda project refers to the visual representation and management of process definitions within the Camunda Cockpit. It provides an interface for users to interact with, monitor, and manage process definitions. This includes viewing process instances, called process definitions, and job definitions. The Cockpit UI Process Definition is implemented using AngularJS and it interacts with the Camunda Platform's backend services to fetch and manipulate data.

<SwmSnippet path="/webapps/frontend/ui/cockpit/tests/pages/process-definition/definition-view.js" line="23">

---

# Process Definition View

This file defines the main view for a process definition. It includes methods for getting the process definition name and checking if the process definition is suspended.

```javascript
  url: '/camunda/app/cockpit/default/#/process-definition/:process/runtime',

  pageHeader: function() {
    return element(by.binding('processDefinition.key'));
  },

  fullPageHeaderProcessDefinitionName: function() {
    return this.pageHeader().getText();
  },

  pageHeaderProcessDefinitionName: function() {
    return this.breadcrumb.activeCrumb().getText();
  },

  isDefinitionSuspended: function() {
    return element(
      by.css('.cam-breadcrumb .active .badge-suspended')
    ).isPresent();
  },

  getReportLink: function() {
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/base/app/views/processDefinition/processInstanceTable.js" line="30">

---

# Process Instances Table

This file defines the table of process instances displayed in the process definition view. It includes functionality for sorting and filtering the table, and for navigating to detailed views of individual process instances.

```javascript
  'ViewsProvider',
  function(ViewsProvider) {
    ViewsProvider.registerDefaultView('cockpit.processDefinition.runtime.tab', {
      id: 'process-instances-table',
      label: 'PLUGIN_PROCESS_INSTANCES_LABEL',
      template: template,
      controller: [
        '$scope',
        '$location',
        'search',
        'routeUtil',
        'PluginProcessInstanceResource',
        '$translate',
        'localConf',
        function(
          $scope,
          $location,
          search,
          routeUtil,
          PluginProcessInstanceResource,
          $translate,
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/base/app/views/processDefinition/calledProcessDefinitionTable.js" line="25">

---

# Called Process Definitions Table

This file defines the table of called process definitions displayed in the process definition view. It includes functionality for sorting and filtering the table, and for navigating to detailed views of individual called process definitions.

```javascript
module.exports = [
  'ViewsProvider',
  function(ViewsProvider) {
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
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/tests/pages/process-definition/tabs/job-definitions-tab.js" line="22">

---

# Job Definitions Table

This file defines the table of job definitions displayed in the process definition view. It includes functionality for sorting and filtering the table, and for navigating to detailed views of individual job definitions.

```javascript
module.exports = Table.extend({
  tabRepeater: 'tabProvider in processDefinitionTabs',
  tabIndex: 2,
  tabLabel: 'Job Definitions',
  tableRepeater: 'jobDefinition in jobDefinitions',

  state: function(idx) {
    return this.tableItem(idx, '.state:not(.ng-hide)');
  },

  activity: function(idx) {
    return this.tableItem(idx, '.activity');
  },

  configuration: function(idx) {
    return this.tableItem(idx, '.configuration');
  },

  suspendJobDefinitionButton: function(idx) {
    return this.tableItem(
      idx,
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
