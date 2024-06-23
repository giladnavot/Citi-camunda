---
title: Basic Concepts of User Management
---
User Management in Citi-camunda refers to the functionality that allows the creation, editing, and deletion of users. This is handled through various scripts in the `webapps/frontend/ui/admin/client/scripts/pages/` and `webapps/frontend/ui/admin/client/scripts/resources/` directories. The `userCreate.js`, `userEdit.js`, and `users.js` files are particularly important, containing functions and properties related to user profiles, credentials, and user-related notifications. Authentication is also a key aspect of user management, ensuring that certain operations are only accessible to authenticated users.

<SwmSnippet path="/webapps/frontend/ui/admin/client/scripts/resources/userResource.js" line="31">

---

## Creating Users

The `createUser` method is used to create a new user. It sends a POST request with the user details.

```javascript
        createUser: {method: 'POST', params: {userId: 'create'}},
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/client/scripts/pages/userCreate.js" line="37">

---

## User Navigation

The `label` and `href` properties are used to set up navigation for the user pages. The `label` is the display name of the navigation link, and the `href` is the URL of the page.

```javascript
      {
        label: $translate.instant('USERS_USERS'),
        href: '#/users/'
      },
      {
        label: $translate.instant('USERS_CREATE'),
        href: '#/users-create'
      }
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/client/scripts/pages/userCreate.js" line="99">

---

## User Authentication

The `authentication` property is used to ensure that only authenticated users can access the user creation page. It is set to 'required', meaning that unauthenticated users will be redirected to the login page.

```javascript
      authentication: 'required'
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/client/scripts/resources/userResource.js" line="33">

---

## Counting Users

The `count` method is used to get the total number of users. It sends a GET request and returns the count.

```javascript
        count: {method: 'GET', params: {userId: 'count'}}
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
