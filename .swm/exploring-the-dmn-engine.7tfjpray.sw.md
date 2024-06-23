---
title: Exploring the DMN Engine
---
Engine DMN in Citi-camunda refers to the DMN (Decision Model and Notation) engine, which is a component of the Camunda platform. The DMN engine is responsible for parsing DMN decision models and evaluating decisions. It is represented by the `DmnEngine` interface, which provides methods for parsing decisions from DMN files or model instances, parsing decision requirements graphs, and evaluating decision tables. The `DmnEngine` can be built using a `DmnEngineConfiguration`, which can be customized to suit specific needs. The `DefaultDmnEngine` class is the default implementation of the `DmnEngine` interface.

<SwmSnippet path="/engine-dmn/engine/src/main/java/org/camunda/bpm/dmn/engine/DmnEngine.java" line="26">

---

# DmnEngine Interface

The `DmnEngine` interface defines the methods that a DMN Engine must implement. These methods include parsing decisions from a DMN decision model and evaluating decisions.

```java
/**
 * A DMN engine which can parse DMN decision models
 * and evaluate decisions.
 *
 * <p>
 * A new DMN engine can be build with a DMN engine configuration
 * (see {@link DmnEngineConfiguration#buildEngine()}).
 * </p>
 */
public interface DmnEngine {

  /**
   * The configuration of this engine.
   *
   * @return the DMN engine configuration
   */
  DmnEngineConfiguration getConfiguration();

  /**
   * Parse all decisions in a DMN decision model.
   *
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/engine/src/main/java/org/camunda/bpm/dmn/engine/DmnEngineConfiguration.java" line="26">

---

# DmnEngineConfiguration Class

The `DmnEngineConfiguration` class is used to configure a DMN Engine. It provides methods to set the engine metric collector, decision table evaluation listeners, and decision evaluation listeners.

```java
/**
 * The configuration of a {@link DmnEngine}. It can be used
 * to build a new engine using {@link #buildEngine()}.
 *
 * <p>
 *   To create a new default DMN engine configuration the
 *   method {@link #createDefaultDmnEngineConfiguration()}
 *   can be used.
 * </p>
 *
 * <p>
 *   Please be aware that changes to the configuration can also
 *   influence the behavior of engines which were already created
 *   by this configuration instance.
 * </p>
 */
public abstract class DmnEngineConfiguration {

  /**
   * @return a new default dmn engine configuration
   */
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/engine/src/main/java/org/camunda/bpm/dmn/engine/impl/DefaultDmnEngine.java" line="36">

---

# DefaultDmnEngine Class

The `DefaultDmnEngine` class is an implementation of the `DmnEngine` interface. It provides the functionality to parse and evaluate DMN decision models.

```java
public class DefaultDmnEngine implements DmnEngine {

  protected static final DmnEngineLogger LOG = DmnLogger.ENGINE_LOGGER;

  protected DefaultDmnEngineConfiguration dmnEngineConfiguration;
  protected DmnTransformer transformer;

  public DefaultDmnEngine(DefaultDmnEngineConfiguration dmnEngineConfiguration) {
    this.dmnEngineConfiguration = dmnEngineConfiguration;
    this.transformer = dmnEngineConfiguration.getTransformer();
  }

  public DmnEngineConfiguration getConfiguration() {
    return dmnEngineConfiguration;
  }

  public List<DmnDecision> parseDecisions(InputStream inputStream) {
    ensureNotNull("inputStream", inputStream);
    return transformer.createTransform()
      .modelInstance(inputStream)
      .transformDecisions();
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/engine/src/main/java/org/camunda/bpm/dmn/engine/impl/DefaultDmnEngineConfiguration.java" line="43">

---

# DefaultDmnEngineConfiguration Class

The `DefaultDmnEngineConfiguration` class is an implementation of the `DmnEngineConfiguration` class. It provides the default configuration for a DMN Engine.

```java
public class DefaultDmnEngineConfiguration extends DmnEngineConfiguration {

  public static final String FEEL_EXPRESSION_LANGUAGE = DmnModelConstants.FEEL_NS;
  public static final String FEEL_EXPRESSION_LANGUAGE_ALTERNATIVE = "feel";
  public static final String FEEL_EXPRESSION_LANGUAGE_DMN12 = DmnModelConstants.FEEL12_NS;
  public static final String FEEL_EXPRESSION_LANGUAGE_DMN13 = DmnModelConstants.FEEL13_NS;
  public static final String FEEL_EXPRESSION_LANGUAGE_DMN14 = DmnModelConstants.FEEL14_NS;
  public static final String FEEL_EXPRESSION_LANGUAGE_DMN15 = DmnModelConstants.FEEL15_NS;
  public static final String JUEL_EXPRESSION_LANGUAGE = "juel";

  protected DmnEngineMetricCollector engineMetricCollector;

  protected List<DmnDecisionTableEvaluationListener> customPreDecisionTableEvaluationListeners = new ArrayList<>();
  protected List<DmnDecisionTableEvaluationListener> customPostDecisionTableEvaluationListeners = new ArrayList<>();
  protected List<DmnDecisionTableEvaluationListener> decisionTableEvaluationListeners;

  // Decision evaluation listeners
  protected List<DmnDecisionEvaluationListener> decisionEvaluationListeners;
  protected List<DmnDecisionEvaluationListener> customPreDecisionEvaluationListeners = new ArrayList<>();
  protected List<DmnDecisionEvaluationListener> customPostDecisionEvaluationListeners = new ArrayList<>();

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
