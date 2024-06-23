---
title: Approach to Error Handling in Job API
---
This document will cover the error handling in the Job API of the Citi-camunda repo. We'll cover:

1. How errors are handled in the Job API
2. The role of the `HistoricJobLog` interface in error handling
3. The use of `JobRestService` in managing errors.

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/base/app/views/processInstance/jobsTab.js" line="120">

---

# Error Handling in the Job API

Here, we can see how errors are handled in the Job API. The `Notifications.addError` function is used to display an error message when an error occurs while loading jobs.

```javascript
            Notifications.addError({
              status: $translate.instant('PLUGIN_JOBS'),
              message: $translate.instant('PLUGIN_JOBS_LOADING_ERROR')
            });
          } else {
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/history/HistoricJobLog.java" line="24">

---

# Role of the HistoricJobLog Interface

The `HistoricJobLog` interface provides a log containing information about job execution. It provides details about the complete lifecycle of a job, including when a job execution fails. This is crucial for error handling in the Job API.

```java
/**
 * <p>The {@link HistoricJobLog} is used to have a log containing
 * information about {@link Job job} execution. The log provides
 * details about the complete lifecycle of a {@link Job job}:</p>
 * <ul>
 *   <li>job created</li>
 *   <li>job execution failed</li>
 *   <li>job execution successful</li>
 *   <li>job was deleted</li>
 * </ul>
 *
 * An instance of {@link HistoricJobLog} represents a state in
 * the lifecycle of a {@link Job job}.
 *
 * @author Roman Smirnov
 *
 * @since 7.3
 */
public interface HistoricJobLog {

  /**
```

---

</SwmSnippet>

<SwmSnippet path="/engine-rest/engine-rest/src/main/java/org/camunda/bpm/engine/rest/JobRestService.java" line="36">

---

# Use of JobRestService in Error Management

The `JobRestService` interface provides several methods for managing jobs, including handling errors. For instance, the `getJobsCount` method returns the count of jobs and can be used to check for any discrepancies in the job count, which could indicate an error.

```java
	static final String PATH = "/job";

  @Path("/{id}")
  JobResource getJob(@PathParam("id") String jobId);

  @GET
  @Produces(MediaType.APPLICATION_JSON)
  List<JobDto> getJobs(@Context UriInfo uriInfo,
      @QueryParam("firstResult") Integer firstResult,
      @QueryParam("maxResults") Integer maxResults);


  @POST
  @Consumes(MediaType.APPLICATION_JSON)
  @Produces(MediaType.APPLICATION_JSON)
  List<JobDto> queryJobs(JobQueryDto queryDto,
      @QueryParam("firstResult") Integer firstResult,
      @QueryParam("maxResults") Integer maxResults);

  @GET
  @Path("/count")
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="follow-up"><sup>Powered by [Swimm](/)</sup></SwmMeta>
