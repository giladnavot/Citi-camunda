---
title: Understanding Tasklist Navigation
---
Tasklist Navigation refers to the functionality that allows users to navigate through different views in the tasklist application. It is implemented using AngularJS, a popular JavaScript framework for building web applications. The navigation functionality is primarily handled by two controllers: `camLayoutCtrl` and `camHeaderViewsCtrl`. The `camLayoutCtrl` controller manages the layout of the tasklist application, while the `camHeaderViewsCtrl` controller manages the actions available in the navigation bar of the tasklist application.

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/navigation/index.js" line="26">

---

# Tasklist Navigation Module

This is where the Tasklist Navigation module is defined. It requires AngularJS and two controllers: `camLayoutCtrl` and `camHeaderViewsCtrl`. The module is then exported for use in other parts of the application.

```javascript
var navigationModule = angular.module('cam.tasklist.navigation', [
  require('camunda-commons-ui/lib/util/index').name,
  'ui.bootstrap'
]);

navigationModule.controller('camHeaderViewsCtrl', camHeaderViewsCtrl);
navigationModule.controller('camLayoutCtrl', camLayoutCtrl);

module.exports = navigationModule;
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/navigation/controllers/cam-header-views-ctrl.js" line="21">

---

# Navigation Controllers

This is an example of how a navigation controller is used. In this case, the `camHeaderViewsCtrl` controller is used to manage the navbar actions and variables. It uses the `Views` service to get the providers for the `tasklist.navbar.action` component.

```javascript
  'Views',
  function($scope, Views) {
    $scope.navbarVars = {read: ['tasklistApp']};
    $scope.navbarActions = Views.getProviders({
      component: 'tasklist.navbar.action'
```

---

</SwmSnippet>

# Tasklist Navigation Functions

Let's look at the functions in `cam-header-views-ctrl.js` and `cam-layout-ctrl.js`.

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/navigation/controllers/cam-header-views-ctrl.js" line="21">

---

## cam-header-views-ctrl.js

In `cam-header-views-ctrl.js`, the `$scope.navbarVars` and `$scope.navbarActions` are defined. `$scope.navbarVars` is used to read the tasklist app, and `$scope.navbarActions` is used to get the providers for the tasklist navbar action.

```javascript
  'Views',
  function($scope, Views) {
    $scope.navbarVars = {read: ['tasklistApp']};
    $scope.navbarActions = Views.getProviders({
      component: 'tasklist.navbar.action'
    });
  }
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/navigation/controllers/cam-layout-ctrl.js" line="1">

---

## cam-layout-ctrl.js

In `cam-layout-ctrl.js`, the `cam.tasklist.navigation` module is defined, which includes the controllers for the header views and layout of the tasklist.

```javascript
/*
 * Copyright Camunda Services GmbH and/or licensed to Camunda Services GmbH
 * under one or more contributor license agreements. See the NOTICE file
 * distributed with this work for additional information regarding copyright
 * ownership. Camunda licenses this file to you under the Apache License,
 * Version 2.0; you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *     http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */

'use strict';

var $ = require('jquery');
var $bdy = $('body');
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
