---
title: Guide to Integrating New Plugins into Citi-Camunda
---
This document will cover the process of integrating new plugins into the existing structure of the Citi-camunda project. We'll cover:

1. How plugins are loaded in the frontend
2. How plugins are parsed and integrated in the backend
3. How plugins are added to the process engine configuration

<SwmSnippet path="/webapps/frontend/ui/common/scripts/services/plugins/loadPlugins.js" line="68">

---

# Loading Plugins in the Frontend

In the frontend, plugins are loaded asynchronously using `Promise.all(fetchers)`. The loaded modules are reduced into an accumulator (`acc`), which is returned as the final list of loaded plugins.

```javascript
  return (await Promise.all(fetchers)).reduce((acc, module) => {
    const plugins = module.default;
    if (!plugins) {
      return acc;
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/container/impl/metadata/DeploymentMetadataParse.java" line="78">

---

# Parsing and Integrating Plugins in the Backend

In the backend, the `parseProcessEngine` method is used to parse and integrate plugins. It creates a new `ProcessEngineXmlImpl` object, sets its properties, and adds it to the list of parsed engines. If a `PLUGINS` tag is found in the child elements of the process engine element, the `parseProcessEnginePlugins` method is called to parse and integrate the plugins.

```java
  protected void parseProcessEngine(Element element, List<ProcessEngineXml> parsedProcessEngines) {

    ProcessEngineXmlImpl processEngine = new ProcessEngineXmlImpl();

    // set name
    processEngine.setName(element.attribute(NAME));

    // set default
    String defaultValue = element.attribute(DEFAULT);
    if(defaultValue == null || defaultValue.isEmpty()) {
      processEngine.setDefault(false);
    } else {
      processEngine.setDefault(Boolean.parseBoolean(defaultValue));
    }

    Map<String, String> properties = new HashMap<String, String>();
    List<ProcessEnginePluginXml> plugins = new ArrayList<ProcessEnginePluginXml>();

    for (Element childElement : element.elements()) {
      if(CONFIGURATION.equals(childElement.getTagName())) {
        processEngine.setConfigurationClass(childElement.getText());
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/container/impl/deployment/StartProcessEngineStep.java" line="65">

---

# Adding Plugins to the Process Engine Configuration

In the `performOperationStep` method, plugins are added to the process engine configuration. The `configurePlugins` method is called to instantiate the plugins and add them to the configuration. Additional plugins can be added using the `addAdditionalPlugins` method.

```java
  public void performOperationStep(DeploymentOperation operationContext) {

    final PlatformServiceContainer serviceContainer = operationContext.getServiceContainer();
    final AbstractProcessApplication processApplication = operationContext.getAttachment(PROCESS_APPLICATION);

    ClassLoader classLoader = null;

    if(processApplication != null) {
      classLoader = processApplication.getProcessApplicationClassloader();
    }

    String configurationClassName = processEngineXml.getConfigurationClass();

    if(configurationClassName == null || configurationClassName.isEmpty()) {
      configurationClassName = StandaloneProcessEngineConfiguration.class.getName();
    }

    // create & instantiate configuration class
    Class<? extends ProcessEngineConfigurationImpl> configurationClass = loadClass(configurationClassName, classLoader, ProcessEngineConfigurationImpl.class);
    ProcessEngineConfigurationImpl configuration = ReflectUtil.createInstance(configurationClass);

```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="follow-up"><sup>Powered by [Swimm](/)</sup></SwmMeta>
