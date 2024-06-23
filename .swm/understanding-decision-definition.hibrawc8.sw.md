---
title: Understanding Decision Definition
---
A Decision Definition in the Citi-camunda project refers to a specific set of rules or conditions that are used to automate and manage business processes. It is a key component in the decision management system of the Camunda platform. It is used to define the logic for making decisions within a business process, such as determining the approval of a loan application or the routing of a customer service request. The decision definition is typically created using the Decision Model and Notation (DMN) standard, which provides a common language for defining decision logic in a way that can be easily understood by both business and IT professionals.

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/decisionList/app/views/decisionDefinition/decisionInstanceTable.js" line="146">

---

# Decision Definition in Code

Here, a decision instance query is being created. The `decisionDefinitionId` is used to specify which decision definition the query pertains to. This is an example of how the decision definition ID is used to manage specific decision definitions.

```javascript
            var decisionInstanceQuery = angular.extend(
              {
                decisionDefinitionId: $scope.decisionDefinition.id,
                firstResult: firstResult,
                maxResults: count,
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/decisionList/app/views/decisionDefinition/decision-instance-table.html" line="35">

---

# Decision Definition in UI

In this HTML template, the `getProcessDefinitionLink` function is used to generate a link to the process definition associated with a decision instance. This shows how decision definitions are used in the context of process definitions.

```html
            cam-widget-clipboard="decisionInstance.processDefinitionKey">
          <a ng-href="{{ getProcessDefinitionLink(decisionInstance) }}">
            {{ decisionInstance.processDefinitionKey }}
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/decisionList/app/views/decisionDefinition/decision-instance-search-config.json" line="1">

---

# Decision Definition Search Config

This JSON file defines the configuration for searching decision instances. It includes various keys and operators that can be used in the search, demonstrating the flexibility and complexity of managing decision definitions.

```json
{
  "types": [
    {
      "id": {
        "key": "decisionInstanceId",
        "value": "PLUGIN_DECISION_DEFINITION_VALUE_TYPE_ID"
      },
      "operators": [
        {
          "key": "eq",
          "value": "="
        }
      ],
      "default": true
    },
    {
      "id": {
        "key": "processDefinitionId",
        "value": "PLUGIN_DECISION_DEFINITION_VALUE_PROCESS_DEFINITION_ID"
      },
      "operators": [
```

---

</SwmSnippet>

# Functions of Decision Definition

The Decision Definition in the Citi-camunda project is a crucial part of the workflow process. It includes several functions and properties that are used to define and manipulate decisions.

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/decisionList/app/views/decisionDefinition/decisionInstanceTable.js" line="30">

---

## ViewsProvider

The `ViewsProvider` function is used to register default views for the decision definition tab. It is used to define the layout and labels of the decision definition tab.

```javascript
  'ViewsProvider',
  function(ViewsProvider) {
    ViewsProvider.registerDefaultView('cockpit.decisionDefinition.tab', {
      id: 'decision-instances-table',
      label: 'DECISION_DEFINITION_LABEL',
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/decisionList/app/views/decisionDefinition/decisionInstanceTable.js" line="83">

---

## getProcessDefinitionLink

The `getProcessDefinitionLink` function is used to generate a link to the process definition associated with a decision instance. This link is used in the decision instance table to navigate to the process definition.

```javascript
          $scope.getProcessDefinitionLink = function(decisionInstance) {
            if (hasHistoryPlugin) {
              return (
                '#/process-definition/' +
                decisionInstance.processDefinitionId +
                '/history'
              );
            } else {
              return (
                '#/process-definition/' + decisionInstance.processDefinitionId
              );
            }
          };
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/decisionList/app/views/decisionDefinition/decisionInstanceTable.js" line="146">

---

## decisionDefinitionId

The `decisionDefinitionId` property is used to identify a specific decision definition. It is used in queries to fetch decision instances associated with a particular decision definition.

```javascript
            var decisionInstanceQuery = angular.extend(
              {
                decisionDefinitionId: $scope.decisionDefinition.id,
                firstResult: firstResult,
                maxResults: count,
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
