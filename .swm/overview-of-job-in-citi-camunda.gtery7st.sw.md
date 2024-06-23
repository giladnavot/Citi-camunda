---
title: Overview of Job in Citi-camunda
---
In Citi-camunda, a Job refers to a unit of work that the process engine needs to perform at a given time. These jobs can be created, retrieved, updated, and deleted through various API endpoints. Jobs can have different properties such as due date, priority, and retries. They can also be suspended or activated. Each job is identified by a unique ID and errors related to non-existent jobs are handled gracefully.

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/job/{id}/get.ftl" line="6">

---

# Job API Endpoints

This is the endpoint for retrieving a job by its id. It returns a job according to the `Job` interface in the engine.

```ftl
      tag = "Job"
      summary = "Get Job"
      desc = "Retrieves a job by id, according to the `Job` interface in the engine."
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/job/{id}/delete.ftl" line="5">

---

This is the endpoint for deleting a job. It removes the job with the given id from the system.

```ftl
      tag = "Job"
      summary = "Delete Job"
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/job/{id}/retries/put.ftl" line="6">

---

This is the endpoint for setting the number of retries for a job. It allows for the adjustment of the retry count for a job, which can be useful in handling failed jobs.

```ftl
      tag = "Job"
      summary = "Set Job Retries"
```

---

</SwmSnippet>

# Functions of Job

The 'Job' in Citi-camunda is a crucial part of the process automation. It is implemented in several files and has various functions.

<SwmSnippet path="/spring-boot-starter/starter/src/main/java/org/camunda/bpm/spring/boot/starter/property/JobExecutionProperty.java" line="1">

---

## JobExecutionProperty.java

In 'JobExecutionProperty.java', the 'Job' is defined as a property of the Spring Boot starter. It contains configurations for job execution such as the core pool size, max pool size, and queue capacity.

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
 */
package org.camunda.bpm.spring.boot.starter.property;

import static org.camunda.bpm.spring.boot.starter.property.CamundaBpmProperties.joinOn;

public class JobExecutionProperty {
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/camunda-bpm-sdk-js/lib/api-client/resources/job-definition.js" line="1">

---

## job-definition.js

In 'job-definition.js', the 'Job' is defined as a resource in the API client. It provides functions for interacting with job definitions such as retrieving a list of job definitions, getting a single job definition, and updating the suspension state of job definitions.

```javascript
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
 */

'use strict';

var AbstractClientResource = require('./../abstract-client-resource');

```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/camunda-bpm-sdk-js/lib/api-client/resources/job.js" line="1">

---

## job.js

In 'job.js', the 'Job' is also defined as a resource in the API client. It provides functions for interacting with jobs such as retrieving a list of jobs, getting a single job, and updating the suspension state of jobs.

```javascript
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
 */

'use strict';

var AbstractClientResource = require('./../abstract-client-resource');

```

---

</SwmSnippet>

# Job Suspension APIs

Job Suspension Endpoints

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/job/suspended/put.ftl" line="1">

---

## PUT `/job/suspended`

This endpoint is used to activate or suspend jobs matching a given criterion. The criterion can be one of `jobDefinitionId`, `processDefinitionId`, `processInstanceId`, or `processDefinitionKey`. The request body should be a JSON object containing the criterion and a `suspended` field indicating whether the job(s) should be suspended.

```ftl
<#macro endpoint_macro docsUrl="">
<#-- Generated From File: camunda-docs-manual/public/reference/rest/job/put-activate-suspend-by-proc-def-key/index.html -->
<#-- This file is actually based on four doc files found under put-activate-suspend-by-* as they all describe the same endpoint -->
{
  <@lib.endpointInfo
      id = "updateSuspensionStateBy"
      tag = "Job"
      summary = "Activate/Suspend Jobs"
      desc = "Activates or suspends jobs matching the given criterion.
              This can only be on of:
              * `jobDefinitionId`
              * `processDefinitionId`
              * `processInstanceId`
              * `processDefinitionKey`"
  />

  <@lib.requestBody
      mediaType = "application/json"
      dto = "JobSuspensionStateDto"
      examples = [
      '"example-1": {
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/paths/job/{id}/suspended/put.ftl" line="1">

---

## PUT `/job/{id}/suspended`

This endpoint is used to activate or suspend a specific job by its id. The id of the job is passed as a path parameter. The request body should be a JSON object with a `suspended` field indicating whether the job should be suspended.

```ftl
<#macro endpoint_macro docsUrl="">
<#-- Generated From File: camunda-docs-manual/public/reference/rest/job/put-activate-suspend-by-id/index.html -->
{
  <@lib.endpointInfo
      id = "updateJobSuspensionState"
      tag = "Job"
      summary = "Activate/Suspend Job By Id"
      desc = "Activates or suspends a given job by id."
  />

  "parameters" : [

      <@lib.parameter
          name = "id"
          location = "path"
          type = "string"
          required = true
          desc = "The id of the job to activate or suspend."
          last = true
      />

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
