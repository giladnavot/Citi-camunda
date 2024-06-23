---
title: Basic Concepts of Historic Detail
---
In the context of the Citi-camunda repository, 'Detail' refers to the 'Historic Detail' feature of the Camunda Platform. This feature provides various functionalities related to the retrieval and management of historic details, which are specific pieces of information about the execution of a process. These details can include binary data, counts, and other specific data related to a process history.

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/history/detail/{id}/data/get.ftl" line="6">

---

## Get Historic Detail (Binary)

This endpoint is used to fetch the binary data of a historical detail. The 'id' in the path refers to the ID of the historical detail.

```ftl
      tag = "Historic Detail"
      summary = "Get Historic Detail (Binary)"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/history/detail/count/get.ftl" line="5">

---

## Get Historic Detail Count

This endpoint is used to get the count of historical details. It can be useful for understanding the volume of historical data for a process instance.

```ftl
      tag = "Historic Detail"
      summary = "Get Historic Detail Count"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/history/detail/{id}/get.ftl" line="6">

---

## Get Historic Detail

This endpoint is used to fetch a specific historical detail. The 'id' in the path refers to the ID of the historical detail.

```ftl
      tag = "Historic Detail"
      summary = "Get Historic Detail"
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
