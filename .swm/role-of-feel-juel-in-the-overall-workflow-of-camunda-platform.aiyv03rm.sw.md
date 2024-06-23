---
title: Role of Feel Juel in the Overall Workflow of Camunda Platform
---
This document will cover the FEEL to JUEL transformation process in the Camunda workflow. We'll cover:

1. The role of the `FeelToJuelTransformImpl` class
2. The purpose of the `FeelToJuelTransformer` interface
3. The function of the `FeelToJuelTransform` interface
4. How these components interact in the transformation process.

<SwmSnippet path="/engine-dmn/feel-juel/src/main/java/org/camunda/bpm/dmn/feel/impl/juel/transform/FeelToJuelTransformImpl.java" line="25">

---

# The Role of the `FeelToJuelTransformImpl` Class

The `FeelToJuelTransformImpl` class is the main implementation of the transformation process. It defines several transformers for different types of FEEL expressions, such as `NOT_TRANSFORMER`, `LIST_TRANSFORMER`, `COMPARISON_TRANSFORMER`, etc. These transformers are used to convert FEEL expressions into JUEL expressions.

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

<SwmSnippet path="/engine-dmn/feel-juel/src/main/java/org/camunda/bpm/dmn/feel/impl/juel/transform/FeelToJuelTransformer.java" line="19">

---

# The Purpose of the `FeelToJuelTransformer` Interface

The `FeelToJuelTransformer` interface defines the methods that all transformers must implement. These methods include `canTransform`, which checks if a FEEL expression can be transformed by the transformer, and `transform`, which performs the actual transformation of a FEEL expression into a JUEL expression.

```java
public interface FeelToJuelTransformer {

  /**
   * Test if an expression can be transformed by this transformer.
   *
   * @param feelExpression the FEEL expression to transform
   * @return true if the expression can be transformed by this transformer, false otherwise
   */
  boolean canTransform(String feelExpression);

  /**
   * Transform the FEEL expression to a JUEL expression.
   *
   * @param transform the {@link FeelToJuelTransform} to use for further transforms
   * @param feelExpression the FEEL expression to transform
   * @param inputName the variable name of the input variable to test against
   * @return the resulting JUEL expression
   */
  String transform(FeelToJuelTransform transform, String feelExpression, String inputName);

}
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-juel/src/main/java/org/camunda/bpm/dmn/feel/impl/juel/transform/FeelToJuelTransform.java" line="19">

---

# The Function of the `FeelToJuelTransform` Interface

The `FeelToJuelTransform` interface defines the methods for transforming FEEL expressions into JUEL expressions. It includes methods for transforming different types of FEEL expressions, such as simple unary tests, simple positive unary tests, and endpoints.

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

<SwmSnippet path="/engine-dmn/feel-juel/src/main/java/org/camunda/bpm/dmn/feel/impl/juel/FeelEngineImpl.java" line="34">

---

# Interaction in the Transformation Process

The `FeelEngineImpl` class uses the `FeelToJuelTransform` to transform FEEL expressions into JUEL expressions. It creates an instance of `FeelToJuelTransformImpl` and uses it to perform the transformation.

```java
  protected FeelToJuelTransform transform;
  protected ExpressionFactory expressionFactory;
  protected ElContextFactory elContextFactory;
  protected Cache<TransformExpressionCacheKey, String> transformExpressionCache;

  public FeelEngineImpl(FeelToJuelTransform transform, ExpressionFactory expressionFactory, ElContextFactory elContextFactory,
      Cache<TransformExpressionCacheKey, String> transformExpressionCache) {
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="follow-up"><sup>Powered by [Swimm](/)</sup></SwmMeta>
