---
title: Basic Concepts of Tenant Management
---
Tenant Management in Citi-camunda refers to the functionality that allows the creation, modification, and management of tenants. A tenant, represented by the 'tenant' property, is an entity that can be used to segregate processes, cases, and tasks from each other. This is particularly useful in multi-tenant applications where data and processes need to be isolated from each other. The 'tenant' property is used in various scripts such as 'tenantCreate.js', 'tenants.js', and 'tenantEdit.js' to manage tenant data.

<SwmSnippet path="/webapps/frontend/ui/admin/client/scripts/pages/tenantCreate.js" line="50">

---

## Creating a Tenant

Here we see the creation of a new tenant object with an ID and name. This object is then used to create a new tenant in the system.

```javascript
    $scope.tenant = {
      id: '',
      name: ''
    };
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/client/scripts/pages/tenants.js" line="127">

---

## Managing Tenants

This code snippet shows the route configuration for the tenants page, which is used to manage existing tenants. The controller associated with this route handles the logic for fetching and displaying tenant data.

```javascript
    $routeProvider.when('/tenants', {
      template: template,
      controller: Controller,
      authentication: 'required',
      reloadOnSearch: false
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/client/scripts/pages/tenantEdit.js" line="59">

---

## Editing a Tenant

This code snippet shows the breadcrumbs being set for the tenant editing page. This page allows for the modification of existing tenant details.

```javascript
      pageService.breadcrumbsAdd([
        {
          label: $translate.instant('TENANTS_TENANTS'),
          href: '#/tenants'
        }
      ]);
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
