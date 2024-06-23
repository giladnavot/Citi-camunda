---
title: Exploring the Role of Templates in Citi-camunda
---
Templates in Citi-camunda are used to define the structure of the output that the engine-rest API produces. They are written in FreeMarker, a Java-based template engine, which can generate text output based on templates and changing data. Templates are used to generate responses for various API endpoints, such as the task/{id}/rendered-form endpoint. They provide a flexible way to control the format of the API response.

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/lib/commons/history-process-instance.ftl" line="133">

---

## Using Templates for Process Instances

This template is used to define the structure of a process instance. It includes a description field which provides information about the process instance.

```ftl
    "desc": "Only include process instances which have an incident in status either open or resolved. To get all process instances, use the query parameter withIncidents."
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/lib/commons/task-query-params.ftl" line="436">

---

## Using Templates for Tasks

This template is used to define the structure of a task. It includes a comment that describes a typical use case for the task.

```ftl
              typical use case is to query all `active` tasks for a user for a given date." />
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/models/org/camunda/bpm/engine/rest/dto/ExceptionDto.ftl" line="20">

---

## Using Templates for Exceptions

This template is used to define the structure of an exception. It includes a field that provides information about the exception codes.

```ftl
                You can look up the meaning of all built-in codes and learn how to add custom codes
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/models/org/camunda/bpm/engine/rest/dto/message/CorrelationMessageDto.ftl" line="107">

---

## Using Templates for Messages

This template is used to define the structure of a message. It includes a field that provides information about the usage of the resultEnabled parameter.

```ftl
                The parameter resultEnabled should be set to `true` in order to use this it.
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
