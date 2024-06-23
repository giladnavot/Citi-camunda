---
title: Generating Demo Data for the Camunda Platform
---
This document will cover the process of generating demo data for the Camunda platform, which includes:

 1. Running the main function
 2. Creating report demo data
 3. Creating cockpit demo data
 4. Starting invoice instances
 5. Claiming tasks
 6. Posting HTTP requests
 7. Ending HTTP requests
 8. Solving HALEmbedded
 9. Fetching and locking external tasks
10. Starting and completing reporting instances.

```mermaid
graph TD;
subgraph webapps/assembly/src/main/runtime/develop/java/org/camunda/bpm/pa/DevProcessApplication.java
  run:::mainFlowStyle --> createReportDemoData
end
subgraph webapps/assembly/src/main/runtime/develop/java/org/camunda/bpm/pa/DevProcessApplication.java
  run:::mainFlowStyle --> createCockpitDemoData
end
subgraph webapps/assembly/src/main/runtime/develop/java/org/camunda/bpm/pa/DevProcessApplication.java
  createReportDemoData --> startAndCompleteReportingInstances
end
subgraph webapps/assembly/src/main/runtime/develop/java/org/camunda/bpm/pa/DevProcessApplication.java
  createReportDemoData --> createProcessWithUserTask
end
subgraph webapps/frontend/camunda-bpm-sdk-js/lib/api-client/resources
  startAndCompleteReportingInstances --> complete
end
subgraph webapps/assembly/src/main/runtime/develop/java/org/camunda/bpm/pa/DevProcessApplication.java
  createCockpitDemoData:::mainFlowStyle --> createExternalTaskDemoData
end
subgraph webapps/assembly/src/main/runtime/develop/java/org/camunda/bpm/pa/DevProcessApplication.java
  createCockpitDemoData:::mainFlowStyle --> startInvoiceInstances
end
subgraph webapps/frontend/camunda-bpm-sdk-js/lib/api-client/resources
  createExternalTaskDemoData --> fetchAndLock
end
subgraph webapps/frontend/camunda-bpm-sdk-js/lib/api-client/resources
  createExternalTaskDemoData --> complete
end
subgraph webapps/frontend/camunda-bpm-sdk-js/lib/api-client/resources
  startInvoiceInstances:::mainFlowStyle --> complete
end
subgraph webapps/frontend/camunda-bpm-sdk-js/lib/api-client/resources
  startInvoiceInstances:::mainFlowStyle --> claim
end
subgraph webapps/frontend/camunda-bpm-sdk-js/lib/api-client/http-client.js
  claim:::mainFlowStyle --> post
end
subgraph webapps/frontend/camunda-bpm-sdk-js/lib/api-client/http-client.js
  post:::mainFlowStyle --> end
end
subgraph webapps/frontend/camunda-bpm-sdk-js/lib/utils.js
  end:::mainFlowStyle --> solveHALEmbedded
end
subgraph webapps/frontend/camunda-bpm-sdk-js/lib/utils.js
  solveHALEmbedded:::mainFlowStyle --> keys
end
subgraph webapps/frontend/camunda-bpm-sdk-js/lib/utils.js
  keys:::mainFlowStyle --> isId
end
  isId:::mainFlowStyle --> ...

 classDef mainFlowStyle color:#000000,fill:#7CB9F4
  classDef rootsStyle color:#000000,fill:#00FFF4
```

<SwmSnippet path="/webapps/assembly/src/main/runtime/develop/java/org/camunda/bpm/pa/DevProcessApplication.java" line="1">

---

# Running the main function

The `run` function is the main entry point for the application. It calls `createReportDemoData` and `createCockpitDemoData` to generate demo data for the Camunda platform.

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
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/assembly/src/main/runtime/develop/java/org/camunda/bpm/pa/DevProcessApplication.java" line="473">

---

# Creating report demo data

The `createReportDemoData` function generates random report data for the Camunda cockpit. It creates a process with a user task and starts and completes reporting instances.

