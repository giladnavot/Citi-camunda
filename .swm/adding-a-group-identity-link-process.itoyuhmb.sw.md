---
title: Adding a Group Identity Link Process
---
This document will explain the process of adding a group identity link in the Camunda Platform. The steps include:

1. Adding an identity link
2. Inserting the identity link
3. Creating or updating authorizations by user ID and group ID
4. Creating or updating authorizations
5. Creating or updating an authorization
6. Creating an authorization
7. Updating authorization based on cache entries
8. Saving default authorizations
9. Updating the authorization

```mermaid
graph TD;
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/persistence/entity
  addGroupIdentityLink:::mainFlowStyle --> addIdentityLink
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/persistence/entity
  addIdentityLink:::mainFlowStyle --> insert
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/persistence/entity
  addIdentityLink:::mainFlowStyle --> fireAddIdentityLinkAuthorizationProvider
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/persistence/entity
  insert --> insertTask
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/persistence/entity
  insertTask --> insert
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/persistence/entity
  insertTask --> createDefaultAuthorizations
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/cfg/auth/DefaultAuthorizationProvider.java
  fireAddIdentityLinkAuthorizationProvider:::mainFlowStyle --> newTaskGroupIdentityLink
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/persistence/entity
  fireAddIdentityLinkAuthorizationProvider:::mainFlowStyle --> saveAuthorizations
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/cfg/auth/DefaultAuthorizationProvider.java
  fireAddIdentityLinkAuthorizationProvider:::mainFlowStyle --> newTaskUserIdentityLink
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/cfg/auth/DefaultAuthorizationProvider.java
  newTaskGroupIdentityLink --> createOrUpdateAuthorizationsByGroupId
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/persistence/AbstractManager.java
  saveAuthorizations --> saveDefaultAuthorizations
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/persistence/entity
  saveDefaultAuthorizations --> update
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/cfg/auth/DefaultAuthorizationProvider.java
  newTaskUserIdentityLink:::mainFlowStyle --> createOrUpdateAuthorizationsByUserId
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/cfg/auth/DefaultAuthorizationProvider.java
  createOrUpdateAuthorizationsByUserId:::mainFlowStyle --> createOrUpdateAuthorizations
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/cfg/auth/DefaultAuthorizationProvider.java
  createOrUpdateAuthorizations:::mainFlowStyle --> createOrUpdateAuthorization
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/cfg/auth/DefaultAuthorizationProvider.java
  createOrUpdateAuthorization:::mainFlowStyle --> createAuthorization
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/cfg/auth/DefaultAuthorizationProvider.java
  createAuthorization:::mainFlowStyle --> updateAuthorizationBasedOnCacheEntries
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/db/entitymanager
  updateAuthorizationBasedOnCacheEntries:::mainFlowStyle --> getCachedEntitiesByType
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/persistence/entity
  updateAuthorizationBasedOnCacheEntries:::mainFlowStyle --> getPermissions
end
subgraph engine/src/main/java/org/camunda/bpm/engine/impl/db/entitymanager
  getCachedEntitiesByType --> getEntitiesByType
end
  getPermissions:::mainFlowStyle --> ...

 classDef mainFlowStyle color:#000000,fill:#7CB9F4
  classDef rootsStyle color:#000000,fill:#00FFF4
```

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/persistence/entity/TaskEntity.java" line="726">

---

# Adding an identity link

The `addIdentityLink` function is used to add an identity link to a task. It ensures the task is active, creates a new identity link, inserts it, and then fires the `fireAddIdentityLinkAuthorizationProvider` function.

