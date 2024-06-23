---
title: Getting Started with Case Definitions
---
A Case Definition in the Citi-camunda repository refers to a specific type of process in the Camunda BPMN platform. It is an interface that extends the ResourceDefinition interface. The CaseDefinition interface is used throughout the codebase to handle and manage specific instances of processes, often in conjunction with other components such as the RepositoryService and the ProcessApplicationManager. It is also used in queries to filter or sort case definitions based on various parameters like id, key, category, and version.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/CaseDefinition.java" line="23">

---

# CaseDefinition Interface

The CaseDefinition interface is the main entry point for interacting with case definitions. It extends the ResourceDefinition interface, which provides common functionality for all resource definitions.

```java
public interface CaseDefinition extends ResourceDefinition {

}
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/RepositoryService.java" line="705">

---

# CaseDefinition Usage

The CaseDefinition interface is used in the RepositoryService class to get a case definition by its ID. This is a common operation when working with case definitions.

```java
  CaseDefinition getCaseDefinition(String caseDefinitionId);

  /**
   * Gives access to a deployed case model, e.g., a CMMN 1.0 XML file,
   * through a stream of bytes.
   *
   * @param caseDefinitionId
   *          id of a {@link CaseDefinition}, cannot be null.
   *
   * @throws NotValidException when the given case definition id or deployment id or resource name is null
   * @throws NotFoundException when no case definition or deployment resource is found for the given case definition id
   * @throws ProcessEngineException when an internal exception happens during the execution of the command
   */
  InputStream getCaseModel(String caseDefinitionId);

  /**
   * Gives access to a deployed case diagram, e.g., a PNG image, through a
   * stream of bytes.
   *
   * @param caseDefinitionId id of a {@link CaseDefinition}, cannot be null.
   * @return null when the diagram resource name of a {@link CaseDefinition} is null.
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/CaseDefinitionQuery.java" line="25">

---

# CaseDefinitionQuery Interface

The CaseDefinitionQuery interface provides a way to query the case definitions in the system. It extends the Query interface and provides a number of methods for specifying the criteria of the query.

```java
public interface CaseDefinitionQuery extends Query<CaseDefinitionQuery, CaseDefinition> {

  /**
   * Only select case definition with the given id.
   *
   * @param caseDefinitionId the id of the case definition
   */
  CaseDefinitionQuery caseDefinitionId(String caseDefinitionId);

  /**
   * Only select case definitions with the given ids.
   *
   * @param ids list of case definition ids
   */
  CaseDefinitionQuery caseDefinitionIdIn(String... ids);

  /**
   * Only select case definitions with the given category.
   *
   * @param caseDefinitionCategory the category of the case definition
   */
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/cmmn/entity/repository/CaseDefinitionQueryImpl.java" line="37">

---

# CaseDefinitionQuery Usage

The CaseDefinitionQuery interface is used in the CaseDefinitionQueryImpl class to implement the actual querying logic. This class provides the implementation for the methods defined in the CaseDefinitionQuery interface.

```java
public class CaseDefinitionQueryImpl extends AbstractQuery<CaseDefinitionQuery, CaseDefinition> implements CaseDefinitionQuery {

  private static final long serialVersionUID = 1L;

  protected String id;
  protected String[] ids;
  protected String category;
  protected String categoryLike;
  protected String name;
  protected String nameLike;
  protected String deploymentId;
  protected String key;
  protected String keyLike;
  protected String resourceName;
  protected String resourceNameLike;
  protected Integer version;
  protected boolean latest = false;

  protected boolean isTenantIdSet = false;
  protected String[] tenantIds;
  protected boolean includeDefinitionsWithoutTenantId = false;
```

---

</SwmSnippet>

# CaseDefinitionQuery Interface and Implementations

This section covers the CaseDefinitionQuery interface and its implementations.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/repository/CaseDefinitionQuery.java" line="21">

---

## CaseDefinitionQuery Interface

The CaseDefinitionQuery interface provides methods to filter and sort case definitions. It includes methods to select case definitions by id, category, name, key, and other parameters. The methods return a CaseDefinitionQuery object, allowing for method chaining.

