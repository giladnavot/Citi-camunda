---
title: Exploring the Cockpit UI Job Definition
---
The Cockpit UI Job Definition in the Citi-camunda project refers to the configuration and management of jobs within the Camunda workflow engine. It is part of the Cockpit's user interface, allowing users to view and manage job definitions. A job definition represents a timer event or an asynchronous continuation within a process definition. The Cockpit UI Job Definition includes features such as viewing job definitions, setting job priorities, and suspending or activating job definitions.

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/jobDefinition/app/views/processDefinition/jobDefinitionTable.js" line="162">

---

# Job Definition Table

The job definition table is where job definitions are displayed. It fetches the job definitions using the `Views.getProviders` method with the 'cockpit.jobDefinition.action' component.

```javascript
    };
    $scope.jobDefinitionActions = Views.getProviders({
      component: 'cockpit.jobDefinition.action'
    });
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/jobDefinition/app/views/processDefinition/job-definition-suspension-state-dialog.html" line="1">

---

# Job Definition Suspension State Dialog

The job definition suspension state dialog is used to suspend or activate job definitions. It provides a form for users to specify the suspension state and execution date.

```html
<!-- # CE - camunda-bpm-webapp/webapp/src/main/resources-plugin/jobDefinition/app/views/processDefinition/job-definition-suspension-state-dialog.html -->
<div class="modal-header">
  <h3>{{ (jobDefinition.suspended ? 'PLUGIN_JOBDEFINITION_ACTIVE_JOB_DEFINITION' : 'PLUGIN_JOBDEFINITION_SUSPEND_JOB_DEFINITION' | translate) }}</h3>
</div>

<div class="job-definition-suspension-state modal-body">
  <div notifications-panel></div>

  <div ng-hide="status === 'SUCCESS' || status === 'FAIL'">

    <p ng-show="jobDefinition.suspended">
      <!-- activation -->
      {{ 'PLUGIN_JOBDEFINITION_LEGEND_ACTIVE' | translate }}
    </p>

    <p ng-hide="jobDefinition.suspended">
      <!-- suspension -->
      {{ 'PLUGIN_JOBDEFINITION_LEGEND_SUSPEND' | translate }}
    </p>

    <form class="form-horizontal"
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/jobDefinition/app/actions/override-job-priority/override-job-priority-action.js" line="25">

---

# Override Job Priority Action

The override job priority action allows users to change the priority of jobs. It is registered as a default view for the 'cockpit.jobDefinition.action' component.

```javascript
  ViewsProvider.registerDefaultView('cockpit.jobDefinition.action', {
    id: 'job-definition-override-job-priority-action',
    template: actionTemplate,
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
