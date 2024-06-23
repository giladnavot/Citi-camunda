---
title: Exploration of Services
---
Services in Citi-camunda refer to the various functionalities provided by the application. They are modular pieces of code that perform specific tasks and can be reused throughout the application. For instance, services can handle tasks such as transforming data, managing query results, escaping HTML, managing breadcrumbs, and handling variables.

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/services/main.js" line="27">

---

## Using Services

In this example, several services are imported and used in the `main.js` file. These services include `page`, `camAPI`, `hasPlugin`, `localConf`, and `typeUtils`. Each of these services provides specific functionality that is used in the application.

```javascript
  page = require('./../../../../common/scripts/services/page'),
  camAPI = require('./../../../../common/scripts/services/cam-api'),
  hasPlugin = require('./../../../../common/scripts/services/has-plugin'),
  localConf = require('camunda-commons-ui/lib/services/cam-local-configuration'),
  typeUtils = require('./../../../../common/scripts/services/typeUtils'),
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
