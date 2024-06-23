---
title: Getting Started with Feel Juel EL Context
---
Feel Juel EL Context in Citi-camunda refers to a specific implementation of the ELContext class in the JUEL (Java Unified Expression Language) library. It's used within the Camunda BPMN platform for evaluating FEEL (Friendly Enough Expression Language) expressions. The FeelElContext class extends the ELContext class and provides methods to get ELResolver, FunctionMapper, and VariableMapper instances. These are used for resolving variables, functions, and mapping variables respectively within the context of FEEL expressions.

<SwmSnippet path="/engine-dmn/feel-juel/src/main/java/org/camunda/bpm/dmn/feel/impl/juel/el/FeelElContext.java" line="24">

---

# FeelElContext Class

The `FeelElContext` class extends `ELContext` and provides the context for evaluating expressions. It contains an `ELResolver`, `FunctionMapper`, and `VariableMapper` which are used for resolving expressions, mapping functions, and mapping variables respectively.

```java
public class FeelElContext extends ELContext {

  protected ELResolver elResolver;
  protected FunctionMapper functionMapper;
  protected VariableMapper variableMapper;

  public FeelElContext(ELResolver elResolver, FunctionMapper functionMapper, VariableMapper variableMapper) {
    this.elResolver = elResolver;
    this.functionMapper = functionMapper;
    this.variableMapper = variableMapper;
  }

  public ELResolver getELResolver() {
    return elResolver;
  }

  public FunctionMapper getFunctionMapper() {
    return functionMapper;
  }

  public VariableMapper getVariableMapper() {
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-juel/src/main/java/org/camunda/bpm/dmn/feel/impl/juel/el/FeelElContextFactory.java" line="33">

---

# FeelElContextFactory Class

The `FeelElContextFactory` class is where instances of `FeelElContext` are created. It uses the `createElResolver`, `createFunctionMapper`, and `createVariableMapper` methods to create the necessary components for the `FeelElContext`.

```java
public class FeelElContextFactory implements ElContextFactory {

  public static final FeelEngineLogger LOG = FeelLogger.ENGINE_LOGGER;

  protected CustomFunctionMapper customFunctionMapper = new CustomFunctionMapper();

  public ELContext createContext(ExpressionFactory expressionFactory, VariableContext variableContext) {
    ELResolver elResolver = createElResolver();
    FunctionMapper functionMapper = createFunctionMapper();
    VariableMapper variableMapper = createVariableMapper(expressionFactory, variableContext);

    return new FeelElContext(elResolver, functionMapper, variableMapper);
  }

  public ELResolver createElResolver() {
    return new SimpleResolver(true);
  }

  public FunctionMapper createFunctionMapper() {
    CompositeFunctionMapper functionMapper = new CompositeFunctionMapper();
    functionMapper.add(new FeelFunctionMapper());
```

---

</SwmSnippet>

# Feel Juel EL Context Functions

This section will cover the main functions of the Feel Juel EL Context in the Citi-camunda project.

<SwmSnippet path="/engine-dmn/feel-juel/src/main/java/org/camunda/bpm/dmn/feel/impl/juel/el/FeelElContext.java" line="24">

---

## FeelElContext

The `FeelElContext` class extends the `ELContext` class and is used to resolve expressions. It contains three main components: `ELResolver`, `FunctionMapper`, and `VariableMapper`. These components are used to resolve variables, functions, and types respectively in the expressions.

```java
public class FeelElContext extends ELContext {

  protected ELResolver elResolver;
  protected FunctionMapper functionMapper;
  protected VariableMapper variableMapper;

  public FeelElContext(ELResolver elResolver, FunctionMapper functionMapper, VariableMapper variableMapper) {
    this.elResolver = elResolver;
    this.functionMapper = functionMapper;
    this.variableMapper = variableMapper;
  }

  public ELResolver getELResolver() {
    return elResolver;
  }

  public FunctionMapper getFunctionMapper() {
    return functionMapper;
  }

  public VariableMapper getVariableMapper() {
```

---

</SwmSnippet>

<SwmSnippet path="/engine-dmn/feel-juel/src/main/java/org/camunda/bpm/dmn/feel/impl/juel/el/FeelElContextFactory.java" line="33">

---

## FeelElContextFactory

The `FeelElContextFactory` class is responsible for creating instances of `FeelElContext`. It uses the `createElResolver`, `createFunctionMapper`, and `createVariableMapper` methods to create the necessary components for the `FeelElContext`.

```java
public class FeelElContextFactory implements ElContextFactory {

  public static final FeelEngineLogger LOG = FeelLogger.ENGINE_LOGGER;

  protected CustomFunctionMapper customFunctionMapper = new CustomFunctionMapper();

  public ELContext createContext(ExpressionFactory expressionFactory, VariableContext variableContext) {
    ELResolver elResolver = createElResolver();
    FunctionMapper functionMapper = createFunctionMapper();
    VariableMapper variableMapper = createVariableMapper(expressionFactory, variableContext);

    return new FeelElContext(elResolver, functionMapper, variableMapper);
  }

  public ELResolver createElResolver() {
    return new SimpleResolver(true);
  }

  public FunctionMapper createFunctionMapper() {
    CompositeFunctionMapper functionMapper = new CompositeFunctionMapper();
    functionMapper.add(new FeelFunctionMapper());
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
