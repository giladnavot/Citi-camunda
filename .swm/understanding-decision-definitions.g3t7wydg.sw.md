---
title: Understanding Decision Definitions
---
A Decision Definition in Camunda represents a decision resource in the BPMN 2.0 process engine. It is an interface that extends the ResourceDefinition interface. It provides methods to get information about the decision, such as its ID, key, and version tag. It also provides methods to understand its relationship with other decisions, such as getting the ID and key of the related decision requirements definition.

The DecisionDefinition interface is used in various parts of the codebase. For example, it is used in the RepositoryService to return a DecisionDefinition based on its ID. It is also used in the DecisionEvaluationUtil class to evaluate a decision based on the DecisionDefinition and a set of variables.

The DecisionDefinitionQuery interface provides methods to query for DecisionDefinitions. It allows for filtering and sorting of the results based on various properties of the DecisionDefinition, such as its ID, key, name, and version.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/DecisionDefinition.java" line="22">

---

# DecisionDefinition Interface

This is the definition of the DecisionDefinition interface. It includes methods for getting the ID and key of the related decision requirements definition, and for getting the version tag of the decision definition.

```java
public interface DecisionDefinition extends ResourceDefinition {

  /**
   * Returns the id of the related decision requirements definition. Can be
   * <code>null</code> if the decision has no relations to other decisions.
   *
   * @return the id of the decision requirements definition if exists.
   */
  String getDecisionRequirementsDefinitionId();

  /**
   * Returns the key of the related decision requirements definition. Can be
   * <code>null</code> if the decision has no relations to other decisions.
   *
   * @return the key of the decision requirements definition if exists.
   */
  String getDecisionRequirementsDefinitionKey();

  /** Version tag of the decision definition. */
  String getVersionTag();

```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/util/DecisionEvaluationUtil.java" line="74">

---

# Usage of DecisionDefinition

Here, DecisionDefinition is used to resolve a decision definition and create an invocation. The resolveDecisionDefinition method takes a callable element, an execution, and a default tenant ID as parameters and returns a DecisionDefinition object. The createInvocation method takes a DecisionDefinition object and a VariableMap object as parameters and returns a DecisionInvocation object.

```java
    DecisionDefinition decisionDefinition = resolveDecisionDefinition(callableElement, execution, defaultTenantId);
    DecisionInvocation invocation = createInvocation(decisionDefinition, execution);

    invoke(invocation);

    DmnDecisionResult result = invocation.getInvocationResult();
    if (result != null) {
      TypedValue typedValue = Variables.untypedValue(result, true);
      execution.setVariableLocal(DECISION_RESULT_VARIABLE, typedValue);

      if (resultVariable != null && decisionResultMapper != null) {
        Object mappedDecisionResult = decisionResultMapper.mapDecisionResult(result);
        execution.setVariable(resultVariable, mappedDecisionResult);
      }
    }
  }

  public static DmnDecisionResult evaluateDecision(DecisionDefinition decisionDefinition, VariableMap variables) throws Exception {
    DecisionInvocation invocation = createInvocation(decisionDefinition, variables);
    invoke(invocation);
    return invocation.getInvocationResult();
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/dmn/invocation/DecisionInvocation.java" line="43">

---

# DecisionDefinition in DecisionInvocation

In the DecisionInvocation class, a DecisionDefinition object is used as the target of the invocation. The DecisionInvocation constructor takes a DecisionDefinition object and a VariableContext object as parameters.

```java
  protected DecisionDefinition decisionDefinition;
  protected VariableContext variableContext;

  public DecisionInvocation(DecisionDefinition decisionDefinition, VariableContext variableContext) {
    super(null, (DecisionDefinitionEntity) decisionDefinition);
```

---

</SwmSnippet>

# DecisionDefinition Functions

This section will cover the main functions of the DecisionDefinition interface in the Citi-camunda repository.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/DecisionDefinitionQuery.java" line="30">

---

## decisionDefinitionId

The `decisionDefinitionId` function is used to select a decision definition with a specific id. It takes a string parameter which is the id of the decision definition.

```java
  DecisionDefinitionQuery decisionDefinitionId(String decisionDefinitionId);
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/DecisionDefinitionQuery.java" line="66">

---

## decisionDefinitionKey

The `decisionDefinitionKey` function is used to select a decision definition with a specific key. It takes a string parameter which is the key of the decision definition.

```java
  DecisionDefinitionQuery decisionDefinitionKey(String decisionDefinitionKey);
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/DecisionDefinitionQuery.java" line="44">

---

## decisionDefinitionCategory

The `decisionDefinitionCategory` function is used to select decision definitions with a specific category. It takes a string parameter which is the category of the decision definition.

```java
  DecisionDefinitionQuery decisionDefinitionCategory(String decisionDefinitionCategory);
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/DecisionDefinitionQuery.java" line="112">

---

## decisionDefinitionVersion

The `decisionDefinitionVersion` function is used to select a decision definition with a certain version. It takes an Integer parameter which is the version of the decision definition.

```java
  DecisionDefinitionQuery decisionDefinitionVersion(Integer decisionDefinitionVersion);
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
