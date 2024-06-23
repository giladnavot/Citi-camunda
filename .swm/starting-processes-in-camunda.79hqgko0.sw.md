---
title: Starting Processes in Camunda
---
This document will cover the process of starting processes in the Camunda Platform, which includes:

1. Creating demo data for Admin, Cockpit, Tasklist, and Report.
2. Starting and completing invoice instances.
3. Completing external tasks.
4. Fetching and locking external tasks.

```mermaid
graph TD;
subgraph webapps/assembly/src/main/runtime/develop/java/org/camunda/bpm/pa
  startProcesses:::mainFlowStyle --> createAdminDemoData
end
subgraph webapps/assembly/src/main/runtime/develop/java/org/camunda/bpm/pa
  startProcesses:::mainFlowStyle --> createReportDemoData
end
subgraph webapps/assembly/src/main/runtime/develop/java/org/camunda/bpm/pa
  startProcesses:::mainFlowStyle --> createTasklistDemoData
end
subgraph webapps/assembly/src/main/runtime/develop/java/org/camunda/bpm/pa
  startProcesses:::mainFlowStyle --> createCockpitDemoData
end
subgraph webapps/assembly/src/main/java/org/camunda/bpm/admin/impl/web/SetupResource.java
  createAdminDemoData --> createInitialUser
end
subgraph webapps/assembly/src/main/java/org/camunda/bpm/admin/impl/web/SetupResource.java
  createInitialUser --> lookupProcessEngine
end
subgraph webapps/assembly/src/main/runtime/develop/java/org/camunda/bpm/pa
  createReportDemoData --> startAndCompleteReportingInstances
end
subgraph webapps/assembly/src/main/runtime/develop/java/org/camunda/bpm/pa
  createReportDemoData --> createProcessWithUserTask
end
subgraph webapps/frontend/camunda-bpm-sdk-js/lib/api-client/resources
  startAndCompleteReportingInstances --> complete
end
subgraph webapps/assembly/src/main/runtime/develop/java/org/camunda/bpm/pa
  createTasklistDemoData --> createDemoData
end
subgraph webapps/frontend/camunda-bpm-sdk-js/lib/api-client/http-client.js
  createDemoData --> put
end
subgraph webapps/assembly/src/main/runtime/develop/java/org/camunda/bpm/pa
  createCockpitDemoData:::mainFlowStyle --> createExternalTaskDemoData
end
subgraph webapps/assembly/src/main/runtime/develop/java/org/camunda/bpm/pa
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

<SwmSnippet path="/webapps/assembly/src/main/runtime/develop/java/org/camunda/bpm/pa/DevProcessApplication.java" line="348">

---

# Creating Admin Demo Data

The `createAdminDemoData` function is used to create a demo user for the Admin application. It sets up the user profile and credentials, and then calls the `createInitialUser` function to create the user in the system.

```java
  private void createAdminDemoData(ProcessEngine engine) throws Exception {
    UserDto user = new UserDto();
    UserProfileDto profile = new UserProfileDto();
    profile.setId("jonny1");
    profile.setFirstName("Jonny");
    profile.setLastName("Prosciutto");
    UserCredentialsDto credentials = new UserCredentialsDto();
    credentials.setPassword("jonny1");
    user.setProfile(profile);
    user.setCredentials(credentials);

    // manually perform setup
    new SetupResource().createInitialUser(engine.getName(), user);
  }
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/assembly/src/main/runtime/develop/java/org/camunda/bpm/pa/DevProcessApplication.java" line="283">

---

# Creating Cockpit Demo Data

The `createCockpitDemoData` function is used to create demo data for the Cockpit application. It creates tasks, completes some of them, fails others, and then creates more tasks. It also handles failures and completes tasks after they have failed.

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

<SwmSnippet path="/webapps/assembly/src/main/runtime/develop/java/org/camunda/bpm/pa/DevProcessApplication.java" line="487">

---

# Starting and Completing Invoice Instances

The `startAndCompleteReportingInstances` function is used to start and complete invoice instances. It creates a deployment, starts a number of process instances, and then completes tasks for those instances.

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

<SwmSnippet path="/webapps/frontend/camunda-bpm-sdk-js/lib/api-client/resources/external-task.js" line="136">

---

# Completing External Tasks

The `complete` function in the `ExternalTask` resource is used to complete an external task and update process variables. It makes a POST request to the `/complete` endpoint of the External Task API.

```javascript
/**
 * Complete an external task and update process variables.
 *
 * @param {Object} [params]
 * @param {String} [params.id]            The id of the task to complete.
 * @param {String} [params.workerId]      The id of the worker that completes the task. Must match the id of the worker who has most recently locked the task.
 * @param {String} [params.variables]     A JSON object containing variable key-value pairs.
 *
 * Each key is a variable name and each value a JSON variable value object with the following properties:
 *  Name	        Description
 *  value	        The variable's value. For variables of type Object, the serialized value has to be submitted as a String value.
 *                For variables of type File the value has to be submitted as Base64 encoded string.
 *  type	        The value type of the variable.
 *  valueInfo	    A JSON object containing additional, value-type-dependent properties.
 *                For serialized variables of type Object, the following properties can be provided:
 *                - objectTypeName: A string representation of the object's type name.
 *                - serializationDataFormat: The serialization format used to store the variable.
 *                For serialized variables of type File, the following properties can be provided:
 *                - filename: The name of the file. This is not the variable name but the name that will be used when downloading the file again.
 *                - mimetype: The mime type of the file that is being uploaded.
 *                - encoding: The encoding of the file that is being uploaded.
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/camunda-bpm-sdk-js/lib/api-client/resources/external-task.js" line="115">

---

# Fetching and Locking External Tasks

The `fetchAndLock` function in the `ExternalTask` resource is used to fetch and lock external tasks. It makes a POST request to the `/fetchAndLock` endpoint of the External Task API.

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

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="flows"><sup>Powered by [Swimm](/)</sup></SwmMeta>
