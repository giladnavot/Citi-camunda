---
title: Understanding the Welcome Module
---
In the Citi-camunda project, 'Welcome' refers to a module that is part of the frontend user interface. It is responsible for rendering the welcome page of the application. This module is implemented using AngularJS and it includes several components such as a controller, a template, and a style sheet.

The 'welcome' module is defined in the 'main.js' file. It is then used in the 'welcome.js' file to create two types of components: 'welcome.profile' and 'welcome.dashboard'. These components are used to display user profile information and dashboard data respectively on the welcome page.

The 'welcome' module also includes a route provider that defines the '/welcome' route. When this route is accessed, the welcome page is displayed. The welcome page requires user authentication, as indicated by the 'authentication: required' property.

The appearance of the welcome page is defined in the 'welcome.less' file. This file includes styles for different elements on the page, such as the app label wrapper and the app name.

The 'welcome-page.js' file is a controller that is part of the 'welcome' module. It retrieves the application vendor and name from the configuration and makes them available to the view.

The 'welcome.html' file is the template for the welcome page. It uses AngularJS directives and expressions to dynamically generate the content of the page based on the data provided by the controller.

<SwmSnippet path="/webapps/frontend/ui/welcome/client/scripts/pages/main.js" line="19">

---

# Welcome Module Definition

Here, the 'welcome' module is defined as an AngularJS module. It is named 'cam.welcome.pages' and does not have any dependencies.

```javascript
/* jshint browserify: true */
var angular = require('camunda-commons-ui/vendor/angular'),
  welcome = require('./welcome');

var pagesModule = angular.module('cam.welcome.pages', []);
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/welcome/client/scripts/pages/welcome.js" line="23">

---

# Welcome Page Route Definition

This is where the route for the welcome page is defined. When the '/welcome' route is accessed, the welcome page template is loaded and the associated controller is invoked.

```javascript
  '$routeProvider',
  function($routeProvider) {
    $routeProvider.when('/welcome', {
      template: template,
      // controller: Controller,
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/welcome/client/scripts/pages/welcome.js" line="43">

---

# Welcome Page Components

The welcome page consists of several components, including a profile section and a dashboard. These components are loaded dynamically using the 'Views.getProviders' function.

```javascript
          $scope.profilePlugins = Views.getProviders({
            component: 'welcome.profile'
          });

          $scope.plugins = Views.getProviders({
            component: 'welcome.dashboard'
          });
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/welcome/client/scripts/pages/welcome.js" line="54">

---

# Welcome Page Authentication

Authentication is required to access the welcome page. This is specified by the 'authentication' property in the route definition.

```javascript
      authentication: 'required',
      reloadOnSearch: false
    });
```

---

</SwmSnippet>

# Welcome Page Functions

This section will cover the main functions related to the 'Welcome' page in the Citi-camunda project. We will look at how the page is set up, how user data is handled, and how the page interacts with other parts of the application.

<SwmSnippet path="/webapps/frontend/ui/welcome/client/scripts/pages/welcome.js" line="18">

---

## Welcome Page Setup

The 'welcome.js' file sets up the 'Welcome' page. It defines the template to be used for the page and configures the route to the page. It also sets up the controller for the page, which handles user interaction and data display.

```javascript
'use strict';

var template = require('./welcome.html?raw');

var RouteConfig = [
  '$routeProvider',
  function($routeProvider) {
    $routeProvider.when('/welcome', {
      template: template,
      // controller: Controller,
      controller: [
        '$scope',
        'Views',
        'Uri',
        function($scope, Views, Uri) {
          var auth = $scope.$root.authentication;

          $scope.canAccessApp = function(appName) {
            return auth.authorizedApps.indexOf(appName) > -1;
          };

```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/welcome/client/scripts/directives/user-profile.js" line="18">

---

## User Profile Handling

The 'user-profile.js' file handles the user profile section of the 'Welcome' page. It defines a directive that sets up the user profile form and handles user interaction with the form. It also communicates with the server to retrieve and update user profile data.

```javascript
'use strict';

var template = require('./user-profile.html?raw');
var angular = require('camunda-commons-ui/vendor/angular');

module.exports = [
  'camAPI',
  'Notifications',
  '$translate',
  function(camAPI, Notifications, $translate) {
    return {
      restrict: 'A',

      template: template,

      scope: {
        username: '='
      },

      replace: true,

```

---

</SwmSnippet>

# Welcome Page

Welcome Page Configuration

<SwmSnippet path="/webapps/frontend/ui/welcome/client/scripts/pages/welcome.js" line="25">

---

## Welcome Page Route

This section of the code defines the '/welcome' route in the AngularJS routing configuration. When the user navigates to '/welcome', the welcome page is displayed. The route configuration includes the HTML template to use for the page, the controller to handle the page's logic, and other settings such as whether authentication is required to access the page (it is) and whether the page should reload when the URL's query parameters change (it shouldn't).

```javascript
    $routeProvider.when('/welcome', {
      template: template,
      // controller: Controller,
      controller: [
        '$scope',
        'Views',
        'Uri',
        function($scope, Views, Uri) {
          var auth = $scope.$root.authentication;

          $scope.canAccessApp = function(appName) {
            return auth.authorizedApps.indexOf(appName) > -1;
          };

          $scope.columnWidth = function() {
            return 12 / (auth.authorizedApps.length - 1);
          };

          $scope.profilePlugins = Views.getProviders({
            component: 'welcome.profile'
          });
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/welcome/client/scripts/camunda-welcome-ui.js" line="45">

---

## Welcome Page Initialization

This section of the code initializes the 'welcome' module, including its AngularJS dependencies, services, and plugins. It also sets up the application's URL configuration using the 'UriProvider' service, including the base URL for the 'welcome' API.

```javascript
export function init(pluginDependencies) {
  var ngDependencies = [
    'ng',
    'ngResource',
    'pascalprecht.translate',
    commons.name,
    pagesModule.name,
    directivesModule.name,
    servicesModule.name,
    pluginsModule.name
  ].concat(
    pluginDependencies.map(function(el) {
      return el.ngModuleName;
    })
  );

  var appNgModule = angular.module(APP_NAME, ngDependencies);

  function getUri(id) {
    var uri = $('base').attr(id);
    if (!id) {
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
