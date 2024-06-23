---
title: 'Understanding AuthorizationResource Implementation and Usage '
---
This document will cover the implementation and usage of the AuthorizationResource across the application. We'll cover:

1. The definition of AuthorizationResource
2. How AuthorizationResource is used in the application
3. The role of AuthorizationService in managing access permissions
4. The creation of users and groups for authorization.

<SwmSnippet path="/engine-rest/engine-rest/src/main/java/org/camunda/bpm/engine/rest/sub/authorization/AuthorizationResource.java" line="27">

---

# Definition of AuthorizationResource

The `AuthorizationResource` interface defines the structure for managing authorizations. It includes methods for getting, deleting, and updating authorizations, as well as checking available operations.

```java
/**
 * @author Daniel Meyer
 *
 */
public interface AuthorizationResource {

  @GET
  @Produces(MediaType.APPLICATION_JSON)
  public AuthorizationDto getAuthorization(@Context UriInfo context);

  @DELETE
  @Produces(MediaType.APPLICATION_JSON)
  public void deleteAuthorization();

  @PUT
  @Consumes(MediaType.APPLICATION_JSON)
  public void updateAuthorization(AuthorizationDto Authorization);
  
  @OPTIONS
  @Produces(MediaType.APPLICATION_JSON)
  ResourceOptionsDto availableOperations(@Context UriInfo context);
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest/src/main/java/org/camunda/bpm/engine/rest/sub/authorization/impl/AuthorizationResourceImpl.java" line="43">

---

# Usage of AuthorizationResource

`AuthorizationResource` is implemented in `AuthorizationResourceImpl` class, extending the `AbstractAuthorizedRestResource` and implementing the `AuthorizationResource` interface.

```java
public class AuthorizationResourceImpl extends AbstractAuthorizedRestResource implements AuthorizationResource {
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/AuthorizationService.java" line="29">

---

# Role of AuthorizationService

The `AuthorizationService` interface allows managing `Authorization` objects. It provides methods for creating, saving, and querying authorizations. It is used to manage access permissions for users and groups.

```java
/**
 * <p>The authorization service allows managing {@link Authorization Authorizations}.</p>
 * 
 * <h2>Creating an authorization</h2>
 * <p>An authorization is created between a user/group and a resource. It describes 
 * the user/group's <em>permissions</em> to access that resource. An authorization may 
 * express different permissions, such as the permission to READ, UPDATE, DELETE the 
 * resource. (See {@link Authorization} for details).</p>
 * 
 * <h2>Granting / revoking permissions</h2>
 * <p>In order to grant the permission to access a certain resource, an authorization 
 * object is created:
 * <pre>
 * Authorization auth = authorizationService.createNewAuthorization();
 * //... configure auth
 * authorizationService.saveAuthorization(auth);
 * </pre>
 * The authorization object can be configured either for a user or a group:
 * <pre>
 * auth.setUserId("john");
 *   -OR-
```

---

</SwmSnippet>

<SwmSnippet path="/examples/invoice/src/main/java/org/camunda/bpm/example/invoice/DemoDataGenerator.java" line="62">

---

# Creation of Users and Groups for Authorization

The `createUsers` method is used to create demo users and groups for the invoice example. It checks if the identity service is read-only and if the user already exists before creating a new user and saving it. It also creates groups like 'sales', 'accounting', and 'management' and saves them.

```java
    public void createUsers(ProcessEngine engine) {

      final IdentityServiceImpl identityService = (IdentityServiceImpl) engine.getIdentityService();

      if(identityService.isReadOnly()) {
        LOGGER.info("Identity service provider is Read Only, not creating any demo users.");
        return;
      }

      User singleResult = identityService.createUserQuery().userId("demo").singleResult();
      if (singleResult != null) {
        return;
      }

      LOGGER.info("Generating demo data for invoice showcase");

      User user = identityService.newUser("demo");
      user.setFirstName("Demo");
      user.setLastName("Demo");
      user.setPassword("demo");
      user.setEmail("demo@camunda.org");
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="follow-up"><sup>Powered by [Swimm](/)</sup></SwmMeta>
