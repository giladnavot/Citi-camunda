---
title: Introduction to Groups in the Engine
---
In the Citi-camunda repository, 'Groups' refers to a Java interface located in the 'org.camunda.bpm.engine.authorization' package. This interface holds a set of built-in user identities for the Camunda Platform. It contains constants like 'CAMUNDA_ADMIN', 'GROUP_TYPE_SYSTEM', and 'GROUP_TYPE_WORKFLOW' which represent different types of user groups within the system. The 'Groups' interface is used throughout the codebase to manage user permissions and authorizations. For instance, it is used to check if a user is a member of a certain group before granting them specific permissions.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/authorization/Groups.java" line="19">

---

# 'Groups' Interface

This is the 'Groups' interface. It defines constants for built-in groups such as 'CAMUNDA_ADMIN', 'GROUP_TYPE_SYSTEM', and 'GROUP_TYPE_WORKFLOW'.

```java
/**
 * Holds the set of built-in user identities for Camunda Platform.
 *
 * @author Nico Rehwaldt
 */
public interface Groups {

  public static final String CAMUNDA_ADMIN = "camunda-admin";
  public static final String GROUP_TYPE_SYSTEM = "SYSTEM";
  public static final String GROUP_TYPE_WORKFLOW = "WORKFLOW";
  
}
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/ManagementService.java" line="27">

---

# Usage of 'Groups' in 'ManagementService'

Here, the 'Groups' interface is used in the 'ManagementService' class. The 'CAMUNDA_ADMIN' group is used to check if a user has administrative permissions.

```java
import org.camunda.bpm.engine.authorization.BatchPermissions;
import org.camunda.bpm.engine.authorization.Groups;
import org.camunda.bpm.engine.authorization.Permissions;
import org.camunda.bpm.engine.authorization.ProcessDefinitionPermissions;
import org.camunda.bpm.engine.authorization.ProcessInstancePermissions;
import org.camunda.bpm.engine.authorization.Resources;
import org.camunda.bpm.engine.batch.Batch;
import org.camunda.bpm.engine.batch.BatchQuery;
import org.camunda.bpm.engine.batch.BatchStatisticsQuery;
import org.camunda.bpm.engine.history.HistoricProcessInstanceQuery;
import org.camunda.bpm.engine.impl.jobexecutor.JobExecutor;
import org.camunda.bpm.engine.management.ActivityStatisticsQuery;
import org.camunda.bpm.engine.management.DeploymentStatisticsQuery;
import org.camunda.bpm.engine.management.JobDefinition;
import org.camunda.bpm.engine.management.JobDefinitionQuery;
import org.camunda.bpm.engine.management.MetricsQuery;
import org.camunda.bpm.engine.management.ProcessDefinitionStatisticsQuery;
import org.camunda.bpm.engine.management.SchemaLogQuery;
import org.camunda.bpm.engine.management.SetJobRetriesBuilder;
import org.camunda.bpm.engine.management.SetJobRetriesByJobsAsyncBuilder;
import org.camunda.bpm.engine.management.SetJobRetriesByProcessAsyncBuilder;
```

---

</SwmSnippet>

<SwmSnippet path="/examples/invoice/src/main/java/org/camunda/bpm/example/invoice/DemoDataGenerator.java" line="41">

---

# Usage of 'Groups' in 'DemoDataGenerator'

In the 'DemoDataGenerator' class, the 'Groups' interface is used to create a new group and assign permissions to it.

```java
import org.camunda.bpm.engine.authorization.Authorization;
import org.camunda.bpm.engine.authorization.Groups;
import org.camunda.bpm.engine.authorization.Permissions;
import org.camunda.bpm.engine.authorization.Resource;
import org.camunda.bpm.engine.authorization.Resources;
import org.camunda.bpm.engine.filter.Filter;
import org.camunda.bpm.engine.identity.Group;
import org.camunda.bpm.engine.identity.User;
import org.camunda.bpm.engine.impl.IdentityServiceImpl;
import org.camunda.bpm.engine.impl.persistence.entity.AuthorizationEntity;
import org.camunda.bpm.engine.task.TaskQuery;

/**
 * Creates demo credentials to be used in the invoice showcase.
 *
 * @author drobisch
 */
public class DemoDataGenerator {

    private final static Logger LOGGER = Logger.getLogger(DemoDataGenerator.class.getName());

```

---

</SwmSnippet>

# Groups and Authorization

Understanding Groups and Authorization

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/authorization/Groups.java" line="19">

---

## Groups Interface

The 'Groups' interface holds the set of built-in user identities for Camunda Platform. It defines constants for different types of groups, such as 'CAMUNDA_ADMIN', 'GROUP_TYPE_SYSTEM', and 'GROUP_TYPE_WORKFLOW'.

```java
/**
 * Holds the set of built-in user identities for Camunda Platform.
 *
 * @author Nico Rehwaldt
 */
public interface Groups {

  public static final String CAMUNDA_ADMIN = "camunda-admin";
  public static final String GROUP_TYPE_SYSTEM = "SYSTEM";
  public static final String GROUP_TYPE_WORKFLOW = "WORKFLOW";
  
}
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/authorization/Authorization.java" line="24">

---

## Authorization Interface

The 'Authorization' interface defines the way an identity is allowed to interact with a certain resource. It includes constants for different types of authorizations and permissions, and provides a detailed explanation of how authorizations work in Camunda Platform.

```java
/**
 * <p>An {@link Authorization} assigns a set of {@link Permission Permissions}
 * to an identity to interact with a given {@link Resource}.</p>
 * <p>EXAMPLES:
 * <ul>
 *   <li>User 'jonny' is authorized to start new instances of the 'invoice' process</li>
 *   <li>Group 'marketing' is not authorized to cancel process instances.</li>
 *   <li>Group 'marketing' is not allowed to use the tasklist application.</li>
 *   <li>Nobody is allowed to edit process variables in the cockpit application,
 *   except the distinct user 'admin'.</li>
 * </ul>
 *
 * <h2>Identities</h2>
 * <p>Camunda Platform distinguishes two types of identities: <em>users</em> and
 * <em>groups</em>. Authorizations can either range over all users
 * (userId = {@link #ANY}), an individual {@link User} or a {@link Group} of users.</p>
 *
 * <h2>Permissions</h2>
 * <p>A {@link Permission} defines the way an identity is allowed to interact
 * with a certain resource. Examples of permissions are {@link Permissions#CREATE CREATE},
 * {@link Permissions#READ READ}, {@link Permissions#UPDATE UPDATE},
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
