---
title: Basic Concepts of Feel Scala in Citi-camunda
---
Feel Scala in the Citi-camunda repository refers to the implementation of the FEEL (Friendly Enough Expression Language) engine using Scala. The FEEL engine is a crucial part of the Camunda BPMN platform, used for evaluating expressions and making decisions in business processes. The Scala implementation, represented by the `ScalaFeelEngine` class, provides a way to evaluate simple expressions and unary tests, among other functionalities. It also includes custom function providers and value mappers, which are used to transform and map values respectively.

<SwmSnippet path="/engine-dmn/feel-scala/src/main/java/org/camunda/bpm/dmn/feel/impl/scala/ScalaFeelEngine.java" line="45">

---

# ScalaFeelEngine Class

The `ScalaFeelEngine` class is the main entry point for using Feel Scala. It provides methods for evaluating expressions and unary tests, and can be customized with custom functions through the `FeelCustomFunctionProvider` interface.

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

<SwmSnippet path="/engine-dmn/feel-scala/src/main/java/org/camunda/bpm/dmn/feel/impl/scala/ScalaFeelEngineFactory.java" line="36">

---

# ScalaFeelEngineFactory Class

The `ScalaFeelEngineFactory` class is used to create instances of the `ScalaFeelEngine` class. This is typically done at the start of a decision-making process.

```java
  public FeelEngine createInstance() {
      return new ScalaFeelEngine(customFunctionProviders);
   }
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-scala/src/test/java/org/camunda/bpm/dmn/engine/feel/helper/FeelRule.java" line="30">

---

# FeelRule Class

The `FeelRule` class is a helper class used in tests to evaluate expressions using the `ScalaFeelEngine`. It provides a convenient way to evaluate expressions in a controlled environment.

```java
public class FeelRule extends TestWatcher {

  protected FunctionProvider functionProvider;
  protected ScalaFeelEngine feelEngine;

  protected FeelRule(FunctionProvider functionProvider) {
    this.functionProvider = functionProvider;
  }

  protected FeelRule() {
    feelEngine = new ScalaFeelEngine(null);
  }

  public static FeelRule buildWithFunctionProvider() {
    FunctionProvider functionProvider = new FunctionProvider();
    return new FeelRule(functionProvider);
  }

  public static FeelRule build() {
    return new FeelRule();
  }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
