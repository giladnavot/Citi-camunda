---
title: Integrating Additional Tools with the Feel API to Enhance Functionality
---
This document will cover the process of integrating additional tools and components with the Feel API to extend its capabilities. The topics covered include:

1. Understanding the Feel API
2. How to extend the capabilities of the Feel API
3. Code examples of integration with the Feel API.

# Understanding the Feel API

The Feel API is part of the Camunda Platform 7, an open-source platform for workflow and process automation. It provides a native BPMN 2.0 process engine that runs inside the Java Virtual Machine and can be embedded inside any Java application and any Runtime Container. It includes components for process implementation and execution, process design, process operations, and human task management. The platform is highly integrable and embeddable.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/container/impl/deployment/DeployProcessArchiveStep.java" line="76">

---

# How to extend the capabilities of the Feel API

The `performOperationStep` method is a good example of how to extend the capabilities of the Feel API. This method is responsible for building a deployment map, scanning for additional process definitions, and performing process engine deployment. It shows how additional tools and components can be integrated with the Feel API.

```java
  @Override
  public void performOperationStep(DeploymentOperation operationContext) {

    final PlatformServiceContainer serviceContainer = operationContext.getServiceContainer();
    final AbstractProcessApplication processApplication = operationContext.getAttachment(Attachments.PROCESS_APPLICATION);
    final ClassLoader processApplicationClassloader = processApplication.getProcessApplicationClassloader();

    ProcessEngine processEngine = getProcessEngine(serviceContainer, processApplication.getDefaultDeployToEngineName());

    // start building deployment map
    Map<String, byte[]> deploymentMap = new HashMap<String, byte[]>();

    // add all processes listed in the processes.xml
    List<String> listedProcessResources = processArchive.getProcessResourceNames();
    for (String processResource : listedProcessResources) {
      InputStream resourceAsStream = null;
      try {
        resourceAsStream = processApplicationClassloader.getResourceAsStream(processResource);
        byte[] bytes = IoUtil.readInputStream(resourceAsStream, processResource);
        deploymentMap.put(processResource, bytes);
      } finally {
```

---

</SwmSnippet>

<SwmSnippet path="/distro/wildfly/subsystem/src/main/java/org/camunda/bpm/container/impl/jboss/service/ProcessApplicationDeploymentService.java" line="136">

---

# Code examples of integration with the Feel API

The `performDeployment` method is another example of how to extend the capabilities of the Feel API. This method is responsible for building the deployment, enabling duplicate filtering, setting the name for the deployment, and adding deployment resources. It shows how additional tools and components can be integrated with the Feel API.

```java
  protected void performDeployment() throws StartException {

    ManagedReference reference = null;
    try {

      // get process engine
      ProcessEngine processEngine = processEngineSupplier.get();

      // get the process application component
      ProcessApplicationInterface processApplication = null;
      if(paComponentViewSupplier != null) {
        ComponentView componentView = paComponentViewSupplier.get();
        reference = componentView.createInstance();
        processApplication = (ProcessApplicationInterface) reference.getInstance();
      } else {
        processApplication = noViewProcessApplicationSupplier.get();
      }

      // get the application name
      String processApplicationName = processApplication.getName();

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="follow-up"><sup>Powered by [Swimm](/)</sup></SwmMeta>
