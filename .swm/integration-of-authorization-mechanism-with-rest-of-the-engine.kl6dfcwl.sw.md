---
title: Integration of Authorization Mechanism with Rest of the Engine
---
This document will cover the integration of the authorization mechanism with other parts of the Camunda engine. We'll cover:

1. How the authorization mechanism is enabled and configured
2. How authorization is created and updated
3. How authorization exceptions are handled

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/ProcessEngineConfiguration.java" line="820">

---

# Enabling and Configuring Authorization

The `ProcessEngineConfiguration` class contains methods to enable and configure the authorization mechanism. The `isAuthorizationEnabled` method checks if authorization is enabled, while the `setAuthorizationEnabled` method enables or disables authorization.

```java
  public boolean isAuthorizationEnabled() {
    return authorizationEnabled;
  }

  public ProcessEngineConfiguration setAuthorizationEnabled(boolean isAuthorizationChecksEnabled) {
    this.authorizationEnabled = isAuthorizationChecksEnabled;
    return this;
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest/src/main/java/org/camunda/bpm/engine/rest/dto/authorization/AuthorizationDto.java" line="45">

---

# Creating and Updating Authorization

The `AuthorizationDto` class contains the `fromAuthorization` method which transforms a database authorization object into a DTO. It sets the id, type, permissions, userId, groupId, resourceType, and resourceId of the DTO from the database authorization object.

```java
  // transformers ///////////////////////////////////////

  public static AuthorizationDto fromAuthorization(Authorization dbAuthorization, ProcessEngineConfiguration engineConfiguration) {
    AuthorizationDto authorizationDto = new AuthorizationDto();

    authorizationDto.setId(dbAuthorization.getId());
    authorizationDto.setType(dbAuthorization.getAuthorizationType());

    Permission[] dbPermissions = getPermissions(dbAuthorization, engineConfiguration);
    authorizationDto.setPermissions(PermissionConverter.getNamesForPermissions(dbAuthorization, dbPermissions));

    authorizationDto.setUserId(dbAuthorization.getUserId());
    authorizationDto.setGroupId(dbAuthorization.getGroupId());
    authorizationDto.setResourceType(dbAuthorization.getResourceType());
    authorizationDto.setResourceId(dbAuthorization.getResourceId());
    authorizationDto.setRemovalTime(dbAuthorization.getRemovalTime());
    authorizationDto.setRootProcessInstanceId(dbAuthorization.getRootProcessInstanceId());

    return authorizationDto;
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest/src/main/java/org/camunda/bpm/engine/rest/dto/authorization/AuthorizationDto.java" line="66">

---

The `update` method in the `AuthorizationDto` class is used to update an existing authorization. It sets the groupId, userId, resourceId, resourceType, and permissions of the database authorization object from the DTO.

```java
  public static void update(AuthorizationDto dto, Authorization dbAuthorization, ProcessEngineConfiguration engineConfiguration) {

    dbAuthorization.setGroupId(dto.getGroupId());
    dbAuthorization.setUserId(dto.getUserId());
    dbAuthorization.setResourceId(dto.getResourceId());

    // update optional fields

    if(dto.getResourceType() != null) {
      dbAuthorization.setResourceType(dto.getResourceType());
    }

    if(dto.getPermissions() != null) {
      dbAuthorization.setPermissions(PermissionConverter.getPermissionsForNames(dto.getPermissions(), dto.getResourceType(), engineConfiguration));
    }

  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest/src/main/java/org/camunda/bpm/engine/rest/dto/AuthorizationExceptionDto.java" line="43">

---

# Handling Authorization Exceptions

The `AuthorizationExceptionDto` class handles authorization exceptions. The `fromException` method transforms an `AuthorizationException` into a DTO. It sets the message, type, userId, missingAuthorizations, permissionName, resourceId, and resourceName of the DTO from the exception.

```java
  public static AuthorizationExceptionDto fromException(AuthorizationException e) {
    AuthorizationExceptionDto dto = new AuthorizationExceptionDto();
    
    dto.setMessage(e.getMessage());
    dto.setType(AuthorizationException.class.getSimpleName());
    
    dto.setUserId(e.getUserId());
    dto.setMissingAuthorizations(MissingAuthorizationDto.fromInfo(e.getMissingAuthorizations()));
    dto.setPermissionName(e.getViolatedPermissionName());
    dto.setResourceId(e.getResourceId());
    dto.setResourceName(e.getResourceType());
    
    return dto;
  }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="follow-up"><sup>Powered by [Swimm](/)</sup></SwmMeta>
