---
title: Overview of Analytics
---
Analytics in the Citi-camunda repository refers to the collection and processing of telemetry data from the Camunda process engine. This data is used to understand the usage and performance of the process engine, which can help in identifying potential improvements and troubleshooting issues. The analytics functionality is implemented through the telemetry API, which can be configured to enable or disable data collection. The collected data is then processed and visualized in the analytics dashboard.

<SwmSnippet path="/webapps/frontend/ui/admin/client/scripts/pages/analytics.js" line="29">

---

# Telemetry Resource

The 'telemetry' resource of the Camunda API is used to interact with the telemetry feature. It is obtained using the 'resource' method of the 'camAPI' service.

```javascript
    var telemetryResource = camAPI.resource('telemetry');

```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/client/scripts/pages/analytics.js" line="31">

---

# Getting the Telemetry Configuration

The 'get' method of the 'telemetry' resource is used to get the current configuration of the telemetry feature. If there is an error in getting the configuration, an error notification is added. If the configuration is obtained successfully, the 'enableUsage' property of the 'form' object in the scope is set to the 'enableTelemetry' property of the obtained configuration.

```javascript
    telemetryResource.get(function(err, res) {
      if (err) {
        const msg = err.message;
        Notifications.addError({
          status: $translate.instant('ERROR'),
          message: $translate.instant(
            'TELEMETRY_FETCH_CONFIGURATION_ERROR_MESSAGE',
            {
              msg
            }
          )
        });
      } else {
        $scope.authorized = true;
        $scope.form.enableUsage = res.enableTelemetry;
      }
    });
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/client/scripts/pages/analytics.js" line="49">

---

# Changing the Telemetry Configuration

The 'submit' function is used to apply the changes made by the user to the telemetry configuration. The 'configure' method of the 'telemetry' resource is used to change the configuration. If there is no error in changing the configuration, a success notification is added.

```javascript
    $scope.submit = function() {
      telemetryResource.configure(!!$scope.form.enableUsage, function(err) {
        if (!err) {
          Notifications.addMessage({
            status: $translate.instant('TELEMETRY_SUCCESS_HEADING'),
            message: $translate.instant('TELEMETRY_SUCCESS')
          });
        }
      });
    };
```

---

</SwmSnippet>

# Analytics Functions

This section discusses the functions 'submit' and 'PluginConfiguration' found in the analytics.js file.

<SwmSnippet path="/webapps/frontend/ui/admin/client/scripts/pages/analytics.js" line="49">

---

## Submit Function

The 'submit' function is responsible for configuring telemetry settings. It makes a call to the 'configure' method of the 'telemetryResource' object, passing in the current form's 'enableUsage' value. If the configuration is successful, a success message is added to the notifications.

```javascript
    $scope.submit = function() {
      telemetryResource.configure(!!$scope.form.enableUsage, function(err) {
        if (!err) {
          Notifications.addMessage({
            status: $translate.instant('TELEMETRY_SUCCESS_HEADING'),
            message: $translate.instant('TELEMETRY_SUCCESS')
          });
        }
      });
    };
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/client/scripts/pages/analytics.js" line="64">

---

## PluginConfiguration Function

The 'PluginConfiguration' function registers a default view for the system admin. It uses the 'registerDefaultView' method of the 'ViewsProvider' object, passing in the view id, label, template, controller, and priority.

```javascript
  function PluginConfiguration(ViewsProvider) {
    ViewsProvider.registerDefaultView('admin.system', {
      id: 'analytics-settings-general',
      label: 'TELEMETRY_SETTINGS',
      template: template,
      controller: Controller,
      priority: 950
    });
  }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
