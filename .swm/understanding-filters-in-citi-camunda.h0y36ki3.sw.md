---
title: Understanding Filters in Citi-camunda
---
In Citi-camunda, a Filter refers to a functionality that allows users to create, update, delete, and execute operations on data. It is used to manage and manipulate data according to specific criteria. Filters are identified by unique IDs and can be used to retrieve single or multiple results. They are also used to count the number of data entries that meet the specified criteria.

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/filter/create/post.ftl" line="6">

---

# Creating a Filter

This is where a new filter is created. The 'Create Filter' endpoint is used to define a new filter.

```ftl
      tag = "Filter"
      summary = "Create Filter"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/filter/{id}/put.ftl" line="6">

---

# Updating a Filter

This is where an existing filter is updated. The 'Update Filter' endpoint is used to modify the properties of a filter.

```ftl
      tag = "Filter"
      summary = "Update Filter"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/filter/{id}/delete.ftl" line="6">

---

# Deleting a Filter

This is where a filter is deleted. The 'Delete Filter' endpoint is used to remove a filter.

```ftl
      tag = "Filter"
      summary = "Delete Filter"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/filter/{id}/list/get.ftl" line="6">

---

# Executing a Filter

This is where a filter is executed on a data set. The 'Execute Filter List' endpoint is used to apply a filter to a data set and return the filtered results.

```ftl
      tag = "Filter"
      summary = "Execute Filter List"
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
