---
title: Performance Implications of Frequent Permission Checks
---
This document will cover the performance implications of checking permissions frequently in the Citi-camunda repository. We'll cover:

1. How permissions are checked
2. The impact of frequent permission checks on performance
3. How to mitigate performance issues.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/db/AuthorizationCheck.java" line="31">

---

# How permissions are checked

The `AuthorizationCheck` class is responsible for checking permissions. It has several properties that control the behavior of the check, such as `isAuthorizationCheckEnabled` which determines if the check is enabled, and `shouldPerformAuthorizatioCheck` which determines if the check should be performed. The `isRevokeAuthorizationCheckEnabled` property indicates if the revoke authorization checks are enabled or not. The comment on line 49 indicates that authorization checks without checking revoke permissions are much faster, implying a performance implication.

```java
public class AuthorizationCheck implements Serializable {

  private static final long serialVersionUID = 1L;

  /**
   * If true authorization check is enabled. for This switch is
   * useful when implementing a query which may perform an authorization check
   * only under certain circumstances.
   */
  protected boolean isAuthorizationCheckEnabled = false;

  /**
   * If true authorization check is performed.
   */
  protected boolean shouldPerformAuthorizatioCheck = false;

  /**
   * Indicates if the revoke authorization checks are enabled or not.
   * The authorization checks without checking revoke permissions are much more faster.
   */
  protected boolean isRevokeAuthorizationCheckEnabled = false;
```

---

</SwmSnippet>

# The impact of frequent permission checks on performance

Frequent permission checks can have a significant impact on performance. Each check involves a query to the database to retrieve the relevant permissions for the user or group. If these checks are performed frequently, for example, in a loop or for every request, it can lead to a large number of database queries, which can slow down the application. This is especially true if the checks involve revoke permissions, as indicated by the comment on line 49 of the `AuthorizationCheck` class.

# How to mitigate performance issues

To mitigate the performance issues associated with frequent permission checks, it's important to use them judiciously. For example, you can cache the results of permission checks to avoid querying the database every time. You can also consider disabling the revoke authorization checks if they're not necessary, as they can slow down the process significantly.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="follow-up"><sup>Powered by [Swimm](/)</sup></SwmMeta>
