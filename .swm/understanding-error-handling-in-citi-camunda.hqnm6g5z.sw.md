---
title: Understanding Error Handling in Citi-camunda
---
Error handling in Citi-camunda is primarily managed through the use of exceptions. The codebase defines several custom exception classes, each corresponding to a specific type of error that can occur during the execution of the system. These exceptions include `EngineException`, `RestException`, `BadRequestException`, `NotFoundException`, `ConnectionLostException`, and `ValueMapperException`. Each of these exceptions is used in different parts of the codebase to handle specific error scenarios.

`EngineException` is thrown when something goes wrong during the engine execution, such as a persistence exception. `RestException` is thrown when a request from the engine's REST API fails. `BadRequestException` is thrown when an illegal operation is performed or the given data is invalid. `NotFoundException` is thrown if the task has been canceled and therefore does not exist anymore. `ConnectionLostException` is thrown if the connection could not be established. `ValueMapperException` is thrown when a value could not be mapped.

These exceptions are used throughout the codebase to handle errors and exceptions that may occur during the execution of the system. They provide a way to categorize and handle different types of errors in a consistent and meaningful way.

<SwmSnippet path="/clients/java/client/src/main/java/org/camunda/bpm/client/exception/EngineException.java" line="19">

---

# EngineException Class

The `EngineException` class is a custom exception used in Citi-camunda to indicate that something went wrong during the engine execution. It extends from the `RestException` class, and takes a message and a `RestException` as parameters in its constructor.

```java
/**
 * Thrown if something went wrong during the engine execution (e.g., a persistence exception occurred).
 */
public class EngineException extends RestException {

  public EngineException(String message, RestException restException) {
    super(message, restException);
  }

}
```

---

</SwmSnippet>

<SwmSnippet path="/clients/java/client/src/main/java/org/camunda/bpm/client/task/ExternalTaskService.java" line="45">

---

# Usage of EngineException

The `EngineException` is used in various methods of the `ExternalTaskService` class. It is thrown when something goes wrong during the engine execution, such as a persistence exception. This allows the calling code to catch and handle this exception as needed.

```java
   * @throws BadRequestException if an illegal operation was performed or the given data is invalid.
   * @throws EngineException if something went wrong during the engine execution (e.g., a persistence exception occurred)
   * @throws ConnectionLostException if the connection could not be established
   * @throws UnknownHttpErrorException if the HTTP status code is not known by the client
   */
  void lock(String externalTaskId, long lockDuration);

  /**
   * Locks a task by a given amount of time.
   *
   * Note: This method should be used to lock external tasks
   * that have been obtained without using the fetch & lock API.
   *
   * @param externalTask which lock will be extended
   * @param lockDuration specifies the lock duration in milliseconds
   *
   * @throws NotFoundException if the task doesn't exist or has already been canceled or completed
   * @throws BadRequestException if an illegal operation was performed or the given data is invalid.
   * @throws EngineException if something went wrong during the engine execution (e.g., a persistence exception occurred)
   * @throws ConnectionLostException if the connection could not be established
   * @throws UnknownHttpErrorException if the HTTP status code is not known by the client.
```

---

</SwmSnippet>

<SwmSnippet path="/clients/java/client/src/it/java/org/camunda/bpm/client/util/RecordingExternalTaskHandler.java" line="52">

---

# Handling EngineException

Here, the `EngineException` is caught in a try-catch block. When the exception is caught, the `failed` flag is set to true, indicating that an error occurred during the execution of the handler.

```java
      handler.execute(task, externalTaskService);
    } catch (EngineException ex) {
      failed = true;
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
