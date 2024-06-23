---
title: Exploring Group Management in Citi-camunda
---
Group Management in Citi-camunda refers to the functionality that allows the creation, editing, and organization of groups. This is achieved through the use of various scripts such as `groupCreate.js`, `groupEdit.js`, and `groups.js`. These scripts handle the creation of new groups, editing of existing groups, and the overall management of groups respectively. The `groupResource.js` file is used to manage the resources related to groups.

<SwmSnippet path="/webapps/frontend/ui/admin/client/scripts/pages/groupCreate.js" line="61">

---

## Creating a Group

The `createGroup` function is used to create a new group. It takes the group details from `$scope.group` and uses the `GroupResource.createGroup` method to create the group.

```javascript
    $scope.createGroup = function() {
      var group = $scope.group;
      GroupResource.createGroup(group).$promise.then(
        function() {
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/client/scripts/pages/groupEdit.js" line="265">

---

## Editing a Group

The group details can be edited using the `$scope.group.id`. The changes are reflected in the group with the corresponding id.

```javascript
              status: $translate.instant('NOTIFICATIONS_STATUS_SUCCESS'),
              message: $translate.instant('GROUP_EDIT_REMOVED_FROM_TENANT', {
                group: $scope.group.id
              })
            });
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/client/scripts/pages/groups.js" line="107">

---

## Group Navigation

The `breadcrumbsAdd` function is used to add navigation breadcrumbs for the groups page. The `href` property is used to set the URL for the groups page.

```javascript
    pageService.breadcrumbsAdd({
      label: $translate.instant('GROUPS_GROUP'),
      href: '#/groups'
    });
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
