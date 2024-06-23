---
title: Understanding the Tasklist Card
---
The Tasklist Card in Citi-camunda refers to a specific view in the tasklist application. It is a component that displays task-related variables in a card-like format. This view is registered using the ViewsProvider, which is a service that allows for the registration and configuration of views within the application. The Tasklist Card is defined with a unique id 'tasklist-card-variables' and a template that specifies its structure and content. The template uses the 'cam-tasklist-variables' directive to display the task variables.

The Tasklist Card also includes a 'details' function, which is used to provide detailed information about a specific task. This function is used in various parts of the application, such as the tasklist directives and styles, to control the display of task details.

The Tasklist Card is part of the tasklist plugin, which is a modular part of the tasklist application. The plugin is responsible for adding functionality to the tasklist, such as displaying task variables in a card-like format.

<SwmSnippet path="/webapps/frontend/ui/tasklist/plugins/tasklistCard/app/variables/main.js" line="31">

---

## Tasklist Card Plugin Configuration

This is where the Tasklist Card plugin is configured. The `ViewsProvider.registerDefaultView` method is used to register the Tasklist Card as a default view in the tasklist. The `id` property is used to uniquely identify the Tasklist Card, and the `template` property is used to define the HTML structure of the Tasklist Card.

```javascript
  function PluginConfiguration(ViewsProvider) {
    ViewsProvider.registerDefaultView('tasklist.card', {
      id: 'tasklist-card-variables',
      template:
        '<div cam-tasklist-variables ' +
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/plugins/tasklistCard/app/variables/directives/cam-tasklist-variables.js" line="54">

---

## Tasklist Card Details

The `details` function is used to resolve the details of a task. It returns the `variable` object which contains the details of a task. This function is used in the Tasklist Card to display the details of a task.

```javascript
              resolve: {
                details: function() {
                  return variable;
                }
              },
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/plugins/tasklistCard/app/variables/directives/cam-tasklist-variables.js" line="30">

---

## Tasklist Card Template

The `template` property is used to define the HTML structure of the Tasklist Card. It is a function that returns a string of HTML. This HTML string is used to render the Tasklist Card in the frontend of the application.

```javascript
  function($modal, $window, Uri) {
    return {
      template: template,

      scope: {
```

---

</SwmSnippet>

# Tasklist Card Functions

This section will delve into the functions of the Tasklist Card, focusing on how variables are handled and displayed.

<SwmSnippet path="/webapps/frontend/ui/tasklist/plugins/tasklistCard/app/variables/modals/cam-tasklist-variables-detail-modal.html" line="11">

---

## Variable Type

The 'variable-type' class is used to display the type of a variable. It is used in the detail modal of a task's variables, showing the type of each variable in a formatted manner.

```html
  </div>
  <div class="form-group">
    {{ 'VARIABLE_OBJECT_TYPE_NAME' | translate }}:
    <code class="variable-type">{{ type }}</code>
  </div>
  <div class="form-group">
    {{ 'VARIABLE_SERIALIZATION_DATA_FORMAT' | translate }}:
    <code class="variable-type">{{ dataFormat }}</code>
  </div>
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/plugins/tasklistCard/app/variables/directives/cam-tasklist-variables.html" line="28">

---

## Variable Value

The 'variable-value' class is used to display the value of a variable. It handles different types of variables, including 'Date', 'Null', 'Bytes', and 'Object'. For 'Object' type variables, it also provides a link to show the value in a modal.

```html
      <span class="variable-value"
            ng-switch-when="Date"
            tooltip-placement="top"
            uib-tooltip="{{ variablesByName[info.name].value | camDate }}">
        {{ variablesByName[info.name].value | camDate }}
      </span>

      <span class="variable-value"
            ng-switch-when="Null">
        {{ variablesByName[info.name].value }}
      </span>

      <a class="variable-value variable-type"
         ng-if="!expanded"
         ng-switch-when="Object"
         ng-click="showValue(variablesByName[info.name], $event)">
        {{ variablesByName[info.name].valueInfo.objectTypeName }}
      </a>

      <a class="variable-value variable-type"
         ng-if="expanded"
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/plugins/tasklistCard/app/variables/directives/cam-tasklist-variables.html" line="7">

---

## Variable Label

The 'variable-label' class is used to display the label of a variable. It also handles the case when a variable is undefined, showing a tooltip with the variable's name in such cases.

```html
      <strong class="variable-label"
              ng-class="{'undefined' : !variablesByName[info.name] && filterProperties.showUndefinedVariable}"
              tooltip-placement="top"
              uib-tooltip="{{ info.name }}">
        {{ info.label }}:
      </strong>
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
