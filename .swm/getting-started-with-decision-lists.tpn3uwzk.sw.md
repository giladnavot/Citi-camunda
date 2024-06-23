---
title: Getting Started with Decision Lists
---
A Decision List in the Citi-camunda project refers to a collection of decisions that are used in the process automation workflow. These decisions are defined and managed through various functions and properties in the codebase. For instance, the `getDecisionsLists` function retrieves the decision lists, while the `getDecisions` function fetches individual decisions. The `decisions` property stores the decisions, and the `decisionList` variable is used to update the Decision Requirements Diagram (DRD) page. The Decision List is an integral part of the Camunda Platform's process automation capabilities, enabling the execution of complex decision logic at runtime.

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/decisionList/app/views/dashboard/services/decision-list.js" line="124">

---

# getDecisionsLists Function

The `getDecisionsLists` function is used to retrieve a list of all decision tables. This function is part of the Decision List service, which is responsible for managing decision tables.

```javascript
      getDecisionsLists: getDecisionsLists,
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/decisionList/app/views/dashboard/services/decision-list.js" line="125">

---

# getDecisions Function

The `getDecisions` function is used to execute a specific decision table. The results of the decision table execution are then stored in the `decisions` property.

```javascript
      getDecisions: getDecisions,
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/decisionList/app/views/dashboard/services/decision-list.js" line="41">

---

# decisions Property

The `decisions` property stores the results of the decision table execution. This property is updated every time a decision table is executed using the `getDecisions` function.

```javascript
          decisions = result;
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/decisionList/app/views/dashboard/views/decision-list.js" line="29">

---

# DecisionListController

The `DecisionListController` is responsible for managing the Decision List view. It uses the Decision List service to retrieve and execute decision tables, and updates the view with the results.

```javascript
      controller: 'DecisionListController',
```

---

</SwmSnippet>

# Decision List Functions

This section will cover the main functions of the Decision List in the Citi-camunda project.

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/decisionList/app/views/dashboard/services/decision-list.js" line="37">

---

## getDecisions Function

The `getDecisions` function fetches decision data. It uses the `decisionDefinitionService` to list decisions based on the provided parameters. The function also connects decision requirement definitions (DRDs) to the fetched decisions if they exist.

```javascript
    function getDecisions(params) {
      return decisionDefinitionService
        .list(Object.assign({}, defaultParams, params))
        .then(function(result) {
          decisions = result;

          if (drds) result = connectDrdsToDecisionDefinitions(drds, result);

          return result;
        });
    }
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/decisionList/app/views/dashboard/services/decision-list.js" line="62">

---

## getDecisionsLists Function

The `getDecisionsLists` function fetches both decision and DRD data. It uses the `decisionDefinitionService` and `drdService` to list and count decisions and DRDs respectively. The function then connects DRDs to the fetched decisions.

```javascript
    function getDecisionsLists(decParams, drdParams) {
      var decisionsProm = decisionDefinitionService.list(
        Object.assign({}, defaultParams, decParams)
      );

      var decisionsCountProm = decisionDefinitionService.count({
        latestVersion: true
      });

      var drdsProm = drdService.list(
        Object.assign({}, defaultParams, drdParams)
      );

      var drdsCountProm = drdService.count({
        latestVersion: true
      });

      return $q
        .all({
          decisions: decisionsProm,
          decisionsCount: decisionsCountProm,
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/decisionList/app/views/dashboard/services/decision-list.js" line="101">

---

## connectDrdsToDecisionDefinitions Function

The `connectDrdsToDecisionDefinitions` function connects DRDs to decisions. It maps through the decisions and if a decision has a `decisionRequirementsDefinitionId`, it finds the corresponding DRD and attaches it to the decision.

```javascript
    function connectDrdsToDecisionDefinitions(drds, decisions) {
      return decisions.map(function(decision) {
        if (decision.decisionRequirementsDefinitionId) {
          decision.drd = findDrdById(
            drds,
            decision.decisionRequirementsDefinitionId
          ) || {
            key: decision.decisionRequirementsDefinitionKey,
            id: decision.decisionRequirementsDefinitionId
          };
        }

        return decision;
      });
    }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
