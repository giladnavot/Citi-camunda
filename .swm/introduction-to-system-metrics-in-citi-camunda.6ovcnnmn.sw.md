---
title: Introduction to System Metrics in Citi-camunda
---
System Metrics in Citi-camunda refer to the quantitative measurements of the system's properties and performance. They provide insights into the system's behavior, resource utilization, and overall performance. Metrics can be collected at various levels, including the application level, process level, and system level. In the context of Citi-camunda, system metrics are used to monitor and optimize the performance of the Camunda BPM platform.

<SwmSnippet path="/webapps/frontend/ui/admin/plugins/base/app/resources/metrics.js" line="28">

---

## Fetching System Metrics

This section of the code defines the 'getAggregated' function, which is used to fetch system metrics. The 'method' property is set to 'GET', indicating that it's a read operation. The 'isArray' property is set to true, meaning the response will be an array. The 'params' property specifies the action to be 'aggregated', which means it will fetch aggregated metrics.

```javascript
        getAggregated: {
          method: 'GET',
          isArray: true,
          params: {action: 'aggregated'}
        }
```

---

</SwmSnippet>

# System Metrics Functions

This section will focus on the 'getAggregated' function, which is a key part of the System Metrics in the Citi-camunda project.

<SwmSnippet path="/webapps/frontend/ui/admin/plugins/base/app/resources/metrics.js" line="27">

---

## getAggregated Function

The 'getAggregated' function is a GET method that returns an array of aggregated metrics. It is used to fetch and aggregate system metrics from the server.

```javascript
      {
        getAggregated: {
          method: 'GET',
          isArray: true,
          params: {action: 'aggregated'}
        }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
