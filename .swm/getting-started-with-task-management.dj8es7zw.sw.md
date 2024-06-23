---
title: Getting Started with Task Management
---
Task Management in Citi-camunda refers to the handling of tasks in the context of workflow and process automation. It involves the interaction with fetched and locked tasks, which is facilitated by the `ExternalTaskService` interface. This interface provides methods to lock and unlock tasks, complete tasks, and set variables for tasks. Tasks are represented by the `ExternalTask` interface, which provides details such as the task's id, worker id, lock expiration time, and process definition details. Task Management is crucial in controlling the flow of the process automation, ensuring tasks are properly assigned, executed, and completed.

<SwmSnippet path="/clients/java/client/src/main/java/org/camunda/bpm/client/task/ExternalTask.java" line="32">

---

# ExternalTask Interface

The `ExternalTask` interface represents an external task. It provides methods to get information about the task, such as its ID, activity ID, error message, and more. It also provides methods to get and set variables associated with the task.

```java
public interface ExternalTask {

  /**
   * @return the id of the activity that this external task belongs to
   */
  String getActivityId();

  /**
   * @return the id of the activity instance that the external task belongs to
   */
  String getActivityInstanceId();

  /**
   * @return the error message that was supplied when the last failure of this task was reported
   */
  String getErrorMessage();

  /**
   * @return the error details submitted with the latest reported failure executing this task
   */
  String getErrorDetails();
```

---

</SwmSnippet>

<SwmSnippet path="/clients/java/client/src/main/java/org/camunda/bpm/client/task/ExternalTaskService.java" line="33">

---

# ExternalTaskService Interface

The `ExternalTaskService` interface provides methods to interact with tasks. This includes locking a task for a given amount of time, unlocking a task, and completing a task. It also provides methods to set variables for a task.

```java
public interface ExternalTaskService {

  /**
   * Locks a task by a given amount of time.
   *
   * Note: This method should be used to lock external tasks
   * that have been obtained without using the fetch & lock API.
   *
   * @param externalTaskId the id of the external task whose lock will be extended
   * @param lockDuration specifies the lock duration in milliseconds
   *
   * @throws NotFoundException if the task doesn't exist or has already been canceled or completed
   * @throws BadRequestException if an illegal operation was performed or the given data is invalid.
   * @throws EngineException if something went wrong during the engine execution (e.g., a persistence exception occurred)
   * @throws ConnectionLostException if the connection could not be established
   * @throws UnknownHttpErrorException if the HTTP status code is not known by the client
   */
  void lock(String externalTaskId, long lockDuration);

  /**
   * Locks a task by a given amount of time.
```

---

</SwmSnippet>

<SwmSnippet path="/clients/java/client/src/main/java/org/camunda/bpm/client/task/impl/ExternalTaskServiceImpl.java" line="40">

---

# Usage of ExternalTask and ExternalTaskService

The `ExternalTaskServiceImpl` class provides an implementation of the `ExternalTaskService` interface. It uses the `ExternalTask` interface to interact with tasks. For example, the `lock` method locks a task by calling the `getId` method of the `ExternalTask` interface.

```java
  @Override
  public void lock(ExternalTask externalTask, long lockDuration) {
    lock(externalTask.getId(), lockDuration);
  }

  @Override
  public void lock(String externalTaskId, long lockDuration) {
    try {
      engineClient.lock(externalTaskId, lockDuration);
    } catch (EngineClientException e) {
      throw LOG.handledEngineClientException("locking task", e);
    }
  }

  @Override
  public void unlock(ExternalTask externalTask) {
    try {
      engineClient.unlock(externalTask.getId());
    } catch (EngineClientException e) {
      throw LOG.handledEngineClientException("unlocking the external task", e);
    }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
