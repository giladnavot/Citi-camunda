---
title: Understanding Migration Validation
---
Migration Validation in the Citi-camunda project refers to the process of verifying the correctness of a migration plan. This is done through interfaces like `MigrationPlanValidationReport`, `MigrationInstructionValidationReport`, and `MigrationVariableValidationReport`. These interfaces collect validation failures for all instructions and variables of the migration plan which contain failures. If the validation process encounters any failures, a `MigrationPlanValidationException` is thrown. This exception contains a `MigrationPlanValidationReport` that details all validation errors.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/migration/MigrationPlanValidationReport.java" line="22">

---

# MigrationPlanValidationReport Interface

The `MigrationPlanValidationReport` interface provides methods to get the migration plan, check if there are any reports, and get the instruction and variable reports.

```java
/**
 * Collects the migration validation reports for
 * all instructions and variables of the migration plan which contain failures.
 */
public interface MigrationPlanValidationReport {

  /**
   * @return the migration plan of the validation report
   */
  MigrationPlan getMigrationPlan();

  /**
   * @return {@code true} if either instruction or variable reports exist, {@code false} otherwise
   */
  boolean hasReports();

  /**
   * @return true if instructions reports exist, false otherwise
   */
  boolean hasInstructionReports();

```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/migration/MigrationInstructionValidationReport.java" line="23">

---

# MigrationInstructionValidationReport Interface

The `MigrationInstructionValidationReport` interface provides methods to get the migration instruction and to check if the report contains failures.

```java
/**
 * Collects the validation failures for a single migration
 * instruction.
 */
public interface MigrationInstructionValidationReport {

  /**
   * @return the migration instruction of this report
   */
  MigrationInstruction getMigrationInstruction();

  /**
   * @return true if the report contains failures, false otherwise
   */
  boolean hasFailures();

  /**
   * @return the list of failure messages
   */
  List<String> getFailures();

```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/migration/MigrationVariableValidationReport.java" line="23">

---

# MigrationVariableValidationReport Interface

The `MigrationVariableValidationReport` interface provides methods to get the typed value and to check if the report contains failures.

```java
/**
 * Collects the validation failures for a single migration
 * variable.
 */
public interface MigrationVariableValidationReport {

  /**
   * @return the variable's {@link TypedValue}
   */
  <T extends TypedValue> T getTypedValue();

  /**
   * @return {@code true} if the report contains failures, {@code false} otherwise
   */
  boolean hasFailures();

  /**
   * @return the list of failure messages
   */
  List<String> getFailures();

```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/migration/MigrationPlanValidationException.java" line="22">

---

# MigrationPlanValidationException Class

The `MigrationPlanValidationException` class is thrown when a migration plan is not valid. It contains a `MigrationPlanValidationReport` that contains the details for all validation errors.

```java
/**
 * Thrown if a migration plan is not valid, e.g. because it contains instructions that can in general not be executed.
 * Contains a {@link MigrationPlanValidationReport} that contains the details for all validation erorrs.
 *
 * @author Thorben Lindhauer
 */
public class MigrationPlanValidationException extends BadUserRequestException {

  private static final long serialVersionUID = 1L;

  protected MigrationPlanValidationReport validationReport;

  public MigrationPlanValidationException(String message, MigrationPlanValidationReport validationReport) {
    super(message);
    this.validationReport = validationReport;
  }

  /**
   * A report with all invalid instructions
   */
  public MigrationPlanValidationReport getValidationReport() {
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/migration/MigratingProcessInstanceValidationException.java" line="21">

---

# MigratingProcessInstanceValidationException Class

The `MigratingProcessInstanceValidationException` class is thrown when at least one migration instruction cannot be applied to the activity instance it matches. It contains a validation report that contains the details for all validation errors.

```java
/**
 * Thrown if at least one migration instruction cannot be applied to the activity instance it matches. Contains
 * a object that contains the details for all validation errors.
 *
 * @author Thorben Lindhauer
 */
public class MigratingProcessInstanceValidationException extends ProcessEngineException {

  private static final long serialVersionUID = 1L;

  protected MigratingProcessInstanceValidationReport validationReport;

  public MigratingProcessInstanceValidationException(String message, MigratingProcessInstanceValidationReport validationReport) {
    super(message);
    this.validationReport = validationReport;
  }

