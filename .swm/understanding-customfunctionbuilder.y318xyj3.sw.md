---
title: Understanding CustomFunctionBuilder
---
The `CustomFunctionBuilder` is an interface that provides a fluent builder pattern to create a `CustomFunction`. It allows you to define the parameters of the custom function, enable variable arguments, and define a custom function that only returns a value and has no further business logic. It also allows you to pass a `Function` with a `List` of objects as argument and an object as return value. Finally, it provides a `build` method to return the custom function to be registered in `FeelCustomFunctionProvider`.

<SwmSnippet path="/engine-dmn/feel-scala/src/main/java/org/camunda/bpm/dmn/feel/impl/scala/function/builder/CustomFunctionBuilder.java" line="31">

---

# Defining Parameters

The `setParams` method is used to define the parameters of the custom function. It takes a variable number of strings as arguments, which represent the names of the parameters.

```java
  /**
   * Define the parameters of the custom function.
   *
   * @param params of the custom function
   * @return the builder
   */
  CustomFunctionBuilder setParams(String... params);
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-scala/src/main/java/org/camunda/bpm/dmn/feel/impl/scala/function/builder/CustomFunctionBuilder.java" line="39">

---

# Enabling Variable Arguments

The `enableVarargs` method is used to enable variable arguments for the custom function. This allows the function to accept an arbitrary number of arguments.

```java
  /**
   * Enable variable arguments
   *
   * @return the builder
   */
  CustomFunctionBuilder enableVarargs();
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-scala/src/main/java/org/camunda/bpm/dmn/feel/impl/scala/function/builder/CustomFunctionBuilder.java" line="46">

---

# Setting the Return Value

The `setReturnValue` method is used to define a custom function that only returns a value and has no further business logic. It takes an object as an argument, which represents the value that should be returned by the custom function.

```java
  /**
   * Define a custom function that only returns a value and
   * has no further business logic (method body).
   *
   * It is not possible to use this method together with
   * {@link #setFunction}.
   *
   * @param result that should be returned by the custom function
   * @return the builder
   */
  CustomFunctionBuilder setReturnValue(Object result);
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-scala/src/main/java/org/camunda/bpm/dmn/feel/impl/scala/function/builder/CustomFunctionBuilder.java" line="58">

---

# Setting the Function

The `setFunction` method is used to pass a function with a list of objects as argument and an object as return value. This function will be called when the custom function is invoked.

```java
  /**
   * Pass a {@link Function} with a {@link List} of objects as argument
   * and an object as return value.
   *
   * It is not possible to use this method together with
   * {@link #setReturnValue}.
   *
   * @param function to be called
   * @return the builder
   */
  CustomFunctionBuilder setFunction(Function<List<Object>, Object> function);
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-scala/src/main/java/org/camunda/bpm/dmn/feel/impl/scala/function/builder/CustomFunctionBuilder.java" line="70">

---

# Building the Custom Function

The `build` method is used to create the custom function and register it in the `FeelCustomFunctionProvider`. It throws a `FeelException` when both `setFunction` and `setReturnValue` were called.

```java
  /**
   * Returns the custom function to be registered in
   * {@link FeelCustomFunctionProvider}.
   *
   * @throws FeelException when both {@link #setFunction} and {@link #setReturnValue} were called
   *
   * @return a custom function
   */
  CustomFunction build();
```

---

</SwmSnippet>

# CustomFunctionBuilder Functions

The CustomFunctionBuilder interface provides methods to define and build a custom function.

<SwmSnippet path="/engine-dmn/feel-scala/src/main/java/org/camunda/bpm/dmn/feel/impl/scala/function/builder/CustomFunctionBuilder.java" line="37">

---

## setParams

The `setParams` method is used to define the parameters of the custom function.

```java
  CustomFunctionBuilder setParams(String... params);
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-scala/src/main/java/org/camunda/bpm/dmn/feel/impl/scala/function/builder/CustomFunctionBuilder.java" line="44">

---

## enableVarargs

The `enableVarargs` method is used to enable variable arguments for the custom function.

```java
  CustomFunctionBuilder enableVarargs();
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-scala/src/main/java/org/camunda/bpm/dmn/feel/impl/scala/function/builder/CustomFunctionBuilder.java" line="56">

---

## setReturnValue

The `setReturnValue` method is used to define a custom function that only returns a value and has no further business logic.

```java
  CustomFunctionBuilder setReturnValue(Object result);
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-scala/src/main/java/org/camunda/bpm/dmn/feel/impl/scala/function/builder/CustomFunctionBuilder.java" line="68">

---

## setFunction

The `setFunction` method is used to pass a function with a list of objects as argument and an object as return value.

```java
  CustomFunctionBuilder setFunction(Function<List<Object>, Object> function);
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-scala/src/main/java/org/camunda/bpm/dmn/feel/impl/scala/function/builder/CustomFunctionBuilder.java" line="78">

---

## build

The `build` method is used to return the custom function to be registered in FeelCustomFunctionProvider.

```java
  CustomFunction build();
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
