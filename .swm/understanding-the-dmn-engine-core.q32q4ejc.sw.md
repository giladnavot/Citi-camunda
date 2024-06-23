---
title: Understanding the DMN Engine Core
---
The DMN Engine Core in the Citi-camunda project refers to the core functionality of the DMN (Decision Model and Notation) engine. It is responsible for parsing DMN decision models and evaluating decisions. The DMN Engine Core is implemented as an interface named `DmnEngine` which provides methods for parsing decisions from DMN files or DMN model instances, and for evaluating decisions. The actual implementation of this interface is provided by the `DefaultDmnEngine` class.

The DMN Engine Core is configured using the `DmnEngineConfiguration` interface, which provides methods for setting up the engine. The actual configuration is done by the `DefaultDmnEngineConfiguration` class, which provides default settings for the DMN engine. The configuration includes settings for decision table evaluation listeners, decision evaluation listeners, script engine resolver, and others.

The DMN Engine Core is used throughout the Citi-camunda project. For instance, it is used in the `ProcessEngineConfigurationImpl` class for setting up the process engine, and in the `DecisionInvocation` class for evaluating decisions.

<SwmSnippet path="/engine-dmn/engine/src/main/java/org/camunda/bpm/dmn/engine/DmnEngine.java" line="26">

---

# DmnEngine Interface

The DmnEngine interface provides the methods for parsing decisions and evaluating decision tables. It also provides a method to get the configuration of the engine.

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

The DmnEngineConfiguration class provides the configuration for a DmnEngine. It can be used to build a new engine.

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

The DefaultDmnEngine class is an implementation of the DmnEngine interface. It provides the functionality to parse decisions and evaluate decision tables.

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

# DMN Engine Core Functions

This section provides an overview of the key functions within the DMN Engine Core of the Citi-camunda repository.

<SwmSnippet path="/engine-dmn/engine/src/main/java/org/camunda/bpm/dmn/engine/impl/DefaultDmnEngineConfiguration.java" line="43">

---

## DefaultDmnEngineConfiguration

The 'DefaultDmnEngineConfiguration' class extends the 'DmnEngineConfiguration' class and provides the configuration for the DMN engine. It includes various configuration options such as the expression language to use (FEEL or JUEL), decision table evaluation listeners, and the script engine resolver. The 'init()' method is called when building the engine to initialize these configurations.

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

<SwmSnippet path="/engine-dmn/engine/src/main/java/org/camunda/bpm/dmn/engine/impl/DefaultDmnEngine.java" line="36">

---

## DefaultDmnEngine

The 'DefaultDmnEngine' class implements the 'DmnEngine' interface and provides the functionality for parsing and evaluating decisions. It uses the configurations provided by the 'DefaultDmnEngineConfiguration' class. The 'parseDecisions()' methods are used to parse all decisions in a DMN decision model, while the 'parseDecision()' methods are used to parse a specific decision with a given key.

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

# DMN Engine Core Endpoints

Understanding DMN Engine Core Endpoints

<SwmSnippet path="/engine-dmn/feel-juel/src/main/java/org/camunda/bpm/dmn/feel/impl/juel/transform/FeelToJuelTransformImpl.java" line="1">

---

## FeelToJuelTransformImpl

The `FeelToJuelTransformImpl` class is responsible for transforming FEEL (Friendly Enough Expression Language) expressions into JUEL (Java Unified Expression Language) expressions. It defines several transformers for different types of expressions, including an endpoint transformer.

```java
/*
 * Copyright Camunda Services GmbH and/or licensed to Camunda Services GmbH
 * under one or more contributor license agreements. See the NOTICE file
 * distributed with this work for additional information regarding copyright
 * ownership. Camunda licenses this file to you under the Apache License,
 * Version 2.0; you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *     http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */
package org.camunda.bpm.dmn.feel.impl.juel.transform;

import java.util.ArrayList;
import java.util.List;

```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-juel/src/main/java/org/camunda/bpm/dmn/feel/impl/juel/transform/ComparisonTransformer.java" line="1">

---

## ComparisonTransformer

The `ComparisonTransformer` class is used to transform comparison expressions from FEEL to JUEL. It checks if the expression starts with a comparison operator and then transforms the comparison accordingly.

```java
/*
 * Copyright Camunda Services GmbH and/or licensed to Camunda Services GmbH
 * under one or more contributor license agreements. See the NOTICE file
 * distributed with this work for additional information regarding copyright
 * ownership. Camunda licenses this file to you under the Apache License,
 * Version 2.0; you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *     http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */
package org.camunda.bpm.dmn.feel.impl.juel.transform;

import java.util.regex.Matcher;
import java.util.regex.Pattern;

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
