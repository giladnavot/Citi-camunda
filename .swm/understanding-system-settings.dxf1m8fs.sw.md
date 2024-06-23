---
title: Understanding System Settings
---
System Settings in Citi-camunda refers to the configuration settings of the Camunda platform. It includes settings related to the process engine, plugins, and other system components. The settings are managed through the 'admin.system' component, which provides an interface for viewing and modifying these settings. The system settings are organized into different sections, each managed by a provider. Each provider is responsible for a specific set of settings, identified by an 'id', and has a priority that determines its order in the settings interface.

<SwmSnippet path="/webapps/frontend/ui/admin/client/scripts/pages/system.js" line="54">

---

## System Settings Providers

This section of the code retrieves all the system settings providers registered with the ViewsProvider service. Each provider is a plugin that manages a specific system setting. If the plugin defines an access function, it is invoked to determine if the current user has access to the setting.

```javascript
    $scope.systemSettingsProviders = Views.getProviders({
      component: 'admin.system'
    }).map(function(plugin) {
      if (angular.isArray(plugin.access)) {
        var fn = $injector.invoke(plugin.access);

        fn(function(err, access) {
          if (err) {
            throw err;
          }

          plugin.accessible = access;
        });
      } else {
        plugin.accessible = true;
      }

      return plugin;
    });
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/client/scripts/pages/systemSettingsGeneral.js" line="32">

---

## Registering a System Settings Provider

This section of the code demonstrates how to register a system settings provider. The provider is registered with the ViewsProvider service under the 'admin.system' component. The provider is defined by an object that includes an id, label, template, controller, and priority.

```javascript
  function PluginConfiguration(ViewsProvider) {
    ViewsProvider.registerDefaultView('admin.system', {
      id: 'system-settings-general',
      label: 'SYSTEM_GENERAL',
      template: template,
      controller: Controller,
      priority: 1000
    });
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/client/scripts/pages/system.js" line="74">

---

## Accessing a Specific System Setting

This section of the code demonstrates how to retrieve a specific system settings provider by its id. The id is retrieved from the route parameters and used to retrieve the corresponding provider from the ViewsProvider service.

```javascript
    var selectedProviderId = $routeParams.section;
    if (selectedProviderId) {
      $scope.activeSettingsProvier = Views.getProviders({
        component: 'admin.system',
        id: $routeParams.section
      })[0];
    }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
