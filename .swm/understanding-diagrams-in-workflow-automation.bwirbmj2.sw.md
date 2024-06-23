---
title: Understanding Diagrams in Workflow Automation
---
A Diagram in the context of the Citi-camunda repository refers to the graphical representation of a workflow or process. It is an essential part of the Camunda BPMN 2.0 process engine. The Diagram is composed of various elements, represented by the `DiagramElement` class, which can be either a `DiagramNode` or a `DiagramEdge`. A `DiagramNode` represents a node in the diagram, storing its position and dimensions, while a `DiagramEdge` represents an edge in the diagram, storing its waypoints. The `DiagramLayout` class stores the two-dimensional graph layout of the diagram, including all its nodes and edges.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/DiagramElement.java" line="21">

---

# DiagramElement Class

The DiagramElement class is an abstract class that represents a diagram node. It has an id property and two abstract methods: isNode() and isEdge(). These methods are used to check if the diagram element is a node or an edge.

```java
/**
 * Represents a diagram node.
 *
 * @author Falko Menge
 */
abstract public class DiagramElement implements Serializable {

  private static final long serialVersionUID = 1L;
  
  protected String id = null;

  public DiagramElement() {
  }

  public DiagramElement(String id) {
    this.id = id;
  }

  /**
   * Id of the diagram element.
   */
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/DiagramNode.java" line="19">

---

# DiagramNode Class

The DiagramNode class extends the DiagramElement class and represents a diagram node. It has properties for the position (x, y) and dimensions (width, height) of the node. It overrides the isNode() method to return true and the isEdge() method to return false.

```java
/**
 * Stores position and dimensions of a diagram node.
 *
 * @author Falko Menge
 */
public class DiagramNode extends DiagramElement {

  private static final long serialVersionUID = 1L;

  private Double x = null;
  private Double y = null;
  private Double width = null;
  private Double height = null;

  public DiagramNode() {
    super();
  }
  
  public DiagramNode(String id) {
    super(id);
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/DiagramLayout.java" line="33">

---

# DiagramLayout Class

The DiagramLayout class manages the layout of the diagram nodes. It has a Map property 'elements' that stores the diagram elements. It provides methods to get a node by id, get all nodes, and get all elements.

```java
  private static final long serialVersionUID = 1L;
  
  private Map<String, DiagramElement> elements;

  public DiagramLayout(Map<String, DiagramElement> elements) {
    this.setElements(elements);
  }

  public DiagramNode getNode(String id) {
    DiagramElement element = getElements().get(id);
    if (element instanceof DiagramNode) {
      return (DiagramNode) element;
    } else {
      return null;
    }
  }
  
  public DiagramEdge getEdge(String id) {
    DiagramElement element = getElements().get(id);
    if (element instanceof DiagramEdge) {
      return (DiagramEdge) element;
```

---

</SwmSnippet>

# Diagram Functionality

This section covers the main functions related to the Diagram functionality in the Citi-camunda repository.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/DiagramLayout.java" line="26">

---

## DiagramLayout Class

The DiagramLayout class stores a two-dimensional graph layout. It contains methods to manipulate and retrieve information about the elements of the diagram. The getNode and getEdge methods retrieve a node or edge from the diagram by its ID. The getElements and setElements methods are used to get and set the elements of the diagram. The getNodes method retrieves all the nodes in the diagram.

```java
/**
 * Stores a two-dimensional graph layout.
 *
 * @author Falko Menge
 */
public class DiagramLayout implements Serializable {

  private static final long serialVersionUID = 1L;
  
  private Map<String, DiagramElement> elements;

  public DiagramLayout(Map<String, DiagramElement> elements) {
    this.setElements(elements);
  }

  public DiagramNode getNode(String id) {
    DiagramElement element = getElements().get(id);
    if (element instanceof DiagramNode) {
      return (DiagramNode) element;
    } else {
      return null;
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/DiagramElement.java" line="26">

---

## DiagramElement Class

The DiagramElement class represents a diagram node. It contains methods to manipulate and retrieve information about the diagram element. The getId method retrieves the ID of the diagram element. The isNode and isEdge methods check whether the diagram element is a node or an edge.

```java
abstract public class DiagramElement implements Serializable {

  private static final long serialVersionUID = 1L;
  
  protected String id = null;

  public DiagramElement() {
  }

  public DiagramElement(String id) {
    this.id = id;
  }

  /**
   * Id of the diagram element.
   */
  public String getId() {
    return id;
  }

  public void setId(String id) {
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