```java
/**
 * @author Roman Smirnov
 *
 */
public interface CaseDefinitionQuery extends Query<CaseDefinitionQuery, CaseDefinition> {

  /**
   * Only select case definition with the given id.
   *
   * @param caseDefinitionId the id of the case definition
   */
  CaseDefinitionQuery caseDefinitionId(String caseDefinitionId);

  /**
   * Only select case definitions with the given ids.
   *
   * @param ids list of case definition ids
   */
  CaseDefinitionQuery caseDefinitionIdIn(String... ids);

  /**
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/cmmn/entity/repository/CaseDefinitionQueryImpl.java" line="30">

---

## CaseDefinitionQueryImpl Class

The CaseDefinitionQueryImpl class implements the CaseDefinitionQuery interface. It provides the functionality for the methods defined in the interface. For example, the caseDefinitionId method ensures that the caseDefinitionId is not null.

```java
import org.camunda.bpm.engine.repository.CaseDefinition;
import org.camunda.bpm.engine.repository.CaseDefinitionQuery;

/**
 * @author Roman Smirnov
 *
 */
public class CaseDefinitionQueryImpl extends AbstractQuery<CaseDefinitionQuery, CaseDefinition> implements CaseDefinitionQuery {

  private static final long serialVersionUID = 1L;

  protected String id;
  protected String[] ids;
  protected String category;
  protected String categoryLike;
  protected String name;
  protected String nameLike;
  protected String deploymentId;
  protected String key;
  protected String keyLike;
  protected String resourceName;
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest/src/main/java/org/camunda/bpm/engine/rest/dto/repository/CaseDefinitionQueryDto.java" line="27">

---

## CaseDefinitionQueryDto Class

The CaseDefinitionQueryDto class uses the CaseDefinitionQuery interface to create a new query, apply filters, and sort the results. It uses the methods of the CaseDefinitionQuery interface in its own methods.

```java
import org.camunda.bpm.engine.ProcessEngine;
import org.camunda.bpm.engine.repository.CaseDefinitionQuery;
import org.camunda.bpm.engine.rest.dto.AbstractQueryDto;
import org.camunda.bpm.engine.rest.dto.CamundaQueryParam;
import org.camunda.bpm.engine.rest.dto.converter.BooleanConverter;
import org.camunda.bpm.engine.rest.dto.converter.IntegerConverter;
import org.camunda.bpm.engine.rest.dto.converter.StringListConverter;

import com.fasterxml.jackson.databind.ObjectMapper;

/**
 *
 * @author Roman Smirnov
 *
 */
public class CaseDefinitionQueryDto extends AbstractQueryDto<CaseDefinitionQuery> {

  private static final String SORT_BY_ID_VALUE = "id";
  private static final String SORT_BY_KEY_VALUE = "key";
  private static final String SORT_BY_NAME_VALUE = "name";
  private static final String SORT_BY_VERSION_VALUE = "version";
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest/src/main/java/org/camunda/bpm/engine/rest/impl/CaseDefinitionRestServiceImpl.java" line="25">

---

## CaseDefinitionRestServiceImpl Class

The CaseDefinitionRestServiceImpl class uses the CaseDefinitionQuery interface to create a new query and execute it. It uses the toQuery method of the CaseDefinitionQueryDto class to convert the queryDto to a CaseDefinitionQuery.

```java
import org.camunda.bpm.engine.repository.CaseDefinition;
import org.camunda.bpm.engine.repository.CaseDefinitionQuery;
import org.camunda.bpm.engine.rest.CaseDefinitionRestService;
import org.camunda.bpm.engine.rest.dto.CountResultDto;
import org.camunda.bpm.engine.rest.dto.repository.CaseDefinitionDto;
import org.camunda.bpm.engine.rest.dto.repository.CaseDefinitionQueryDto;
import org.camunda.bpm.engine.rest.exception.RestException;
import org.camunda.bpm.engine.rest.sub.repository.CaseDefinitionResource;
import org.camunda.bpm.engine.rest.sub.repository.impl.CaseDefinitionResourceImpl;
import org.camunda.bpm.engine.rest.util.QueryUtil;

/**
 *
 * @author Roman Smirnov
 *
 */
public class CaseDefinitionRestServiceImpl extends AbstractRestProcessEngineAware implements CaseDefinitionRestService {

  public CaseDefinitionRestServiceImpl(String engineName, ObjectMapper objectMapper) {
    super(engineName, objectMapper);
  }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
