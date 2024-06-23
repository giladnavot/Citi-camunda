---
title: Overview of User Management
---
User Management in Citi-camunda refers to the functionality that allows administrators to handle user-related tasks. This includes creating, updating, and deleting users, as well as managing user groups. The user management functionality is implemented in the `users.js` and `groups.js` files, where the `ViewsProvider` registers default views for users and groups. These views are then controlled by the respective controllers, which interact with the Camunda API to perform the necessary operations.

<SwmSnippet path="/webapps/frontend/ui/admin/plugins/base/app/views/dashboard/users.js" line="24">

---

## User View Registration

Here, the 'user' view is registered with the ViewsProvider module. The 'id' property is set to 'user', and the 'label' property is set to 'USERS_USERS'. The 'template' property specifies the HTML template to be used for the view, and the 'pagePath' property specifies the URL path for the view.

```javascript
  function(ViewsProvider) {
    ViewsProvider.registerDefaultView('admin.dashboard.section', {
      id: 'user',
      label: 'USERS_USERS',
      template: template,
      pagePath: '#/users',
      controller: [
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/plugins/base/app/views/dashboard/users.js" line="30">

---

## User Controller

The 'controller' property specifies the logic for the 'user' view. It uses the camAPI to interact with the user resource. The 'access' property on the $scope object is used to manage user permissions.

```javascript
      controller: [
        '$scope',
        'camAPI',
        function($scope, camAPI) {
          var service = camAPI.resource('user');

          $scope.access = {};

          service.options(function(err, data) {
            if (err) {
              throw err;
            }
            $scope.access = {};

            for (var a in data.links) {
              $scope.access[data.links[a].rel] = true;
            }
          });
        }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
