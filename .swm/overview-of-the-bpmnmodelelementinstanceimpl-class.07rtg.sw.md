---
title: Overview of the BpmnModelElementInstanceImpl Class
---
This document will cover the `BpmnModelElementInstanceImpl` class in the Citi-camunda repository. We'll cover:

1. What is `BpmnModelElementInstanceImpl`.
2. Variables and functions of `BpmnModelElementInstanceImpl`.
3. An example of how to use `BpmnModelElementInstanceImpl`.

```mermaid
graph TD;
 BpmnModelElementInstance --> BpmnModelElementInstanceImpl:::currentBaseStyle
BpmnModelElementInstanceImpl --> PointImpl
PointImpl --> WaypointImpl
BpmnModelElementInstanceImpl --> CamundaGenericValueElementImpl
CamundaGenericValueElementImpl --> CamundaEntryImpl
CamundaGenericValueElementImpl --> CamundaInputParameterImpl
CamundaGenericValueElementImpl --> CamundaOutputParameterImpl
BpmnModelElementInstanceImpl --> StyleImpl
StyleImpl --> BpmnLabelStyleImpl
BpmnModelElementInstanceImpl --> 1[...]

 classDef currentBaseStyle color:#000000,fill:#7CB9F4
```

# What is BpmnModelElementInstanceImpl

`BpmnModelElementInstanceImpl` is a shared base class for all BPMN Model Elements. It provides an implementation of the `BpmnModelElementInstance` interface. This class is abstract and is extended by other classes in the codebase to provide specific functionality.

<SwmSnippet path="/model-api/bpmn-model/src/main/java/org/camunda/bpm/model/bpmn/impl/instance/BpmnModelElementInstanceImpl.java" line="34">

---

# Variables and functions

The constructor `BpmnModelElementInstanceImpl` takes a `ModelTypeInstanceContext` as an argument and passes it to the superclass constructor.

```java
  public BpmnModelElementInstanceImpl(ModelTypeInstanceContext instanceContext) {
    super(instanceContext);
  }
```

---

</SwmSnippet>

<SwmSnippet path="/model-api/bpmn-model/src/main/java/org/camunda/bpm/model/bpmn/impl/instance/BpmnModelElementInstanceImpl.java" line="39">

---

The function `builder` is used to create a new instance of the class. However, it throws an exception as it's not implemented in this class.

```java
  public AbstractBaseElementBuilder builder() {
    throw new BpmnModelException("No builder implemented for " + this);
  }
```

---

</SwmSnippet>

<SwmSnippet path="/model-api/bpmn-model/src/main/java/org/camunda/bpm/model/bpmn/impl/instance/BpmnModelElementInstanceImpl.java" line="43">

---

The function `isScope` checks if the current instance is of type `Process` or `SubProcess`. It returns a boolean value.

```java
  public boolean isScope() {
    return this instanceof org.camunda.bpm.model.bpmn.instance.Process || this instanceof SubProcess;
  }
```

---

</SwmSnippet>

<SwmSnippet path="/model-api/bpmn-model/src/main/java/org/camunda/bpm/model/bpmn/impl/instance/BpmnModelElementInstanceImpl.java" line="47">

---

The function `getScope` returns the scope of the current model element instance. It checks if the parent element is a scope, if not, it recursively checks the parent's scope.

```java
  public BpmnModelElementInstance getScope() {
    BpmnModelElementInstance parentElement = (BpmnModelElementInstance) getParentElement();
    if (parentElement != null) {
      if (parentElement.isScope()) {
        return parentElement;
      }
      else {
        return parentElement.getScope();
      }
    }
    else {
      return null;
    }
  }
```

---

</SwmSnippet>

<SwmSnippet path="/model-api/bpmn-model/src/main/java/org/camunda/bpm/model/bpmn/impl/instance/LoopDataOutputRef.java" line="32">

---

# Usage example

`LoopDataOutputRef` is an example of a class that extends `BpmnModelElementInstanceImpl`. It inherits all the methods and properties of `BpmnModelElementInstanceImpl` and can override or add new ones as needed.

```java
public class LoopDataOutputRef extends BpmnModelElementInstanceImpl {

  public static void registerType(ModelBuilder modelBuilder) {
    ModelElementTypeBuilder typeBuilder = modelBuilder
      .defineType(LoopDataOutputRef.class, BPMN_ELEMENT_LOOP_DATA_OUTPUT_REF)
      .namespaceUri(BPMN20_NS)
      .instanceProvider(
        new ModelElementTypeBuilder.ModelTypeInstanceProvider<LoopDataOutputRef>() {
          public LoopDataOutputRef newInstance(ModelTypeInstanceContext instanceContext) {
            return new LoopDataOutputRef(instanceContext);
          }
        });

    typeBuilder.build();
  }

  public LoopDataOutputRef(ModelTypeInstanceContext instanceContext) {
    super(instanceContext);
  }
}

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="general-class"><sup>Powered by [Swimm](/)</sup></SwmMeta>
