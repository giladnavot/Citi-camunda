---
title: Exploring the ScalaFeelEngine
---
The `ScalaFeelEngine` is a class that implements the `FeelEngine` interface. It is used to evaluate expressions and unary tests in the context of a given variable. The engine is built with a `CustomFunctionTransformer` and a `CompositeValueMapper`, which are used to transform custom functions and map values respectively. The `ScalaFeelEngine` also provides methods to convert Java lists to Scala lists, which is necessary for the engine's operation.

<SwmSnippet path="/engine-dmn/feel-scala/src/main/java/org/camunda/bpm/dmn/feel/impl/scala/ScalaFeelEngine.java" line="45">

---

# ScalaFeelEngine Class

This is the ScalaFeelEngine class. It implements the FeelEngine interface and provides methods to evaluate expressions and unary tests.

```java
public class ScalaFeelEngine implements FeelEngine {

  protected static final String INPUT_VARIABLE_NAME = "inputVariableName";

  protected static final ScalaFeelLogger LOGGER = ScalaFeelLogger.LOGGER;

  protected org.camunda.feel.FeelEngine feelEngine;

  public ScalaFeelEngine(java.util.List<FeelCustomFunctionProvider> functionProviders) {
    List<CustomValueMapper> valueMappers = getValueMappers();

    CompositeValueMapper compositeValueMapper = new CompositeValueMapper(valueMappers);

    CustomFunctionTransformer customFunctionTransformer =
      new CustomFunctionTransformer(functionProviders, compositeValueMapper);

    feelEngine = buildFeelEngine(customFunctionTransformer, compositeValueMapper);
  }

  public <T> T evaluateSimpleExpression(String expression, VariableContext variableContext) {

```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-scala/src/main/java/org/camunda/bpm/dmn/feel/impl/scala/ScalaFeelEngine.java" line="64">

---

# evaluateSimpleExpression Method

This is the `evaluateSimpleExpression` method. It takes an expression and a variable context as parameters and evaluates the expression in the context of the given variable.

```java
  public <T> T evaluateSimpleExpression(String expression, VariableContext variableContext) {

    CustomContext context = new CustomContext() {
      public VariableProvider variableProvider() {
        return new ContextVariableWrapper(variableContext);
      }
    };

    Either either = feelEngine.evalExpression(expression, context);

    if (either instanceof Right) {
      Right right = (Right) either;

      return (T) right.value();

    } else {
      Left left = (Left) either;
      Failure failure = (Failure) left.value();
      String message = failure.message();

      throw LOGGER.evaluationException(message);
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-scala/src/main/java/org/camunda/bpm/dmn/feel/impl/scala/ScalaFeelEngine.java" line="89">

---

# evaluateSimpleUnaryTests Method

This is the `evaluateSimpleUnaryTests` method. It takes an expression, an input variable, and a variable context as parameters and evaluates the unary tests in the context of the given variable.

```java
  public boolean evaluateSimpleUnaryTests(String expression,
                                          String inputVariable,
                                          VariableContext variableContext) {
    Map inputVariableMap = new Map.Map1(INPUT_VARIABLE_NAME, inputVariable);

    StaticVariableProvider inputVariableContext = new StaticVariableProvider(inputVariableMap);

    ContextVariableWrapper contextVariableWrapper = new ContextVariableWrapper(variableContext);

    CustomContext context = new CustomContext() {
      public VariableProvider variableProvider() {
        return new CompositeVariableProvider(toScalaList(inputVariableContext, contextVariableWrapper));
      }
    };

    Either either = feelEngine.evalUnaryTests(expression, context);

    if (either instanceof Right) {
      Right right = (Right) either;
      Object value = right.value();

```

---

</SwmSnippet>

# ScalaFeelEngine Functions

The ScalaFeelEngine class contains several important methods that are used for evaluating expressions and unary tests.

<SwmSnippet path="/engine-dmn/feel-scala/src/main/java/org/camunda/bpm/dmn/feel/impl/scala/ScalaFeelEngine.java" line="64">

---

## evaluateSimpleExpression

The `evaluateSimpleExpression` method is used to evaluate a simple expression in the context of a given variable. It takes an expression and a variable context as parameters. The method creates a custom context and evaluates the expression using the FEEL engine. If the evaluation is successful, it returns the result. If not, it throws an evaluation exception with a failure message.

```java
  public <T> T evaluateSimpleExpression(String expression, VariableContext variableContext) {

    CustomContext context = new CustomContext() {
      public VariableProvider variableProvider() {
        return new ContextVariableWrapper(variableContext);
      }
    };

    Either either = feelEngine.evalExpression(expression, context);

    if (either instanceof Right) {
      Right right = (Right) either;

      return (T) right.value();

    } else {
      Left left = (Left) either;
      Failure failure = (Failure) left.value();
      String message = failure.message();

      throw LOGGER.evaluationException(message);
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-scala/src/main/java/org/camunda/bpm/dmn/feel/impl/scala/ScalaFeelEngine.java" line="89">

---

## evaluateSimpleUnaryTests

The `evaluateSimpleUnaryTests` method is used to evaluate simple unary tests in the context of a given variable. It takes an expression, an input variable, and a variable context as parameters. The method creates a custom context and evaluates the unary tests using the FEEL engine. If the evaluation is successful, it returns the result. If not, it throws an evaluation exception with a failure message.

```java
  public boolean evaluateSimpleUnaryTests(String expression,
                                          String inputVariable,
                                          VariableContext variableContext) {
    Map inputVariableMap = new Map.Map1(INPUT_VARIABLE_NAME, inputVariable);

    StaticVariableProvider inputVariableContext = new StaticVariableProvider(inputVariableMap);

    ContextVariableWrapper contextVariableWrapper = new ContextVariableWrapper(variableContext);

    CustomContext context = new CustomContext() {
      public VariableProvider variableProvider() {
        return new CompositeVariableProvider(toScalaList(inputVariableContext, contextVariableWrapper));
      }
    };

    Either either = feelEngine.evalUnaryTests(expression, context);

    if (either instanceof Right) {
      Right right = (Right) either;
      Object value = right.value();

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
