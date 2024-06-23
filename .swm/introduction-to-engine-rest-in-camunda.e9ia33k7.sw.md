---
title: Introduction to Engine REST in Camunda
---
Engine REST in Citi-camunda refers to the REST API provided by the Camunda BPM platform. This API allows developers to interact with the process engine and perform various operations such as starting a process instance, completing a task, or retrieving process definitions. The API is designed to be highly flexible and integrable, making it easy to embed within any Java application.

<SwmSnippet path="/engine-rest/engine-rest/src/main/java/org/camunda/bpm/engine/rest/impl/AbstractProcessEngineRestServiceImpl.java" line="149">

---

# Engine REST Implementation

The `getUserRestService` method is an example of how the REST API is implemented. It creates a new instance of `UserRestServiceImpl`, which provides the REST API for user-related operations. The `engineName` parameter is used to specify which process engine to use.

```java
  public UserRestService getUserRestService(String engineName) {
    String rootResourcePath = getRelativeEngineUri(engineName).toASCIIString();
    UserRestServiceImpl subResource = new UserRestServiceImpl(engineName, getObjectMapper());
    subResource.setRelativeRootResourceUri(rootResourcePath);
    return subResource;
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest/src/main/java/org/camunda/bpm/engine/rest/impl/history/HistoricProcessDefinitionRestServiceImpl.java" line="36">

---

# Engine REST Usage

The `HistoricProcessDefinitionRestServiceImpl` class extends `AbstractRestProcessEngineAware`, which means it can use the REST API provided by the engine. This class provides the REST API for operations related to historic process definitions.

```java
public class HistoricProcessDefinitionRestServiceImpl extends AbstractRestProcessEngineAware implements HistoricProcessDefinitionRestService {
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
