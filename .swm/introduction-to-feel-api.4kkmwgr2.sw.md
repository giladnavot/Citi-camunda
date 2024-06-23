---
title: Introduction to Feel API
---
The Feel API in Citi-camunda is a part of the Camunda BPM platform that is used to evaluate FEEL (Friendly Enough Expression Language) expressions. FEEL is a simple expression language designed by the OMG (Object Management Group) for use with DMN (Decision Model and Notation).

The API is primarily composed of two main components: the `FeelEngine` and the `FeelEngineFactory`. The `FeelEngine` is an interface that defines methods for evaluating FEEL expressions. It includes methods like `evaluateSimpleExpression` and `evaluateSimpleUnaryTests` which take in a FEEL expression and a variable context, and return the result of the expression.

The `FeelEngineFactory` is an interface that defines a method for creating instances of the `FeelEngine`. This factory pattern allows for the creation of `FeelEngine` instances without specifying the exact class of the object that will be created. This can be useful when the specific implementation of the `FeelEngine` may vary.

<SwmSnippet path="/engine-dmn/feel-api/src/main/java/org/camunda/bpm/dmn/feel/impl/FeelEngine.java" line="24">

---

## FeelEngine Interface

The `FeelEngine` interface provides methods to evaluate FEEL expressions and simple unary tests. The `evaluateSimpleExpression` method evaluates a simple FEEL expression, while the `evaluateSimpleUnaryTests` method evaluates a simple unary tests expression.

```java
public interface FeelEngine {

  /**
   * Evaluate a FEEL simple expression
   *
   * @param simpleExpression the simple expression to evaluate
   * @param variableContext the variable context which are available
   * @param <T> the expected return type
   * @return the result of the simple expression
   *
   * @throws FeelException
   *           if the expression cannot be evaluated
   */
  <T> T evaluateSimpleExpression(String simpleExpression, VariableContext variableContext);

  /**
   * Evaluate a FEEL simple unary tests expression
   *
   * @param simpleUnaryTests the simple unary tests expression to evaluate
   * @param inputName the name of the variable which is tested
   * @param variableContext the variable context are available
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-api/src/main/java/org/camunda/bpm/dmn/feel/impl/FeelEngineFactory.java" line="22">

---

## FeelEngineFactory Interface

The `FeelEngineFactory` interface provides a method to create an instance of the `FeelEngine`. This is used to instantiate the `FeelEngine` for evaluating FEEL expressions.

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

<SwmSnippet path="/engine-dmn/engine/src/main/java/org/camunda/bpm/dmn/engine/impl/DefaultDmnEngineConfiguration.java" line="369">

---

## Using FeelEngineFactory

The `FeelEngineFactory` is used in the `DefaultDmnEngineConfiguration` class to set and get the `FeelEngineFactory` instance. It also provides a method to set the `FeelEngineFactory` instance while returning the `DefaultDmnEngineConfiguration` instance for method chaining.

```java
   */
  public FeelEngineFactory getFeelEngineFactory() {
    return feelEngineFactory;
  }

  /**
   * Set the factory to create a {@link FeelEngine}
   *
   * @param feelEngineFactory the feel engine factory
   */
  public void setFeelEngineFactory(FeelEngineFactory feelEngineFactory) {
    this.feelEngineFactory = feelEngineFactory;
    this.feelEngine = null; // clear cached FEEL engine
  }

  /**
   * Set the factory to create a {@link FeelEngine}
   *
   * @param feelEngineFactory the feel engine factory
   * @return this
   */
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/engine/src/main/java/org/camunda/bpm/dmn/engine/impl/DefaultDmnEngineConfiguration.java" line="203">

---

## Creating an instance of FeelEngine

The `createInstance` method of the `FeelEngineFactory` is used to create an instance of the `FeelEngine`. This instance is then used to evaluate FEEL expressions.

```java
    if (feelEngine == null) {
      feelEngine = feelEngineFactory.createInstance();
    }
```

---

</SwmSnippet>

# Feel API Functions

The Feel API is a crucial part of the Camunda Platform, providing the ability to evaluate FEEL expressions. The main components of the Feel API are the FeelEngine and the FeelEngineFactory.

<SwmSnippet path="/engine-dmn/feel-api/src/main/java/org/camunda/bpm/dmn/feel/impl/FeelEngine.java" line="21">

---

## FeelEngine

The `FeelEngine` is an interface that defines the methods for evaluating FEEL expressions. It has two main methods: `evaluateSimpleExpression` for evaluating simple expressions and `evaluateSimpleUnaryTests` for evaluating unary tests.

```java
/**
 * Engine to evaluate FEEL expressions.
 */
public interface FeelEngine {

  /**
   * Evaluate a FEEL simple expression
   *
   * @param simpleExpression the simple expression to evaluate
   * @param variableContext the variable context which are available
   * @param <T> the expected return type
   * @return the result of the simple expression
   *
   * @throws FeelException
   *           if the expression cannot be evaluated
   */
  <T> T evaluateSimpleExpression(String simpleExpression, VariableContext variableContext);

  /**
   * Evaluate a FEEL simple unary tests expression
   *
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-api/src/main/java/org/camunda/bpm/dmn/feel/impl/FeelEngineFactory.java" line="19">

---

## FeelEngineFactory

The `FeelEngineFactory` is an interface that defines a method for creating instances of `FeelEngine`. The `createInstance` method is used to create a new instance of `FeelEngine`.

```java
/**
 * Factory to create a instance of a {@link FeelEngine}.
 */
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

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
