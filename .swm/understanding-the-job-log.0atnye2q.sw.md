---
title: Understanding the Job Log
---
Job Log in Citi-camunda refers to the historical record of jobs executed in the Camunda BPM platform. It provides detailed information about the execution of jobs, including any exceptions that occurred. This information is crucial for debugging and understanding the behavior of the system.

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/history/job-log/{id}/get.ftl" line="6">

---

# Accessing Job Log

This is the endpoint for getting a specific job log. You can use the job log ID as a parameter to retrieve the details of a specific job log.

```ftl
      tag = "Historic Job Log"
      summary = "Get Job Log"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/history/job-log/count/get.ftl" line="6">

---

# Getting Job Log Count

This endpoint is used to get the count of job logs. It can be useful when you want to know the total number of job logs in the system.

```ftl
      tag = "Historic Job Log"
      summary = "Get Job Log Count"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/history/job-log/{id}/stacktrace/get.ftl" line="6">

---

# Getting Job Log Exception Stacktrace

This endpoint is used to get the exception stacktrace of a job log. It can be useful when you are debugging a job that has failed and you want to understand the cause of the failure.

```ftl
      tag = "Historic Job Log"
      summary = "Get Job Log Exception Stacktrace"
```

---

</SwmSnippet>

# Job Log Functions

Job Log Functions

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/history/HistoricJobLog.java" line="0">

---

## HistoricJobLog

The `HistoricJobLog` interface provides methods to access the historic job log entries for a particular job. It includes information about the job's state and properties.

```java
/*
 * Copyright Camunda Services GmbH and/or licensed to Camunda Services GmbH
 * under one or more contributor license agreements. See the NOTICE file
 * distributed with this work for additional information regarding copyright
 * ownership. Camunda licenses this file to you under the Apache License,
 * Version 2.0; you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *     http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/history/HistoricJobLogQuery.java" line="0">

---

## HistoricJobLogQuery

The `HistoricJobLogQuery` interface provides methods to programmatic query the historic job log. It allows to filter the job logs based on various parameters like jobId, jobDefinitionId, etc.

```java
/*
 * Copyright Camunda Services GmbH and/or licensed to Camunda Services GmbH
 * under one or more contributor license agreements. See the NOTICE file
 * distributed with this work for additional information regarding copyright
 * ownership. Camunda licenses this file to you under the Apache License,
 * Version 2.0; you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *     http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/runtime/Job.java" line="0">

---

## Job

The `Job` interface provides methods to manage and manipulate jobs. It includes methods to retrieve job details, execute jobs, etc.

```java
/*
 * Copyright Camunda Services GmbH and/or licensed to Camunda Services GmbH
 * under one or more contributor license agreements. See the NOTICE file
 * distributed with this work for additional information regarding copyright
 * ownership. Camunda licenses this file to you under the Apache License,
 * Version 2.0; you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *     http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/history/job-log/post.ftl" line="1">

---

## Job Log REST API

The Job Log REST API provides endpoints to query and manage job logs. The `post.ftl` file defines the POST endpoint to query historic job logs. It allows filtering by job log values of different types such as `String`, `Number`, or `Boolean`.

```ftl
<#-- Generated From File: camunda-docs-manual/public/reference/rest/history/job-log/post-job-log-query/index.html -->
<#macro endpoint_macro docsUrl="">
{
  <@lib.endpointInfo
      id = "queryHistoricJobLogs"
      tag = "Historic Job Log"
      summary = "Get Job Logs (POST)"
      desc = "Queries for historic job logs that fulfill the given parameters.
              This method is slightly more powerful than the
              [Get Job Logs](${docsUrl}/reference/rest/history/job-log/get-job-log-query/)
              method because it allows filtering by historic job logs values of the
              different types `String`, `Number` or `Boolean`."
  />

  "parameters" : [

    <#assign last = true >
    <#include "/lib/commons/pagination-params.ftl">

  ],

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
