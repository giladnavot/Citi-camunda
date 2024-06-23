---
title: Understanding API Clients
---
API Clients in the Citi-camunda repository refer to the software modules that interact with the Camunda Platform's API. They are responsible for sending requests to the server and handling the responses. The clients are implemented in Java and are located in the 'clients/java' directory. The 'ClientIT' class, for example, tests the functionality of the client by sending requests to the server and asserting the responses. The 'ClientRequestContext' interface provides methods for manipulating the request data, such as adding headers.

<SwmSnippet path="/clients/java/client/src/it/java/org/camunda/bpm/client/client/ClientIT.java" line="515">

---

# Creating an API Client

This code snippet shows how to create an API Client. The `create()` method is called to create a new `ExternalTaskClientBuilder`. The `baseUrl()` method is then called to set the base URL of the Camunda BPM Platform REST API. Finally, the `build()` method is called to create the `ExternalTaskClient`.

```java
  @Test
  public void shouldPerformAutoFetching() {
    ExternalTaskClient client = null;

    try {
      // given
      ExternalTaskClientBuilder clientBuilder = ExternalTaskClient.create()
        .baseUrl(BASE_URL);

      // when
      client = clientBuilder.build();

      // then
      assertThat(client.isActive()).isTrue();
    } finally {
```

---

</SwmSnippet>

<SwmSnippet path="/clients/java/client/src/it/java/org/camunda/bpm/client/client/ClientIT.java" line="261">

---

# Using an API Client

This code snippet shows how to use an API Client. The `subscribe()` method is called to subscribe to an external task topic. The `handler()` method is then called to set the handler for the tasks. Finally, the `open()` method is called to start fetching and locking tasks.

```java
  public void shouldUseCustomWorkerId() {
    // given
    engineRule.startProcessInstance(processDefinition.getId());

    ClientRule clientRule = new ClientRule(() -> ExternalTaskClient.create()
      .baseUrl(BASE_URL)
      .workerId("aWorkerId"));

    try {
      clientRule.before();

      // when
      clientRule.client().subscribe(EXTERNAL_TASK_TOPIC_FOO)
        .handler(handler)
        .open();

      // then
      clientRule.waitForFetchAndLockUntil(() -> !handler.getHandledTasks().isEmpty());
    } finally {
      clientRule.after();
    }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
