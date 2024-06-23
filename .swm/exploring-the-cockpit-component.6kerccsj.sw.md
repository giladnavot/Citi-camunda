---
title: Exploring the Cockpit Component
---
Cockpit is a component of the Camunda Platform that allows process administrators to monitor running process instances, make decisions when problems arise, and analyze the history of completed process instances. It provides a visual interface for process instances and their associated data, making it easier to understand the state of the system and make informed decisions.

In the Citi-camunda codebase, Cockpit is implemented as a series of scripts and directives within the 'webapps/frontend/ui/cockpit' directory. These scripts handle various aspects of the Cockpit's functionality, such as form handling, resource management, and dashboard display.

For example, the 'cam-cockpit-form.js' script is responsible for handling forms within the Cockpit, while the 'dashboard.js' script manages the display of the Cockpit dashboard. These scripts work together to provide a comprehensive interface for process management.

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/camunda-cockpit-bootstrap.js" line="282">

---

# Initialization of Cockpit

The `initCockpitUi` function is used to initialize Cockpit. It clears any AMD globals and then calls the `init` function from `camunda-cockpit-ui.js` to set up the necessary dependencies.

```javascript
        function initCockpitUi(pluginDependencies) {
          /**
           * Clearing AMD globals is necessary so third-party AMD scripts users
           * register via script tag are prevented from registration via RequireJS
           * and made global on the window object.
           */
          function clearAmdGlobals() {
            window.define = undefined;
            window.require = undefined;
          }

          clearAmdGlobals();

          // now that we loaded the plugins and the additional modules, we can finally
          // initialize Cockpit
          camundaCockpitUi.init(pluginDependencies);
        }
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/repository/resources/directives/cam-cockpit-resources.js" line="34">

---

# Resource Management in Cockpit

Cockpit uses directives for resource management. The `controller` property in `cam-cockpit-resources.js` is an example of how resources are managed in Cockpit.

```javascript
      template: template,

      controller: [
        '$scope',
        '$location',
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/repository/deployments/directives/cam-cockpit-deployments.js" line="34">

---

# Deployment Management in Cockpit

Cockpit also uses directives for deployment management. The `deployments` property in `cam-cockpit-deployments.js` is an example of how deployments are managed in Cockpit.

```javascript
        deploymentsData: '=',
        totalItems: '=',
        deployments: '='
      },
      template: template,
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/repository/resource/directives/cam-cockpit-form.js" line="29">

---

# Form Handling in Cockpit

Cockpit handles forms through directives as well. The `name` and `source` properties in `cam-cockpit-form.js` are examples of how form data is handled in Cockpit.

```javascript
      scope: {
        name: '=',
        source: '='
      },
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
