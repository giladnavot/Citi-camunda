---
title: Overview of the Backend Engine
---
The Backend Engine in Citi-camunda refers to the Camunda Platform 7, an open-source platform for workflow and process automation. It is a native BPMN 2.0 process engine that runs inside the Java Virtual Machine and can be embedded inside any Java application and any Runtime Container. The Backend Engine is responsible for process implementation and execution, process design, process operations, and human task management. It is highly integrable and embeddable, making it a versatile tool for developers.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/ManagementServiceImpl.java" line="110">

---

# ManagementServiceImpl Class

The `ManagementServiceImpl` class is a crucial part of the Backend Engine. It provides methods for managing and manipulating processes, such as registering and unregistering process applications, executing and deleting jobs, and setting job retries. This class is used throughout the codebase to perform various operations related to process management.

```java
public class ManagementServiceImpl extends ServiceImpl implements ManagementService {

  protected ProcessEngineConfiguration processEngineConfiguration;

  public ManagementServiceImpl(ProcessEngineConfiguration processEngineConfiguration) {
    this.processEngineConfiguration = processEngineConfiguration;
  }

  public ProcessApplicationRegistration registerProcessApplication(String deploymentId, ProcessApplicationReference reference) {
    return commandExecutor.execute(new RegisterProcessApplicationCmd(deploymentId, reference));
  }

  public void unregisterProcessApplication(String deploymentId, boolean removeProcessesFromCache) {
    commandExecutor.execute(new UnregisterProcessApplicationCmd(deploymentId, removeProcessesFromCache));
  }

  public void unregisterProcessApplication(Set<String> deploymentIds, boolean removeProcessesFromCache) {
    commandExecutor.execute(new UnregisterProcessApplicationCmd(deploymentIds, removeProcessesFromCache));
  }

  public String getProcessApplicationForDeployment(String deploymentId) {
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/ProcessEngineInfo.java" line="24">

---

# ProcessEngineInfo Interface

The `ProcessEngineInfo` interface provides information about the initialization of the process engine. It offers methods to get the name of the process engine, the resources the engine was configured from, and any exceptions that occurred during initialization. This interface is used to manage and monitor the state of the process engine.

```java
public interface ProcessEngineInfo {

  /**
   * Returns the name of the process engine.
   */
  String getName();

  /**
   * Returns the resources the engine was configured from.
   */
  String getResourceUrl();

  /**
   * Returns the exception stacktrace in case an exception occurred while initializing
   * the engine. When no exception occured, null is returned.
   */
  String getException();

}
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/ProcessEngines.java" line="63">

---

# ProcessEngines Class

The `ProcessEngines` class is responsible for initializing and closing process engines in server environments. It maintains a registry of all created ProcessEngines and provides methods to start, shutdown, register, and unregister process engines. This class plays a vital role in managing the lifecycle of process engines in the Backend Engine.

```java
public abstract class ProcessEngines {

  private final static ProcessEngineLogger LOG = ProcessEngineLogger.INSTANCE;

  public static final String NAME_DEFAULT = "default";

  protected static boolean isInitialized = false;
  protected static Map<String, ProcessEngine> processEngines = new HashMap<String, ProcessEngine>();
  protected static Map<String, ProcessEngineInfo> processEngineInfosByName = new HashMap<String, ProcessEngineInfo>();
  protected static Map<String, ProcessEngineInfo> processEngineInfosByResourceUrl = new HashMap<String, ProcessEngineInfo>();
  protected static List<ProcessEngineInfo> processEngineInfos = new ArrayList<ProcessEngineInfo>();

  public synchronized static void init() {
    init(true);
  }

  /** Initializes all process engines that can be found on the classpath for
   * resources <code>camunda.cfg.xml</code> (plain Activiti style configuration)
   * and for resources <code>activiti-context.xml</code> (Spring style configuration). */
  public synchronized static void init(boolean forceCreate) {
    if (!isInitialized) {
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/jobexecutor/JobExecutor.java" line="43">

---

# JobExecutor Class

The `JobExecutor` class is responsible for performing background work or jobs. It is capable of dispatching to multiple process engines, allowing multiple process engines to share a single Thread Pool for performing Background Work. This class is essential for managing and executing jobs in the Backend Engine.

```java
public abstract class JobExecutor {

  private final static JobExecutorLogger LOG = ProcessEngineLogger.JOB_EXECUTOR_LOGGER;

  protected String name = "JobExecutor["+getClass().getName()+"]";
  protected List<ProcessEngineImpl> processEngines = new CopyOnWriteArrayList<>();
  protected AcquireJobsCommandFactory acquireJobsCmdFactory;
  protected AcquireJobsRunnable acquireJobsRunnable;
  protected RejectedJobsHandler rejectedJobsHandler;
  protected Thread jobAcquisitionThread;

  protected boolean isAutoActivate = false;
  protected boolean isActive = false;

  protected int maxJobsPerAcquisition = 3;

  // waiting when job acquisition is idle
  protected int waitTimeInMillis = 5 * 1000;
  protected float waitIncreaseFactor = 2;
  protected long maxWait = 60 * 1000;

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
