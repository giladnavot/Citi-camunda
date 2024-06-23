---
title: Overview of the Feel API
---
The Feel API in the Citi-camunda project is a part of the DMN engine. It is used to evaluate FEEL (Friendly Enough Expression Language) expressions, which are a part of the DMN (Decision Model and Notation) standard. The API is defined in the `engine-dmn/feel-api` directory.

The main interface of the Feel API is the `FeelEngine`. This interface defines methods for evaluating FEEL simple expressions and FEEL simple unary tests. The results of these evaluations can be used in decision-making processes.

The `FeelEngineFactory` interface is used to create instances of `FeelEngine`. This allows for the creation of different implementations of the `FeelEngine`, which can be used to evaluate FEEL expressions in different ways.

<SwmSnippet path="/engine-dmn/feel-api/src/main/java/org/camunda/bpm/dmn/feel/impl/FeelEngineFactory.java" line="22">

---

# FeelEngineFactory Interface

This is the FeelEngineFactory interface. It has a single method `createInstance()` which is used to create a new instance of the FeelEngine.

```java
public interface FeelEngineFactory {

  /**
   * Create an instance of a {@link FeelEngine}.
   *
   * @return the instance of a {@link FeelEngine}
   */
  FeelEngine createInstance();

}
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/engine/src/main/java/org/camunda/bpm/dmn/engine/impl/DefaultDmnEngineConfiguration.java" line="66">

---

# Usage of FeelEngineFactory

Here, the FeelEngineFactory is used in the DefaultDmnEngineConfiguration class. The `feelEngineFactory` field is used to store the factory instance, and the `setFeelEngineFactory()` and `feelEngineFactory()` methods are used to set the factory instance. The `getFeelEngineFactory()` method is used to retrieve the factory instance.

```java
  protected FeelEngineFactory feelEngineFactory;
  protected FeelEngine feelEngine;

  /**
   * a list of DMN FEEL custom function providers
   */
  protected List<FeelCustomFunctionProvider> feelCustomFunctionProviders;

  /**
   * Enable FEEL legacy behavior
   */
  protected boolean enableFeelLegacyBehavior = false;

  protected String defaultInputExpressionExpressionLanguage = null;
  protected String defaultInputEntryExpressionLanguage = null;
  protected String defaultOutputEntryExpressionLanguage = null;
  protected String defaultLiteralExpressionLanguage = null;

  protected DmnTransformer transformer = new DefaultDmnTransformer();

  protected boolean returnBlankTableOutputAsNull = false;
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-juel/src/main/java/org/camunda/bpm/dmn/feel/impl/juel/FeelEngineFactoryImpl.java" line="39">

---

# Implementations of FeelEngineFactory

This is an example of an implementation of the FeelEngineFactory interface. The FeelEngineFactoryImpl class in the feel-juel module implements the FeelEngineFactory interface.

```java
public class FeelEngineFactoryImpl implements FeelEngineFactory {
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-scala/src/main/java/org/camunda/bpm/dmn/feel/impl/scala/ScalaFeelEngineFactory.java" line="25">

---

This is another example of an implementation of the FeelEngineFactory interface. The ScalaFeelEngineFactory class in the feel-scala module implements the FeelEngineFactory interface.

```java
public class ScalaFeelEngineFactory implements FeelEngineFactory {
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
