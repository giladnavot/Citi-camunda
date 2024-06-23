---
title: Getting Started with Resources in Citi-camunda
---
In Citi-camunda, 'Resources' refer to modules that provide an interface for interacting with different entities in the application. These entities include jobs, tasks, incidents, and process instances. Each resource module is designed to handle specific operations related to its entity, such as querying, counting, setting retries, and managing identity links. These operations are defined as methods within each resource module. The 'isArray' property is used to specify whether the response from a method should be an array or not.

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/resources/jobResource.js" line="18">

---

# Resource Definition

This is an example of a resource definition. The `Resource` is a function that returns an object with methods for interacting with job data. These methods include `query`, `count`, and `setRetries`.

```javascript
'use strict';

var Resource = [
  '$resource',
  'Uri',
  function($resource, Uri) {
    return $resource(
      Uri.appUri('engine://engine/:engine/job/:id/:action'),
      {id: '@id'},
      {
        query: {method: 'POST', isArray: true},
        count: {method: 'POST', isArray: false, params: {id: 'count'}},
        setRetries: {method: 'PUT', params: {action: 'retries'}}
      }
    );
  }
];

module.exports = Resource;
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/resources/main.js" line="24">

---

# Using Resources

Resources are used by requiring them in the necessary parts of the application. Here, several resources such as `processInstanceResource`, `jobResource`, and `jobDefinitionResource` are required and can be used in this module.

```javascript
var processDefinitionResource = require('./processDefinitionResource'),
  incidentResource = require('./incidentResource'),
  processInstanceResource = require('./processInstanceResource'),
  localExecutionVariableResource = require('./localExecutionVariableResource'),
  jobResource = require('./jobResource'),
  taskResource = require('./taskResource'),
  jobDefinitionResource = require('./jobDefinitionResource');
```

---

</SwmSnippet>

# Resource Functions

The resources in the Citi-camunda project are used to manage different aspects of the workflow and process automation. Each resource has specific functions that allow it to interact with the process engine and perform necessary operations.

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/resources/processDefinitionResource.js" line="29">

---

## Process Definition Resource

The `processDefinitionResource` is used to query process statistics, get BPMN 2.0 XML, and count the number of process definitions. It uses HTTP methods like GET and POST to interact with the process engine.

```javascript
      {
        queryStatistics: {
          method: 'GET',
          isArray: true,
          params: {
            id: 'statistics'
          }
        },
        queryActivityStatistics: {
          method: 'GET',
          isArray: true,
          params: {
            action: 'statistics'
          }
        },
        getBpmn20Xml: {
          method: 'GET',
          params: {action: 'xml'},
          cache: true
        },
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/resources/processInstanceResource.js" line="28">

---

## Process Instance Resource

The `processInstanceResource` is used to query and count the number of process instances. It uses the POST HTTP method to interact with the process engine.

```javascript
        query: {
          method: 'POST',
          isArray: true
        },

        count: {
          method: 'POST',
          isArray: false,
          params: {id: 'count'}
        },
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/resources/jobResource.js" line="18">

---

## Job Resource

The `jobResource` is used to query jobs, count the number of jobs, and set retries for jobs. It uses HTTP methods like POST and PUT to interact with the process engine.

```javascript
'use strict';

var Resource = [
  '$resource',
  'Uri',
  function($resource, Uri) {
    return $resource(
      Uri.appUri('engine://engine/:engine/job/:id/:action'),
      {id: '@id'},
      {
        query: {method: 'POST', isArray: true},
        count: {method: 'POST', isArray: false, params: {id: 'count'}},
        setRetries: {method: 'PUT', params: {action: 'retries'}}
      }
    );
  }
];

module.exports = Resource;
```

---

</SwmSnippet>

# Task Resource Endpoints

Task Resource API

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/resources/taskResource.js" line="28">

---

## TaskResource.query

The `query` method of the `TaskResource` is a POST method that returns an array of tasks. It does not require any specific parameters in the URL, as the task data is sent in the body of the POST request.

```javascript
    return $resource(endpoint, endpointParams, {
      query: {
        method: 'POST',
        isArray: true
      },
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/resources/taskResource.js" line="39">

---

## TaskResource.getIdentityLinks

The `getIdentityLinks` method of the `TaskResource` is a GET method that returns an array of identity links for a specific task. The task ID is required as a parameter in the URL.

```javascript
      getIdentityLinks: {
        method: 'GET',
        isArray: true,
        params: {action: 'identity-links'}
      },
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
