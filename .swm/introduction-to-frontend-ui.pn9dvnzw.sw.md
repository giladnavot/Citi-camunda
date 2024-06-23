---
title: Introduction to Frontend UI
---
The Frontend UI in Citi-camunda is structured into several modules, each serving a specific purpose. The 'webapps/frontend/ui' directory contains the main UI components such as 'common', 'tasklist', 'welcome', 'cockpit', and 'admin'. These components are responsible for the different views and functionalities provided to the user. The 'webapps/frontend/public/app' directory contains the public-facing part of the application, which includes the same modules as in 'webapps/frontend/ui'. The 'webapps/frontend/camunda-commons-ui/lib' directory contains various libraries and services used across the application, such as 'analytics', 'widgets', 'services', 'pages', 'filter', 'search', 'plugin', 'chart', 'resources', 'auth', 'util', and 'directives'. The 'addPlugin' function, for example, is used to add plugins to the application. The 'webapps/frontend/camunda-commons-ui/resources' directory contains resources such as stylesheets and fonts used in the application.

# Frontend UI Structure

The Frontend UI is divided into several modules, each located in its own directory. These include 'common', 'tasklist', 'welcome', 'cockpit', and 'admin'.

# Frontend Scripts

The 'scripts' directory contains scripts that are likely used across the different modules of the Frontend UI. These scripts could be for tasks such as license checking or data transformation.

# Public App Directory

The 'public/app' directory contains the public-facing parts of the different modules. These are the parts of the modules that are served to the user's browser.

# Camunda Commons UI Library

The 'camunda-commons-ui/lib' directory contains a library of UI components, services, and utilities that are likely used across the different modules of the Frontend UI.

<SwmSnippet path="/webapps/frontend/camunda-commons-ui/lib/plugin/service.js" line="56">

---

# Plugin Service

The 'addPlugin' function in 'service.js' is used to add a plugin to the application. Plugins can be used to extend the functionality of the application.

```javascript
      function addPlugin(plugins, definition) {
        var priority =
          typeof definition.priority !== 'undefined'
            ? definition.priority
            : -Infinity;

        // check from right to left (*-) where plugin
        // should be added
        for (var i = 0, p; (p = plugins[i]); i++) {
          if (typeof p.priority === 'undefined' || p.priority < priority) {
            plugins.splice(i, 0, definition);
            return;
          }
        }

        // not yet added; add to front
        plugins.push(definition);
      }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