```java
  protected void createReportDemoData(ProcessEngine engine) {

    LOGGER.info("Generating random report data for cockpit");

    Calendar instance = Calendar.getInstance();
    Date currentTime = instance.getTime();

    BpmnModelInstance model = createProcessWithUserTask("my-reporting-process", "Report Process");

    startAndCompleteReportingInstances(engine, model, currentTime, 24);
    startAndCompleteReportingInstances(engine, model, currentTime, 16);
    startAndCompleteReportingInstances(engine, model, currentTime, 8);
  }
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/assembly/src/main/runtime/develop/java/org/camunda/bpm/pa/DevProcessApplication.java" line="283">

---

# Creating cockpit demo data

The `createCockpitDemoData` function creates demo data for external tasks. It starts process instances, completes tasks, handles failures, and deletes process instances.

```java
  private void createExternalTaskDemoData(ProcessEngine engine) {
    RuntimeService runtimeService = engine.getRuntimeService();
    ExternalTaskService externalTaskService = engine.getExternalTaskService();
    String workerId = "AWorker";
    String topicName = "ATopic";
    long lockDuration = 5 * 60L * 1000L;
    String errorDetails = "java.lang.RuntimeException: A exception message!\n" +
      "  at org.camunda.bpm.pa.service.FailingDelegate.execute(FailingDelegate.java:10)\n" +
      "  at org.camunda.bpm.engine.impl.delegate.JavaDelegateInvocation.invoke(JavaDelegateInvocation.java:34)\n" +
      "  at org.camunda.bpm.engine.impl.delegate.DelegateInvocation.proceed(DelegateInvocation.java:37)\n" +
      "  ...\n";


    // create 5 tasks
    for(int i=0; i<5; i++) {
      runtimeService.startProcessInstanceByKey("SimpleExternalTaskProcess");
    }

    // complete two tasks
    List<LockedExternalTask> lockedTasks = externalTaskService.fetchAndLock(2, workerId, false)
      .topic(topicName, lockDuration)
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/assembly/src/main/runtime/develop/java/org/camunda/bpm/pa/DevProcessApplication.java" line="1">

---

# Starting invoice instances

The `startInvoiceInstances` function is called by `createCockpitDemoData`. It completes and claims tasks.

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
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/camunda-bpm-sdk-js/lib/api-client/resources/task.js" line="1">

---

# Claiming tasks

The `claim` function is used to claim tasks. It sends a POST request via the `post` function.

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
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/camunda-bpm-sdk-js/lib/api-client/http-client.js" line="108">

---

# Posting HTTP requests

The `post` function performs a POST HTTP request. It sets headers, sends data, and ends the request.

```javascript
/**
 * Performs a POST HTTP request
 */
HttpClient.prototype.post = function(path, options) {
  options = options || {};
  var done = options.done || noop;
  var self = this;
  var deferred = Q.defer();
  var url = this.config.baseUrl + (path ? '/' + path : '');
  var req = request.post(url);

  var headers = options.headers || this.config.headers;
  headers.Accept = headers.Accept || this.config.headers.Accept;

  var isFieldOrAttach = false;
  // Buffer object is only available in node.js environement
  if (typeof Buffer !== 'undefined') {
    Object.keys(options.fields || {}).forEach(function(field) {
      req.field(field, options.fields[field]);
      isFieldOrAttach = true;
    });
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/camunda-bpm-sdk-js/lib/api-client/http-client.js" line="55">

---

# Ending HTTP requests

The `end` function is called at the end of the HTTP request. It handles errors and processes the response.

```javascript
function end(self, done, deferred) {
  done = done || noop;
  return function(err, response) {
    // TODO: investigate the possible problems related to response without content
    if (err || (!response.ok && !response.noContent)) {
      err =
        err ||
        response.error ||
        new Error(
          'The ' +
            response.req.method +
            ' request on ' +
            response.req.url +
            ' failed'
        );
      if (response && response.body) {
        if (response.body.message) {
          err.message = response.body.message;
        }
      }
      self.trigger('error', err);
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/camunda-bpm-sdk-js/lib/utils.js" line="25">

---

# Solving HALEmbedded

The `solveHALEmbedded` function is used to process embedded resources in the response.

```javascript
utils.solveHALEmbedded = function(results) {
  function isId(str) {
    if (str.slice(-2) !== 'Id') {
      return false;
    }

    var prop = str.slice(0, -2);
    var embedded = results._embedded;
    return !!(embedded[prop] && !!embedded[prop].length);
  }

  function keys(obj) {
    var arr = Object.keys(obj);

    for (var a in arr) {
      if (arr[a][0] === '_' || !isId(arr[a])) {
        arr.splice(a, 1);
      }
    }

    return arr;
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/camunda-bpm-sdk-js/lib/api-client/resources/external-task.js" line="115">

---

# Fetching and locking external tasks

The `fetchAndLock` function is used to fetch and lock external tasks. It sends a POST request with the workerId and maxTasks parameters.

```javascript
/**
 * Query for the number of external tasks that fulfill given parameters. Takes the same parameters as the get external tasks method.
 *
 * @param {Object} [params]
 * @param {String} [params.workerId]         Mandatory. The id of the worker on which behalf tasks are fetched. The returned tasks are locked for that worker and can only be completed when providing the same worker id.
 * @param {String} [params.maxTasks]         Mandatory. The maximum number of tasks to return.
 * @param {String} [params.topics]           A JSON array of topic objects for which external tasks should be fetched. The returned tasks may be arbitrarily distributed among these topics.
 *
 * Each topic object has the following properties:
 *  Name	         Description
 *  topicName	   Mandatory. The topic's name.
 *  lockDuration	 Mandatory. The duration to lock the external tasks for in milliseconds.
 *  variables	   A JSON array of String values that represent variable names. For each result task belonging to this topic, the given variables are returned as well if they are accessible from the external task's execution.
 */
ExternalTask.fetchAndLock = function(params, done) {
  return this.http.post(this.path + '/fetchAndLock', {
    data: params,
    done: done
  });
};
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/assembly/src/main/runtime/develop/java/org/camunda/bpm/pa/DevProcessApplication.java" line="487">

---

# Starting and completing reporting instances

The `startAndCompleteReportingInstances` function starts and completes reporting instances for the report demo data. It creates a deployment, starts process instances, and completes tasks.

```java
  protected void startAndCompleteReportingInstances(ProcessEngine engine, BpmnModelInstance model, Date currentTime, int offset) {
    Calendar calendar = Calendar.getInstance();

    int currentMonth = calendar.get(Calendar.MONTH);
    int currentYear = calendar.get(Calendar.YEAR);

    calendar.add(Calendar.MONTH, offset * (-1));
    ClockUtil.setCurrentTime(calendar.getTime());

    createDeployment(engine, "reports", model);

    RuntimeService runtimeService = engine.getRuntimeService();
    TaskService taskService = engine.getTaskService();

    while (calendar.get(Calendar.YEAR) < currentYear || calendar.get(Calendar.MONTH) <= currentMonth) {

      int numOfInstances = getRandomBetween(10, 50);

      for(int i = 0; i <= numOfInstances; i++) {
        ProcessInstance pi = runtimeService.startProcessInstanceByKey("my-reporting-process");

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="flows"><sup>Powered by [Swimm](/)</sup></SwmMeta>
