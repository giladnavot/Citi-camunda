---
title: API
---
This document will cover the following topics:

1. Overview of the API and its endpoints.
2. Where to find the list of endpoints.
3. Explanation of API documentation tools available in the repo.

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/main.ftl" line="6">

---

# Overview of the API

The API is titled 'Camunda Platform REST API' and provides an OpenApi Spec for the Camunda Platform REST API. The API version is determined by the `cambpmVersion` variable. The API documentation can be found at the URL specified in `docsUrl`.

```ftl
  "info": {
    "title": "Camunda Platform REST API",
    "description": "OpenApi Spec for Camunda Platform REST API.",
    "version": "${cambpmVersion}",
    "license": {
      "name": "Apache License 2.0",
      "url": "http://www.apache.org/licenses/LICENSE-2.0.html"
    }
  },
  "externalDocs": {
    "description": "Find out more about Camunda Rest API",
    "url": "${docsUrl}/reference/rest/overview/"
  },
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest-openapi/src/main/templates/main.ftl" line="91">

---

# API Endpoints

The API endpoints are defined in the `paths` object. Each endpoint is represented by a path and a list of methods. The details of each method are imported from the respective `.ftl` file.

```ftl
  "paths": {

    <#list endpoints as path, methods>
        "${path}": {
            <#list methods as method>
                <#import "/paths${path}/${method}.ftl" as endpoint>
                "${method}":
                <@endpoint.endpoint_macro docsUrl=docsUrl/><#sep>,
            </#list>
        }<#sep>,
    </#list>

  },
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/form/directives/cam-tasklist-form.js" line="124">

---

# API Documentation Tools

The API is available via the `API` object in the `cam-tasklist-form.js` file. This object is used to set the asynchronous form key and parse the form.

```javascript
        var API = this;

        function setAsynchronousFormKey(formKey) {
          $scope.asynchronousFormKey.key = formKey;
          $scope.asynchronousFormKey.loaded = true;
        }

        function parseForm(form) {
          // Form is already parsed
          if (form.type) {
            setAsynchronousFormKey(form.key);
            return;
          }

          var key = form.key,
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/common/scripts/services/plugins/getApiAttributes.js" line="26">

---

The `getApiAttributes` function in the `getApiAttributes.js` file provides the base API and other related APIs such as `adminApi`, `baseApi`, `cockpitApi`, `tasklistApi`, and `engineApi`. It also provides the CSRF token.

```javascript
  const base = document.querySelector('base');
  const regex = new RegExp(`.*${appName}\/([^/]*).*`);
  const engine = window.location.href.replace(regex, '$1');

  return {
    api: {
      adminApi: base.getAttribute('admin-api').slice(0, -1),
      baseApi: base.getAttribute('engine-api').slice(0, -1),
      cockpitApi: base.getAttribute('cockpit-api').slice(0, -1),
      tasklistApi: base.getAttribute('tasklist-api').slice(0, -1),
      engineApi: base.getAttribute('engine-api') + 'engine/' + engine,
      engine,
      CSRFToken: getCSRFToken(CSRFCookieName)
    },
    ...params
  };
};
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="api"><sup>Powered by [Swimm](/)</sup></SwmMeta>
