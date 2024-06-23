---
title: Understanding Process Plugins
---
Process Plugins in Citi-camunda refer to the extensions that are designed to interact with the process engine. They are used to add or modify functionalities related to process handling in the application. For instance, the 'cam-tasklist-navbar-action-start-process-plugin.js' file contains a Process Plugin that provides an action in the tasklist navbar to start a process. It uses the Camunda API to interact with the process definitions and start a process instance.

The Process Plugin is configured using the 'PluginConfiguration' function, which registers the plugin with a unique ID and sets its priority. The 'registerDefaultView' function is used to register the plugin's view, which is defined in the 'cam-tasklist-navbar-action-start-process-plugin.html' file. This view is what the user interacts with when using the plugin.

The Process Plugin uses the 'processData' function to handle data dependencies. It also uses the 'ProcessDefinition' resource from the Camunda API to interact with process definitions.

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/process/plugins/action/cam-tasklist-navbar-action-start-process-plugin.js" line="34">

---

# ProcessDefinition

Here, `ProcessDefinition` is a resource from the Camunda API. It's used to interact with process definitions in the process engine. This is a common pattern in Process Plugins, where they interact with the process engine through the Camunda API.

```javascript
    var ProcessDefinition = camAPI.resource('process-definition');

    var processData = ($scope.processData = dataDepend.create($scope));
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/process/plugins/action/cam-tasklist-navbar-action-start-process-plugin.js" line="151">

---

# Plugin Registration

This is an example of how a Process Plugin is registered with the process engine. The `id` field is used to uniquely identify the plugin. The `template` and `controller` fields define the behavior of the plugin.

```javascript
var Configuration = function PluginConfiguration(ViewsProvider) {
  ViewsProvider.registerDefaultView('tasklist.navbar.action', {
    id: 'start-process-action',
    template: startProcessActionTemplate,
    controller: Controller,
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/process/plugins/action/cam-tasklist-navbar-action-start-process-plugin.js" line="79">

---

# Starting a Process

This is an example of how a Process Plugin can be used to start a process. The `startForm` method of the `ProcessDefinition` resource is used to start a process with a specific process definition ID.

```javascript
          ProcessDefinition.startForm(currentProcessDefinitionId, function(
            err,
            res
```

---

</SwmSnippet>

# Process Plugins Functions

Process Plugins Functions

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/process/plugins/action/cam-tasklist-navbar-action-start-process-plugin.js" line="115">

---

## processData Function

The `processData` function is used to manage the process data. It is a dependency that is resolved before the plugin is initialized.

```javascript
        resolve: {
          processData: function() {
            return processData;
          }
        }
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/process/plugins/action/cam-tasklist-navbar-action-start-process-plugin.js" line="151">

---

## Configuration Function

The `Configuration` function is used to register the plugin with the ViewsProvider. It sets the id, template, controller, and priority of the plugin.

```javascript
var Configuration = function PluginConfiguration(ViewsProvider) {
  ViewsProvider.registerDefaultView('tasklist.navbar.action', {
    id: 'start-process-action',
    template: startProcessActionTemplate,
    controller: Controller,
    priority: 100
  });
};
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/process/plugins/action/cam-tasklist-navbar-action-start-process-plugin.js" line="153">

---

## id Property

The `id` property is used to uniquely identify the plugin. It is set to 'start-process-action' in this case.

```javascript
    id: 'start-process-action',
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/process/plugins/action/cam-tasklist-navbar-action-start-process-plugin.js" line="154">

---

## template Property

The `template` property is used to specify the HTML template for the plugin. It is set to 'startProcessActionTemplate' in this case.

```javascript
    template: startProcessActionTemplate,
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
