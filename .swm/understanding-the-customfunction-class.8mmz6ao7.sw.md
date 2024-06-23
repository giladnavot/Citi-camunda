---
title: Understanding the CustomFunction Class
---
The `CustomFunction` is a class that represents a custom function in the Camunda BPMN engine. It contains a list of parameters (`params`), a function that takes a list of objects and returns an object (`function`), and a boolean flag indicating whether the function accepts variable arguments (`hasVarargs`). The `CustomFunction` class provides a static `create` method that returns a `CustomFunctionBuilder` for configuring a custom function.

<SwmSnippet path="/engine-dmn/feel-scala/src/main/java/org/camunda/bpm/dmn/feel/impl/scala/function/CustomFunction.java" line="26">

---

# CustomFunction Class

This is the CustomFunction class. It contains a list of parameters, the function itself, and a boolean indicating whether it accepts variable arguments.

```java
public class CustomFunction {

  protected List<String> params;
  protected Function<List<Object>, Object> function;
  protected boolean hasVarargs;

  public CustomFunction() {
    params = Collections.emptyList();
  }

  /**
   * Creates a fluent builder to configure a custom function
   *
   * @return builder to apply configurations on
   */
  public static CustomFunctionBuilder create() {
    return new CustomFunctionBuilderImpl();
  }

  public List<String> getParams() {
    return params;
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-scala/src/main/java/org/camunda/bpm/dmn/feel/impl/scala/function/CustomFunction.java" line="41">

---

# Creating a CustomFunction

This is the create method, which returns a new instance of CustomFunctionBuilder. This builder can be used to configure a new CustomFunction.

```java
  public static CustomFunctionBuilder create() {
    return new CustomFunctionBuilderImpl();
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-scala/src/main/java/org/camunda/bpm/dmn/feel/impl/scala/function/CustomFunction.java" line="49">

---

# Setting Parameters and Function

These are the setter methods for the parameters and function of the CustomFunction. They allow you to define the parameters that the function accepts and the function itself.

```java
  public void setParams(List<String> params) {
    this.params = params;
  }

  public Function<List<Object>, Object> getFunction() {
    return function;
  }

  public void setFunction(Function<List<Object>, Object> function) {
    this.function = function;
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-scala/src/main/java/org/camunda/bpm/dmn/feel/impl/scala/function/CustomFunction.java" line="61">

---

# Variable Arguments

These methods are used to indicate whether the function accepts variable arguments. If setHasVarargs is called with true, the function is considered to accept variable arguments.

```java
  public boolean hasVarargs() {
    return hasVarargs;
  }

  public void setHasVarargs(boolean hasVarargs) {
    this.hasVarargs = hasVarargs;
  }
```

---

</SwmSnippet>

# CustomFunction Class Overview

The CustomFunction class is a key component in the Camunda BPMN platform, allowing for the creation and management of custom functions. It includes several methods for setting and retrieving function parameters, handling variable arguments, and more.

<SwmSnippet path="/engine-dmn/feel-scala/src/main/java/org/camunda/bpm/dmn/feel/impl/scala/function/CustomFunction.java" line="41">

---

## CustomFunction Creation

The `create` method is a static method that returns a new instance of `CustomFunctionBuilderImpl`. This is the starting point for creating a new custom function.

```java
  public static CustomFunctionBuilder create() {
    return new CustomFunctionBuilderImpl();
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-scala/src/main/java/org/camunda/bpm/dmn/feel/impl/scala/function/CustomFunction.java" line="45">

---

## Parameter Management

The `getParams` and `setParams` methods are used to retrieve and set the parameters of the custom function, respectively. The parameters are stored as a list of strings.

```java
  public List<String> getParams() {
    return params;
  }

  public void setParams(List<String> params) {
    this.params = params;
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-scala/src/main/java/org/camunda/bpm/dmn/feel/impl/scala/function/CustomFunction.java" line="53">

---

## Function Handling

The `getFunction` and `setFunction` methods are used to retrieve and set the function of the custom function, respectively. The function is stored as a `java.util.function.Function` object.

```java
  public Function<List<Object>, Object> getFunction() {
    return function;
  }

  public void setFunction(Function<List<Object>, Object> function) {
    this.function = function;
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-scala/src/main/java/org/camunda/bpm/dmn/feel/impl/scala/function/CustomFunction.java" line="61">

---

## Variable Arguments Handling

The `hasVarargs` and `setHasVarargs` methods are used to check if the custom function has variable arguments and to set this property, respectively.

```java
  public boolean hasVarargs() {
    return hasVarargs;
  }

  public void setHasVarargs(boolean hasVarargs) {
    this.hasVarargs = hasVarargs;
  }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
