---
title: An Overview of Navigation Controllers
---
Navigation Controllers in Citi-camunda are responsible for managing the navigation and layout of the application. They handle user interactions and determine the visual state of the application, such as which sections of the application are visible or hidden. For instance, they can control the visibility of search functionality, the opening and closing of different regions of the application, and the maximization or resetting of these regions.

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/navigation/controllers/cam-layout-ctrl.js" line="24">

---

# Layout Controller

The Layout Controller in this file is responsible for managing the layout of the application. It defines functions such as `toggleRegion`, `maximizeRegion`, and `resetRegions` that manipulate the layout based on user actions.

```javascript
  '$scope',
  '$timeout',
  function($scope, $timeout) {
    $scope.toggleVariableSearch = function($event) {
      if ($event && $event.preventDefault) {
        $event.preventDefault();
      }

      $('.tasks-list').toggleClass('show-search');
    };

    function region($event) {
      return $($event.currentTarget).attr('data-region');
    }

    function isClosed(target) {
      return $bdy.hasClass(target + '-column-close');
    }

    function open(target) {
      return $bdy.removeClass(target + '-column-close');
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/navigation/controllers/cam-header-views-ctrl.js" line="20">

---

# Header Views Controller

The Header Views Controller in this file is responsible for managing the navigation bar of the application. It defines the `navbarVars` and `navbarActions` that are used to control the navigation bar.

```javascript
  '$scope',
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

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
