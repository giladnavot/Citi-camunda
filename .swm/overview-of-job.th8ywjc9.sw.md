---
title: Overview of Job
---
A Job in Citi-camunda refers to a unit of work that the process engine needs to execute. Jobs are created during the execution of asynchronous continuations and timer events. They are stored in the database and executed by the Job Executor.

Jobs can be managed through the REST API. The `engine-rest/engine-rest-openapi/src/main/templates/paths/job/` directory contains templates for various job-related operations such as getting job details (`get.ftl`), creating a job (`post.ftl`), updating job suspension state (`suspended/put.ftl`), and setting job retries (`retries/post.ftl`).

Each job has a unique ID and operations can be performed on a specific job using this ID. For example, the `job/{id}/` directory contains templates for operations like deleting a job (`delete.ftl`), getting a job's stacktrace (`stacktrace/get.ftl`), and executing a job (`execute/post.ftl`).

# Job Creation

This is where a Job is created when an asynchronous task is encountered in the process. The Job is then added to the Job queue for later execution.

# Job Execution

This is the Job Executor, which is responsible for executing the Jobs in the Job queue. It periodically polls the Job queue and executes the Jobs in it.

# Job Functions

Let's delve into the functions related to 'Job' in the Citi-camunda repository.

<SwmSnippet path="/spring-boot-starter/starter/src/main/java/org/camunda/bpm/spring/boot/starter/property/JobExecutionProperty.java" line="1">

---

## JobExecutionProperty.java

This file contains properties related to job execution. These properties are used to configure the job execution settings in the Camunda BPM platform.

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

<SwmSnippet path="/webapps/frontend/camunda-bpm-sdk-js/lib/api-client/resources/job.js" line="1">

---

## job.js

This file contains functions for managing jobs in the Camunda BPM platform. These functions include creating, updating, deleting, and retrieving jobs.

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

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
