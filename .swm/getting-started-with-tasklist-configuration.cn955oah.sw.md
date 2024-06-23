---
title: Getting Started with Tasklist Configuration
---
Tasklist Config in Citi-camunda refers to the configuration settings for the tasklist module. This configuration is primarily defined in the `routes.js`, `date.js`, and `uris.js` files located in the `webapps/frontend/ui/tasklist/client/scripts/config/` directory. The `routes.js` file defines the routing for the tasklist, including the template to be used and the required authentication. The `date.js` file sets the date format for the tasklist. The `uris.js` file configures the URIs used within the tasklist, including the app root, app name, and various API endpoints.

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/config/routes.js" line="20">

---

## Configuring Routes

In `routes.js`, we define the routes for the tasklist module. For example, the root route (`/`) is associated with the `tasklistTemplate` and controlled by `camTasklistViewCtrl`. The `authentication` property is set to `required`, meaning the user must be authenticated to access this route.

```javascript
var tasklistTemplate = require('./../index.html?raw');

module.exports = [
  '$routeProvider',
  function($routeProvider) {
    $routeProvider
      .when('/', {
        template: tasklistTemplate,
        controller: 'camTasklistViewCtrl',
        authentication: 'required',
        reloadOnSearch: false
      })
      .otherwise({
        redirectTo: '/'
      });
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/config/date.js" line="18">

---

## Configuring Date Formats

In `date.js`, we configure the date formats for the tasklist module. The `camDateFormatProvider.setDateFormat` function is used to set the date format for different date properties.

```javascript
'use strict';
module.exports = [
  'camDateFormatProvider',
  'configurationProvider',
  function(camDateFormatProvider, configurationProvider) {
    var dateProperties = [
      'monthName',
      'day',
      'abbr',
      'normal',
      'long',
      'short'
    ];
    for (var i = 0; i < dateProperties.length; i++) {
      camDateFormatProvider.setDateFormat(
        configurationProvider.getDateFormat(dateProperties[i]),
        dateProperties[i]
      );
    }
  }
];
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/config/uris.js" line="18">

---

## Configuring URIs

In `uris.js`, we configure the URIs for the tasklist module. The `UriProvider.replace` function is used to replace placeholders in the URIs with actual values from the config.

```javascript
'use strict';

module.exports = function(ngModule, config) {
  ngModule.config([
    'UriProvider',
    function(UriProvider) {
      UriProvider.replace(':appRoot', config['app-root']);
      UriProvider.replace(':appName', 'tasklist');
      UriProvider.replace('app://', config.href);
      UriProvider.replace('adminbase://', config['app-root'] + '/app/admin/');
      UriProvider.replace(
        'tasklistbase://',
        config['app-root'] + '/app/tasklist/'
      );
      UriProvider.replace(
        'cockpitbase://',
        config['app-root'] + '/app/cockpit/'
      );
      UriProvider.replace('admin://', config['admin-api']);
      UriProvider.replace('plugin://', config['tasklist-api'] + 'plugin/');
      UriProvider.replace('engine://', config['engine-api']);
```

---

</SwmSnippet>

# Tasklist Config Functions

This section will focus on the functions and configurations found in routes.js, date.js, and uris.js.

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/config/routes.js" line="25">

---

## Routes Configuration

The routes.js file contains the configuration for the routes in the Tasklist. The `template` property specifies the template to be used for the route, while the `controller` property specifies the controller to be used. The `authentication` property indicates that authentication is required for this route.

```javascript
    $routeProvider
      .when('/', {
        template: tasklistTemplate,
        controller: 'camTasklistViewCtrl',
        authentication: 'required',
        reloadOnSearch: false
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/config/date.js" line="18">

---

## Date Configuration

The date.js file contains the configuration for the date format in the Tasklist. The `camDateFormatProvider.setDateFormat` function is used to set the date format based on the configuration provided.

```javascript
'use strict';
module.exports = [
  'camDateFormatProvider',
  'configurationProvider',
  function(camDateFormatProvider, configurationProvider) {
    var dateProperties = [
      'monthName',
      'day',
      'abbr',
      'normal',
      'long',
      'short'
    ];
    for (var i = 0; i < dateProperties.length; i++) {
      camDateFormatProvider.setDateFormat(
        configurationProvider.getDateFormat(dateProperties[i]),
        dateProperties[i]
      );
    }
  }
];
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/config/uris.js" line="18">

---

## URIs Configuration

The uris.js file contains the configuration for the URIs used in the Tasklist. The `UriProvider.replace` function is used to replace placeholders in the URIs with the actual values from the configuration.

```javascript
'use strict';

module.exports = function(ngModule, config) {
  ngModule.config([
    'UriProvider',
    function(UriProvider) {
      UriProvider.replace(':appRoot', config['app-root']);
      UriProvider.replace(':appName', 'tasklist');
      UriProvider.replace('app://', config.href);
      UriProvider.replace('adminbase://', config['app-root'] + '/app/admin/');
      UriProvider.replace(
        'tasklistbase://',
        config['app-root'] + '/app/tasklist/'
      );
      UriProvider.replace(
        'cockpitbase://',
        config['app-root'] + '/app/cockpit/'
      );
      UriProvider.replace('admin://', config['admin-api']);
      UriProvider.replace('plugin://', config['tasklist-api'] + 'plugin/');
      UriProvider.replace('engine://', config['engine-api']);
```

---

</SwmSnippet>

# Tasklist Configuration Endpoints

Tasklist Configuration Endpoints

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/config/uris.js" line="24">

---

## UriProvider.replace

The `UriProvider.replace` function is used to define several endpoints within the Tasklist application. It takes two arguments: a key and a value. The key is a placeholder that will be replaced with the value in the application's URIs. For example, `:appRoot` is replaced with the application's root URL, and `:appName` is replaced with 'tasklist'.

```javascript
      UriProvider.replace(':appRoot', config['app-root']);
      UriProvider.replace(':appName', 'tasklist');
      UriProvider.replace('app://', config.href);
      UriProvider.replace('adminbase://', config['app-root'] + '/app/admin/');
      UriProvider.replace(
        'tasklistbase://',
        config['app-root'] + '/app/tasklist/'
      );
      UriProvider.replace(
        'cockpitbase://',
        config['app-root'] + '/app/cockpit/'
      );
      UriProvider.replace('admin://', config['admin-api']);
      UriProvider.replace('plugin://', config['tasklist-api'] + 'plugin/');
      UriProvider.replace('engine://', config['engine-api']);

      UriProvider.replace(':engine', [
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/config/routes.js" line="25">

---

## $routeProvider.when

The `$routeProvider.when` function is used to define a route within the Tasklist application. In this case, it defines the root route ('/'). When this route is accessed, the Tasklist application's main view is displayed, controlled by the 'camTasklistViewCtrl' controller. Authentication is required to access this route.

```javascript
    $routeProvider
      .when('/', {
        template: tasklistTemplate,
        controller: 'camTasklistViewCtrl',
        authentication: 'required',
        reloadOnSearch: false
      })
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
