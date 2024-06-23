---
title: Overview of Feel Juel
---
Feel Juel in the Citi-camunda project refers to a set of classes and interfaces that are used for transforming FEEL (Friendly Enough Expression Language) expressions into JUEL (Java Unified Expression Language) expressions. This transformation is necessary because FEEL is the standard expression language for DMN (Decision Model and Notation), but the Camunda engine uses JUEL for expression evaluation. The main classes involved in this transformation are `FeelToJuelTransform`, `FeelToJuelTransformImpl`, and `FeelToJuelTransformer`. The `FeelToJuelTransform` interface defines the methods for transforming different types of FEEL expressions. The `FeelToJuelTransformImpl` class implements these methods and uses different transformers (implementations of `FeelToJuelTransformer`) to handle different types of FEEL expressions. Custom transformers can be added to handle specific types of FEEL expressions.

<SwmSnippet path="/engine-dmn/feel-juel/src/main/java/org/camunda/bpm/dmn/feel/impl/juel/transform/FeelToJuelTransform.java" line="19">

---

# FeelToJuelTransform Interface

The `FeelToJuelTransform` interface defines methods for transforming different types of FEEL expressions into JUEL. These methods include transforming simple unary tests, positive unary tests, endpoints, and adding custom function transformers.

```java
public interface FeelToJuelTransform {

  /**
   * Transform a FEEL simple unary tests expression to a JUEL expression.
   *
   * @param simpleUnaryTests the FEEL simple unary tests expression to transform
   * @param inputName the variable name of the input variable to test against
   * @return the resulting JUEL expression
   */
  String transformSimpleUnaryTests(String simpleUnaryTests, String inputName);

  /**
   * Transform a FEEL simple positive unary tests expression to a JUEL expression.
   *
   * @param simplePositiveUnaryTests the FEEL simple positive unary tests expression to transform
   * @param inputName the variable name of the input variable to test against
   * @return the resulting JUEL expression
   */
  String transformSimplePositiveUnaryTests(String simplePositiveUnaryTests, String inputName);

  /**
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-juel/src/main/java/org/camunda/bpm/dmn/feel/impl/juel/transform/FeelToJuelTransformImpl.java" line="25">

---

# FeelToJuelTransformImpl Class

The `FeelToJuelTransformImpl` class implements the `FeelToJuelTransform` interface. It provides the actual logic for transforming FEEL expressions into JUEL. It also handles custom function transformers, which are used for transforming custom functions defined in FEEL into equivalent JUEL expressions.

```java
public class FeelToJuelTransformImpl implements FeelToJuelTransform {

  public static final FeelEngineLogger LOG = FeelLogger.ENGINE_LOGGER;

  public static final FeelToJuelTransformer NOT_TRANSFORMER = new NotTransformer();
  public static final FeelToJuelTransformer HYPHEN_TRANSFORMER = new HyphenTransformer();
  public static final FeelToJuelTransformer LIST_TRANSFORMER = new ListTransformer();
  public static final FeelToJuelTransformer INTERVAL_TRANSFORMER = new IntervalTransformer();
  public static final FeelToJuelTransformer COMPARISON_TRANSFORMER = new ComparisonTransformer();
  public static final FeelToJuelTransformer EQUAL_TRANSFORMER = new EqualTransformer();
  public static final FeelToJuelTransformer ENDPOINT_TRANSFORMER = new EndpointTransformer();
  public static final List<FeelToJuelTransformer> CUSTOM_FUNCTION_TRANSFORMERS = new ArrayList<FeelToJuelTransformer>();

  public String transformSimpleUnaryTests(String simpleUnaryTests, String inputName) {
    simpleUnaryTests = simpleUnaryTests.trim();
    String juelExpression;
    if (HYPHEN_TRANSFORMER.canTransform(simpleUnaryTests)) {
      juelExpression = HYPHEN_TRANSFORMER.transform(this, simpleUnaryTests, inputName);
    }
    else if (NOT_TRANSFORMER.canTransform(simpleUnaryTests)) {
      juelExpression = NOT_TRANSFORMER.transform(this, simpleUnaryTests, inputName);
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-juel/src/main/java/org/camunda/bpm/dmn/feel/impl/juel/FeelEngineFactoryImpl.java" line="81">

---

# Using FeelToJuelTransform

The `FeelToJuelTransform` is typically used by creating an instance of `FeelToJuelTransformImpl` and then using it to transform FEEL expressions into JUEL. This is demonstrated in the `createFeelToJuelTransform` method of the `FeelEngineFactoryImpl` class.

```java
  protected FeelToJuelTransform createFeelToJuelTransform() {
    FeelToJuelTransformImpl transformer = new FeelToJuelTransformImpl();

    for (FeelToJuelFunctionTransformer functionTransformer : customFunctionTransformers) {
      transformer.addCustomFunctionTransformer(functionTransformer);
    }

    return transformer;
  }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
