---
title: Understanding Feel Juel Transformation
---
Feel Juel Transformation in the Citi-camunda project refers to the process of converting FEEL (Friendly Enough Expression Language) expressions into JUEL (Java Unified Expression Language) expressions. This is done through the `FeelToJuelTransform` interface and its implementation `FeelToJuelTransformImpl`. The transformation process is used in various parts of the codebase, such as in the `FeelEngineImpl` and `FeelEngineFactoryImpl` classes. The `FeelToJuelTransform` interface provides methods for transforming different types of FEEL expressions, such as simple unary tests, simple positive unary tests, and endpoint expressions. Custom function transformers can also be added to the transformation process.

<SwmSnippet path="/engine-dmn/feel-juel/src/main/java/org/camunda/bpm/dmn/feel/impl/juel/transform/FeelToJuelTransform.java" line="19">

---

# FeelToJuelTransform Interface

This is the `FeelToJuelTransform` interface. It provides methods for transforming different types of FEEL expressions into JUEL expressions. Each method takes a FEEL expression and an input variable name as parameters and returns a JUEL expression.

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

This is the `FeelToJuelTransformImpl` class, a concrete implementation of the `FeelToJuelTransform` interface. It uses different transformers to transform the FEEL expressions into JUEL expressions based on their type.

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

# Feel Juel Transformation Functions

This section will cover the main functions of the Feel Juel Transformation in the Citi-camunda repository.

<SwmSnippet path="/engine-dmn/feel-juel/src/main/java/org/camunda/bpm/dmn/feel/impl/juel/transform/FeelToJuelTransformImpl.java" line="25">

---

## FeelToJuelTransformImpl

The `FeelToJuelTransformImpl` class implements the `FeelToJuelTransform` interface. It contains several transformer constants like `NOT_TRANSFORMER`, `LIST_TRANSFORMER`, `COMPARISON_TRANSFORMER`, etc. These transformers are used to transform different types of FEEL expressions to JUEL expressions.

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

<SwmSnippet path="/engine-dmn/feel-juel/src/main/java/org/camunda/bpm/dmn/feel/impl/juel/transform/FeelToJuelTransform.java" line="19">

---

## FeelToJuelTransform

The `FeelToJuelTransform` interface defines the methods for transforming FEEL expressions to JUEL expressions. It includes methods like `transformSimpleUnaryTests`, `transformSimplePositiveUnaryTests`, `transformSimplePositiveUnaryTest`, `transformEndpoint`, and `addCustomFunctionTransformer`.

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

<SwmSnippet path="/engine-dmn/feel-juel/src/main/java/org/camunda/bpm/dmn/feel/impl/juel/transform/FeelToJuelTransformer.java" line="19">

---

## FeelToJuelTransformer

The `FeelToJuelTransformer` interface defines the methods for checking if an expression can be transformed (`canTransform`) and for performing the transformation (`transform`).

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

# Endpoint Transformation

Feel Juel Transformation

<SwmSnippet path="/engine-dmn/feel-juel/src/main/java/org/camunda/bpm/dmn/feel/impl/juel/transform/FeelToJuelTransformImpl.java" line="84">

---

## transformEndpoint

The `transformEndpoint` method is used to transform a FEEL endpoint expression to a JUEL expression. It takes an endpoint and an input name as parameters, trims the endpoint, and then uses the `ENDPOINT_TRANSFORMER` to perform the transformation.

```java
  public String transformEndpoint(String endpoint, String inputName) {
    endpoint = endpoint.trim();
    return ENDPOINT_TRANSFORMER.transform(this, endpoint, inputName);
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-juel/src/main/java/org/camunda/bpm/dmn/feel/impl/juel/transform/ComparisonTransformer.java" line="44">

---

## transformComparison

The `transformComparison` method is used in the process of transforming a comparison expression. It uses the `transformEndpoint` method to transform the endpoint part of the comparison.

```java
  protected String transformComparison(FeelToJuelTransform transform, String operator, String endpoint, String inputName) {
    String juelEndpoint = transform.transformEndpoint(endpoint, inputName);
    return String.format("%s %s %s", inputName, operator, juelEndpoint);
  }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
