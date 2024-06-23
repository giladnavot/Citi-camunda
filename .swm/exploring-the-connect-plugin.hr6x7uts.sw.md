---
title: Exploring the Connect Plugin
---
The Connect Plugin in Citi-camunda is a component that enables the integration of external systems with the Camunda workflow engine. It is implemented as a Process Engine Plugin and is responsible for loading connectors at the initialization of the process engine. The plugin also adds a ConnectorParseListener to the process engine configuration, which listens for events during the parsing of a BPMN process. This allows the Connect Plugin to handle tasks that involve communication with external systems, such as HTTP requests.

<SwmSnippet path="/engine-plugins/connect-plugin/src/main/java/org/camunda/connect/plugin/impl/ConnectProcessEnginePlugin.java" line="28">

---

# ConnectProcessEnginePlugin Class

The `ConnectProcessEnginePlugin` class is the main class of the Connect Plugin. It extends the `AbstractProcessEnginePlugin` class and overrides the `preInit` method. This method is called during the initialization of the process engine and is responsible for setting up the Connect Plugin.

```java
public class ConnectProcessEnginePlugin extends AbstractProcessEnginePlugin {

  @Override
  public void preInit(ProcessEngineConfigurationImpl processEngineConfiguration) {
    // use classloader which loaded the plugin
    ClassLoader classloader = ClassLoaderUtil.getClassloader(ConnectProcessEnginePlugin.class);
    Connectors.loadConnectors(classloader);

    addConnectorParseListener(processEngineConfiguration);

    processEngineConfiguration.setTelemetryHttpConnector(Connectors.getConnector(Connectors.HTTP_CONNECTOR_ID));
  }

  private void addConnectorParseListener(ProcessEngineConfigurationImpl processEngineConfiguration) {
    List<BpmnParseListener> preParseListeners = processEngineConfiguration.getCustomPreBPMNParseListeners();
    if(preParseListeners == null) {
      preParseListeners = new ArrayList<BpmnParseListener>();
      processEngineConfiguration.setCustomPreBPMNParseListeners(preParseListeners);
    }
    preParseListeners.add(new ConnectorParseListener());
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine-plugins/connect-plugin/src/main/java/org/camunda/connect/plugin/impl/ConnectProcessEnginePlugin.java" line="30">

---

# preInit Method

The `preInit` method is where the Connect Plugin is set up. It loads the connectors, adds a connector parse listener, and sets the telemetry HTTP connector.

```java
  @Override
  public void preInit(ProcessEngineConfigurationImpl processEngineConfiguration) {
    // use classloader which loaded the plugin
    ClassLoader classloader = ClassLoaderUtil.getClassloader(ConnectProcessEnginePlugin.class);
    Connectors.loadConnectors(classloader);

    addConnectorParseListener(processEngineConfiguration);

    processEngineConfiguration.setTelemetryHttpConnector(Connectors.getConnector(Connectors.HTTP_CONNECTOR_ID));
  }
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/assembly/src/main/runtime/develop/resources/META-INF/processes.xml" line="20">

---

# Usage of ConnectProcessEnginePlugin

The `ConnectProcessEnginePlugin` is added as a plugin in the Camunda configuration file. This makes it available for use in the process engine.

```xml
      <plugin>
        <class>org.camunda.connect.plugin.impl.ConnectProcessEnginePlugin</class>
      </plugin>
```

---

</SwmSnippet>

# Connect Plugin Functions

This section will cover the main functions of the Connect Plugin in the Citi-camunda repository.

<SwmSnippet path="/engine-plugins/connect-plugin/src/main/java/org/camunda/connect/plugin/impl/ConnectProcessEnginePlugin.java" line="30">

---

## preInit Function

The `preInit` function is part of the `ConnectProcessEnginePlugin` class. This function is responsible for initializing the process engine configuration. It loads the connectors using the classloader which loaded the plugin and adds the connector parse listener to the process engine configuration.

```java
  @Override
  public void preInit(ProcessEngineConfigurationImpl processEngineConfiguration) {
    // use classloader which loaded the plugin
    ClassLoader classloader = ClassLoaderUtil.getClassloader(ConnectProcessEnginePlugin.class);
    Connectors.loadConnectors(classloader);

    addConnectorParseListener(processEngineConfiguration);

    processEngineConfiguration.setTelemetryHttpConnector(Connectors.getConnector(Connectors.HTTP_CONNECTOR_ID));
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine-plugins/connect-plugin/src/main/java/org/camunda/connect/plugin/impl/ConnectProcessEnginePlugin.java" line="41">

---

## addConnectorParseListener Function

The `addConnectorParseListener` function is a private method in the `ConnectProcessEnginePlugin` class. It adds a new `ConnectorParseListener` to the list of pre-parse listeners in the process engine configuration.

```java
  private void addConnectorParseListener(ProcessEngineConfigurationImpl processEngineConfiguration) {
    List<BpmnParseListener> preParseListeners = processEngineConfiguration.getCustomPreBPMNParseListeners();
    if(preParseListeners == null) {
      preParseListeners = new ArrayList<BpmnParseListener>();
      processEngineConfiguration.setCustomPreBPMNParseListeners(preParseListeners);
    }
    preParseListeners.add(new ConnectorParseListener());
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine-plugins/connect-plugin/src/main/java/org/camunda/connect/plugin/impl/ServiceTaskConnectorActivityBehavior.java" line="70">

---

## applyInputParameters Function

The `applyInputParameters` function is part of the `ServiceTaskConnectorActivityBehavior` class. This function applies the input parameters to the connector request. If the IO mapping is not null, it creates a variable scope for input parameters, executes the connector input parameters, and writes the local variables to the request.

```java
  protected void applyInputParameters(ActivityExecution execution, ConnectorRequest<?> request) {
    if(ioMapping != null) {
      // create variable scope for input parameters
      ConnectorVariableScope connectorInputVariableScope = new ConnectorVariableScope((AbstractVariableScope) execution);
      // execute the connector input parameters
      ioMapping.executeInputParameters(connectorInputVariableScope);
      // write the local variables to the request.
      connectorInputVariableScope.writeToRequest(request);
    }
  }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