  /**
   * A report with all instructions that cannot be applied to the given process instance
   */
  public MigratingProcessInstanceValidationReport getValidationReport() {
```

---

</SwmSnippet>

# Migration Validation Functions

This section provides an overview of the main functions involved in Migration Validation in the Citi-camunda repository.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/migration/MigrationPlanValidationReport.java" line="26">

---

## MigrationPlanValidationReport

The `MigrationPlanValidationReport` interface collects the migration validation reports for all instructions and variables of the migration plan which contain failures. It provides methods to get the migration plan, check if reports exist, and retrieve all instruction and variable reports.

```java
public interface MigrationPlanValidationReport {

  /**
   * @return the migration plan of the validation report
   */
  MigrationPlan getMigrationPlan();

  /**
   * @return {@code true} if either instruction or variable reports exist, {@code false} otherwise
   */
  boolean hasReports();

  /**
   * @return true if instructions reports exist, false otherwise
   */
  boolean hasInstructionReports();

  /**
   * @return {@code true} if variable reports exist, {@code false} otherwise
   */
  boolean hasVariableReports();
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/migration/MigrationInstructionValidationReport.java" line="27">

---

## MigrationInstructionValidationReport

The `MigrationInstructionValidationReport` interface collects the validation failures for a single migration instruction. It provides methods to get the migration instruction, check if the report contains failures, and retrieve the list of failure messages.

```java
public interface MigrationInstructionValidationReport {

  /**
   * @return the migration instruction of this report
   */
  MigrationInstruction getMigrationInstruction();

  /**
   * @return true if the report contains failures, false otherwise
   */
  boolean hasFailures();

  /**
   * @return the list of failure messages
   */
  List<String> getFailures();

}
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/migration/MigrationPlanValidationException.java" line="28">

---

## MigrationPlanValidationException

The `MigrationPlanValidationException` class is thrown if a migration plan is not valid. It contains a `MigrationPlanValidationReport` that contains the details for all validation errors.

```java
public class MigrationPlanValidationException extends BadUserRequestException {

  private static final long serialVersionUID = 1L;

  protected MigrationPlanValidationReport validationReport;

  public MigrationPlanValidationException(String message, MigrationPlanValidationReport validationReport) {
    super(message);
    this.validationReport = validationReport;
  }

  /**
   * A report with all invalid instructions
   */
  public MigrationPlanValidationReport getValidationReport() {
    return validationReport;
  }

}
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/migration/MigratingProcessInstanceValidationException.java" line="27">

---

## MigratingProcessInstanceValidationException

The `MigratingProcessInstanceValidationException` class is thrown if at least one migration instruction cannot be applied to the activity instance it matches. It contains a `MigratingProcessInstanceValidationReport` that contains the details for all validation errors.

```java
public class MigratingProcessInstanceValidationException extends ProcessEngineException {

  private static final long serialVersionUID = 1L;

  protected MigratingProcessInstanceValidationReport validationReport;

  public MigratingProcessInstanceValidationException(String message, MigratingProcessInstanceValidationReport validationReport) {
    super(message);
    this.validationReport = validationReport;
  }

  /**
   * A report with all instructions that cannot be applied to the given process instance
   */
  public MigratingProcessInstanceValidationReport getValidationReport() {
    return validationReport;
  }

}
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/migration/MigratingTransitionInstanceValidationReport.java" line="26">

---

## MigratingTransitionInstanceValidationReport

The `MigratingTransitionInstanceValidationReport` interface collects all failures for a migrating transition instance. It provides methods to get the source scope id, transition instance id, migration instruction, check if the report contains failures, and retrieve the list of failures.

```java
public interface MigratingTransitionInstanceValidationReport {

  /**
   * @return the id of the source scope of the migrating transition instance
   */
  String getSourceScopeId();

  /**
   * @return the transition instance id of this report
   */
  String getTransitionInstanceId();

  /**
   * @return the migration instruction that cannot be applied
   */
  MigrationInstruction getMigrationInstruction();

  /**
   * @return true if the reports contains failures, false otherwise
   */
  boolean hasFailures();
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/migration/MigratingProcessInstanceValidationReport.java" line="29">

---

## MigratingProcessInstanceValidationReport

The `MigratingProcessInstanceValidationReport` interface collects general failures and the migrating activity instance validation reports for a migrating process instance. It provides methods to get the process instance id, list of general failures, activity instance validation reports, and transition instance validation reports.

```java
public interface MigratingProcessInstanceValidationReport {

  /**
   * @return the id of the process instance that the migration plan is applied to
   */
  String getProcessInstanceId();

  /**
   * @return the list of general failures of the migrating process instance
   */
  List<String> getFailures();

  /**
   * @return true if general failures or activity instance validation reports exist, false otherwise
   */
  boolean hasFailures();

  /**
   * @return the list of activity instance validation reports
   */
  List<MigratingActivityInstanceValidationReport> getActivityInstanceReports();
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
