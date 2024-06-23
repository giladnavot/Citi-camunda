---
title: Understanding Authorizations
---
Authorizations in Citi-camunda refer to the permissions given to users or groups to perform certain actions. It is a security measure to ensure that only authorized users have access to specific resources or operations. The authorization process checks the user's permissions before granting access to the requested resource. For instance, in the provided code, the 'AuthorizationResource' checks if the user has 'ALL' permissions for the 'authorization' resource.

<SwmSnippet path="/webapps/frontend/ui/admin/plugins/base/app/views/dashboard/authorizations.js" line="20">

---

# Authorization Definition

This is where the authorization is defined. The 'id' property is set to 'authorization', and the 'access' property is an array that includes 'AuthorizationResource' and a function that checks if the user has the required permissions.

```javascript
var template = require('./authorizations.html?raw');

module.exports = [
  'ViewsProvider',
  function(ViewsProvider) {
    ViewsProvider.registerDefaultView('admin.dashboard.section', {
      id: 'authorization',
      label: 'AUTHORIZATION_AUTHORIZATIONS',
      template: template,
      pagePath: '#/authorization',
      controller: [function() {}],
      access: [
        'AuthorizationResource',
        function(AuthorizationResource) {
          return function(cb) {
            AuthorizationResource.check({
              permissionName: 'ALL',
              resourceName: 'authorization',
              resourceType: 4
            })
              .$promise.then(function(response) {
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/plugins/base/app/views/dashboard/authorizations.js" line="34">

---

# Authorization Check

This is where the authorization check is performed. The 'AuthorizationResource.check' function is called with the 'permissionName', 'resourceName', and 'resourceType' parameters. The function returns a promise that resolves to a response indicating whether the user is authorized or not.

```javascript
          return function(cb) {
            AuthorizationResource.check({
              permissionName: 'ALL',
              resourceName: 'authorization',
              resourceType: 4
            })
              .$promise.then(function(response) {
                cb(null, response.authorized);
              })
              .catch(cb);
          };
```

---

</SwmSnippet>

# Authorization Functionality

The 'registerDefaultView' function is used to register a default view in the admin dashboard. It has several properties that define the behavior and appearance of the view.

<SwmSnippet path="/webapps/frontend/ui/admin/plugins/base/app/views/dashboard/authorizations.js" line="25">

---

## registerDefaultView Function

The 'registerDefaultView' function is used to register a default view in the admin dashboard. It takes two parameters: the section id and an object that defines the properties of the view.

```javascript
    ViewsProvider.registerDefaultView('admin.dashboard.section', {
      id: 'authorization',
      label: 'AUTHORIZATION_AUTHORIZATIONS',
      template: template,
      pagePath: '#/authorization',
      controller: [function() {}],
      access: [
        'AuthorizationResource',
        function(AuthorizationResource) {
          return function(cb) {
            AuthorizationResource.check({
              permissionName: 'ALL',
              resourceName: 'authorization',
              resourceType: 4
            })
              .$promise.then(function(response) {
                cb(null, response.authorized);
              })
              .catch(cb);
          };
        }
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/plugins/base/app/views/dashboard/authorizations.js" line="26">

---

### id Property

The 'id' property is used to uniquely identify the view. In this case, the id is 'authorization'.

```javascript
      id: 'authorization',
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/plugins/base/app/views/dashboard/authorizations.js" line="27">

---

### label Property

The 'label' property is used to define the label of the view. In this case, the label is 'AUTHORIZATION_AUTHORIZATIONS'.

```javascript
      label: 'AUTHORIZATION_AUTHORIZATIONS',
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/plugins/base/app/views/dashboard/authorizations.js" line="28">

---

### template Property

The 'template' property is used to define the template of the view. In this case, the template is defined in the 'authorizations.html' file.

```javascript
      template: template,
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/plugins/base/app/views/dashboard/authorizations.js" line="29">

---

### pagePath Property

The 'pagePath' property is used to define the path of the view. In this case, the path is '#/authorization'.

```javascript
      pagePath: '#/authorization',
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/plugins/base/app/views/dashboard/authorizations.js" line="30">

---

### controller Property

The 'controller' property is used to define the controller of the view. In this case, an empty function is used as the controller.

```javascript
      controller: [function() {}],
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/plugins/base/app/views/dashboard/authorizations.js" line="31">

---

### access Property

The 'access' property is used to define the access control of the view. It uses the 'AuthorizationResource' to check if the user has 'ALL' permissions for the 'authorization' resource.

```javascript
      access: [
        'AuthorizationResource',
        function(AuthorizationResource) {
          return function(cb) {
            AuthorizationResource.check({
              permissionName: 'ALL',
              resourceName: 'authorization',
              resourceType: 4
            })
              .$promise.then(function(response) {
                cb(null, response.authorized);
              })
              .catch(cb);
          };
        }
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/plugins/base/app/views/dashboard/authorizations.js" line="47">

---

### priority Property

The 'priority' property is used to define the priority of the view. In this case, the priority is 0.

```javascript
      priority: 0
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
