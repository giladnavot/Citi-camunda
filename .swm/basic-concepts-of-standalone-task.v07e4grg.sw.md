---
title: Basic Concepts of Standalone Task
---
A Standalone Task in the Citi-camunda project refers to a task that is not part of any process instance. It is a self-contained unit of work that can be created, assigned, and completed independently of any process flow. Standalone tasks are managed through the tasklist plugin, specifically within the standaloneTask directory. The task properties such as name, assignee, tenantId, description, and priority are defined in the cam-tasklist-create-task-modal.js file.

<SwmSnippet path="/webapps/frontend/ui/tasklist/plugins/standaloneTask/app/navbar/action/cam-tasklist-navbar-action-create-task-plugin.js" line="18">

---

# Standalone Task Creation

This code snippet shows how the `createTaskActionTemplate` and `createTaskModalTemplate` are required. These templates are used to render the UI for creating a new Standalone Task.

```javascript
'use strict';

var createTaskActionTemplate = require('./cam-tasklist-navbar-action-create-task-plugin.html?raw');
var createTaskModalTemplate = require('./modals/cam-tasklist-create-task-modal.html?raw');
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/plugins/standaloneTask/app/navbar/action/modals/cam-tasklist-create-task-modal.js" line="30">

---

# Standalone Task Properties

This code snippet shows the properties of a Standalone Task. When creating a new task, these properties can be set: `assignee`, `tenantId`, `description`, and `priority`.

```javascript
      assignee: null,
      tenantId: null,
      description: null,
      priority: 50 // default value
    };
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/plugins/standaloneTask/app/navbar/action/modals/cam-tasklist-create-task-modal.js" line="66">

---

# Exclusive Property

The `exclusive` property is set to true when creating a Standalone Task. This indicates that the task is not associated with any process instance.

```javascript
                status: translated,
                message: err ? err.message : '',
                exclusive: true,
                scope: $scope
              });
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