```java
  // task assignment //////////////////////////////////////////////////////////

  public IdentityLinkEntity addIdentityLink(String userId, String groupId, String type) {
    ensureTaskActive();

    IdentityLinkEntity identityLink = newIdentityLink(userId, groupId, type);
    identityLink.insert();
    getIdentityLinks().add(identityLink);

    fireAddIdentityLinkAuthorizationProvider(type, userId, groupId);
    return identityLink;
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/persistence/entity/TaskEntity.java" line="238">

---

# Inserting the identity link

The `insert` function is used to insert the task into the task manager.

```java
  public void insert() {
    CommandContext commandContext = Context.getCommandContext();
    TaskManager taskManager = commandContext.getTaskManager();
    taskManager.insertTask(this);
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/cfg/auth/DefaultAuthorizationProvider.java" line="220">

---

# Creating or updating authorizations by user ID and group ID

The `newTaskGroupIdentityLink` function is used to create or update authorizations by group ID. It ensures the group ID is valid and then calls the `createOrUpdateAuthorizationsByGroupId` function.

```java
  public AuthorizationEntity[] newTaskGroupIdentityLink(Task task, String groupId, String type) {

    ensureValidIndividualResourceId("Cannot grant default authorization for identity link to group " + groupId,
        groupId);

    // create (or update) an authorization for the given group
    // whenever a new user identity link will be added

    return createOrUpdateAuthorizationsByGroupId(task, groupId);
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/cfg/auth/DefaultAuthorizationProvider.java" line="261">

---

# Creating or updating authorizations

The `createOrUpdateAuthorizations` function is used to create or update authorizations. It checks if specific variable permission is enforced, gets runtime permissions, and then creates or updates the authorization.

```java
  /**
   * (1) Fetch existing runtime & history authorizations
   * (2) Update authorizations:
   *     (2a) fetched authorization == null
   *         ->  create a new runtime authorization (with READ, (UPDATE/TASK_WORK) permission,
   *             and READ_VARIABLE if enabled)
   *         ->  create a new history authorization (with READ on HISTORIC_TASK)
   *     (2b) fetched authorization != null
   *         ->  Add READ, (UPDATE/TASK_WORK) permission, and READ_VARIABLE if enabled
   *             UPDATE or TASK_WORK permission is configurable in camunda.cfg.xml and by default,
   *             UPDATE permission is provided
   *         ->  Add READ on HISTORIC_TASK
   */
  protected AuthorizationEntity[] createOrUpdateAuthorizations(Task task, String groupId,
                                                               String userId) {

    boolean enforceSpecificVariablePermission = isEnforceSpecificVariablePermission();

    Permission[] runtimeTaskPermissions = getRuntimePermissions(enforceSpecificVariablePermission);

    AuthorizationEntity runtimeAuthorization = createOrUpdateAuthorization(task, userId, groupId,
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/cfg/auth/DefaultAuthorizationProvider.java" line="298">

---

# Creating or updating an authorization

The `createOrUpdateAuthorization` function is used to create or update an authorization. It gets the grant authorization for the task, and if it doesn't exist, it creates a new one. If it does exist, it adds permissions to the existing authorization.

```java
  protected AuthorizationEntity createOrUpdateAuthorization(Task task, String userId,
                                                            String groupId, Resource resource,
                                                            boolean isHistoric,
                                                            Permission... permissions) {

    String taskId = task.getId();

    AuthorizationEntity authorization = getGrantAuthorization(taskId, userId, groupId, resource);

    if (authorization == null) {
      authorization = createAuthorization(userId, groupId, resource, taskId, permissions);

      if (isHistoric) {
        provideRemovalTime(authorization, task);
      }

    } else {
      addPermissions(authorization, permissions);

    }

```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/cfg/auth/DefaultAuthorizationProvider.java" line="425">

---

# Creating an authorization

The `createAuthorization` function is used to create an authorization. It creates a grant authorization and then updates the authorization based on cache entries.

```java
  protected AuthorizationEntity createAuthorization(String userId, String groupId,
                                                    Resource resource, String resourceId,
                                                    Permission... permissions) {
    AuthorizationEntity authorization =
        createGrantAuthorization(userId, groupId, resource, resourceId, permissions);

    updateAuthorizationBasedOnCacheEntries(authorization, userId, groupId, resource, resourceId);

    return authorization;
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/cfg/auth/DefaultAuthorizationProvider.java" line="479">

---

# Updating authorization based on cache entries

The `updateAuthorizationBasedOnCacheEntries` function is used to update an authorization based on cache entries. It checks if there is an authorization with the same rights in the cache, and if there is, it updates the given authorization with the permissions and removes the old one from the cache.

```java
  /**
   * Searches through the cache, if there is already an authorization with same rights. If that's the case
   * update the given authorization with the permissions and remove the old one from the cache.
   */
  protected void updateAuthorizationBasedOnCacheEntries(AuthorizationEntity authorization, String userId, String groupId,
                                                        Resource resource, String resourceId) {
    DbEntityManager dbManager = Context.getCommandContext().getDbEntityManager();
    List<AuthorizationEntity> list = dbManager.getCachedEntitiesByType(AuthorizationEntity.class);
    for (AuthorizationEntity authEntity : list) {
      boolean hasSameAuthRights = hasEntitySameAuthorizationRights(authEntity, userId, groupId, resource, resourceId);
      if (hasSameAuthRights) {
        int previousPermissions = authEntity.getPermissions();
        authorization.setPermissions(previousPermissions);
        dbManager.getDbEntityCache().remove(authEntity);
        return;
      }
    }
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/persistence/AbstractManager.java" line="295">

---

# Saving default authorizations

The `saveDefaultAuthorizations` function is used to save default authorizations. If there are authorizations, it runs without authorization and inserts or updates the authorizations in the authorization manager.

```java
  public void saveDefaultAuthorizations(final AuthorizationEntity[] authorizations) {
    if(authorizations != null && authorizations.length > 0) {
      Context.getCommandContext().runWithoutAuthorization(new Callable<Void>() {
        public Void call() {
          AuthorizationManager authorizationManager = getAuthorizationManager();
          for (AuthorizationEntity authorization : authorizations) {

            if(authorization.getId() == null) {
              authorizationManager.insert(authorization);
            } else {
              authorizationManager.update(authorization);
            }

          }
          return null;
        }
      });
    }
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/persistence/entity/AuthorizationManager.java" line="181">

---

# Updating the authorization

The `update` function is used to update an authorization. It checks the authorization and then merges it with the DB entity manager.

```java
  public void update(AuthorizationEntity authorization) {
    checkAuthorization(UPDATE, AUTHORIZATION, authorization.getId());
    getDbEntityManager().merge(authorization);
  }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="flows"><sup>Powered by [Swimm](/)</sup></SwmMeta>
