---
title: Getting Started with Paths in OpenAPI Documentation
---
In the Citi-camunda repository, 'Paths' refer to the directory structure that organizes the various FreeMarker template files (.ftl files). These templates are used to generate the OpenAPI documentation for the Camunda REST API. Each subdirectory under the 'paths' directory corresponds to a specific endpoint of the REST API, such as 'process-definition', 'signal', 'external-task', etc. The .ftl files within these subdirectories define the GET, POST, and other HTTP methods for the corresponding endpoint.

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/process-definition/{id}/restart/post.ftl" line="11">

---

# Restarting a Process

This path is used to restart a process. To execute the restart asynchronously, a POST request is made to this endpoint.

```ftl
              To execute the restart asynchronously, use the
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/modification/execute/post.ftl" line="9">

---

# Modifying a Process Instance

This path is used to modify a single process instance. To execute a modification asynchronously, a POST request is made to this endpoint.

```ftl
              To modify a single process instance, use the
              [Modify Process Instance Execution State](${docsUrl}/reference/rest/process-instance/post-modification/) method.
              To execute a modification asynchronously, use the
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/migration/execute/post.ftl" line="9">

---

# Executing a Migration Plan

This path is used to execute a migration plan. To execute the plan asynchronously, a POST request is made to this endpoint.

```ftl
              a migration plan asynchronously, use the
```

---

</SwmSnippet>

# API Endpoints Overview

Understanding API Endpoints

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/process-definition/{id}/static-called-process-definitions/get.ftl" line="1">

---

## getStaticCalledProcessDefinitions

The `getStaticCalledProcessDefinitions` endpoint retrieves a list of called process definitions for a given process. These are all process definitions that are referenced statically by call activities in the given process. The endpoint does not resolve process definitions that are referenced with expressions.

```ftl
<#-- Generated From File: camunda-docs-manual/public/reference/rest/process-definition/get-static-called-process-definitions/index.html -->
<#macro endpoint_macro docsUrl="">
{
  <@lib.endpointInfo
      id = "getStaticCalledProcessDefinitions"
      tag = "Process Definition"
      summary = "Get Static Called Process Definitions"
      desc = "For the given process, returns a list of called process definitions corresponding
              to
              the `CalledProcessDefinition` interface in the engine. The list
              contains all process definitions
              that are referenced statically by call activities in the given
              process. This endpoint does not
              resolve process definitions that are referenced with expressions. Each
              called process definition
              contains a list of call activity ids, which specifies the call
              activities that are calling that
              process. This endpoint does not resolve references to case
              definitions."
  />

```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/job-definition/{id}/jobPriority/put.ftl" line="1">

---

## setJobPriorityJobDefinition

The `setJobPriorityJobDefinition` endpoint sets an overriding execution priority for jobs with the given definition id. Optionally, the priorities of all the definitions' existing jobs are updated accordingly. The priority can be reset by setting it to `null`, meaning that a new job's priority will not be determined based on its definition's priority any longer.

```ftl
<#-- Generated From File: camunda-docs-manual/public/reference/rest/job-definition/put-set-job-priority/index.html -->
<#macro endpoint_macro docsUrl="">
{
  <@lib.endpointInfo
      id = "setJobPriorityJobDefinition"
      tag = "Job Definition"
      summary = "Set Job Definition Priority by Id"
      desc = "Sets an overriding execution priority for jobs with the given definition id.
              Optionally, the priorities of all the definitions' existing jobs are
              updated accordingly. The priority can be reset by setting it to
              `null`, meaning that a new job's priority will not be determined based
              on its definition's priority any longer. See the
              [user guide on job prioritization](${docsUrl}/user-guide/process-engine/the-job-executor/#set-job-definition-priorities-via-managementservice-api)
              for details."
  />

  "parameters" : [

      <@lib.parameter
          name = "id"
          location = "path"
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
