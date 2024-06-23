---
title: Understanding the Spin Plugin
---
The Spin Plugin is a component of the Camunda Platform that provides data format conversion capabilities. It allows for the transformation of data between different formats such as JSON and XML. This is particularly useful in the context of process automation where data may be received in various formats. The plugin is highly configurable, allowing for the enabling or disabling of certain processing features such as XXE and secure XML processing.

<SwmSnippet path="/engine-plugins/spin-plugin/src/main/java/org/camunda/spin/plugin/impl/SpinProcessEnginePlugin.java" line="37">

---

# SpinProcessEnginePlugin Class

The `SpinProcessEnginePlugin` class is a key part of the Spin Plugin. It extends the `SpinConfiguration` class and provides methods for initializing and configuring the plugin. It also provides methods for registering serializers, function mappers, script resolvers, and value types.

```java
/**
 * @author Thorben Lindhauer
 *
 */
public class SpinProcessEnginePlugin extends SpinConfiguration {

  @Override
  public void preInit(ProcessEngineConfigurationImpl processEngineConfiguration) {
    // use classloader which loaded the plugin
    ClassLoader classloader = ClassLoaderUtil.getClassloader(SpinProcessEnginePlugin.class);

    // use Spin plugin configuration properties
    Map<String, Object> configurationOptions = new HashMap<>();
    configurationOptions.put(XXE_PROPERTY, isEnableXxeProcessing());
    configurationOptions.put(SP_PROPERTY, isEnableSecureXmlProcessing());

    DataFormats.loadDataFormats(classloader, configurationOptions);
  }

  @Override
  public void postInit(ProcessEngineConfigurationImpl processEngineConfiguration) {
```

---

</SwmSnippet>

<SwmSnippet path="/engine-plugins/spin-plugin/src/main/java/org/camunda/spin/plugin/impl/SpinProcessEnginePlugin.java" line="43">

---

# preInit Method

The `preInit` method is called during the initialization of the Spin Plugin. It sets up the classloader and configuration options for the plugin, and loads the data formats.

```java
  @Override
  public void preInit(ProcessEngineConfigurationImpl processEngineConfiguration) {
    // use classloader which loaded the plugin
    ClassLoader classloader = ClassLoaderUtil.getClassloader(SpinProcessEnginePlugin.class);

    // use Spin plugin configuration properties
    Map<String, Object> configurationOptions = new HashMap<>();
    configurationOptions.put(XXE_PROPERTY, isEnableXxeProcessing());
    configurationOptions.put(SP_PROPERTY, isEnableSecureXmlProcessing());

    DataFormats.loadDataFormats(classloader, configurationOptions);
  }
```

---

</SwmSnippet>

<SwmSnippet path="/engine-plugins/spin-plugin/src/main/java/org/camunda/spin/plugin/impl/SpinPluginLogger.java" line="26">

---

# SpinPluginLogger Class

The `SpinPluginLogger` class is used for logging within the Spin Plugin. It extends the `BaseLogger` class and uses the `PROJECT_CODE` constant to identify the plugin in the logs.

```java
public class SpinPluginLogger extends BaseLogger {

  public static final String PROJECT_CODE = "SPIN-PLUGIN";

  public static final SpinPluginLogger LOGGER = BaseLogger.createLogger(SpinPluginLogger.class, PROJECT_CODE, "org.camunda.spin.plugin", "01");
```

---

</SwmSnippet>

# Spin Plugin Functions

This section will cover the main functions of the Spin Plugin: SpinProcessEnginePlugin, SpinFunctions, and SpinConfiguration.

<SwmSnippet path="/engine-plugins/spin-plugin/src/main/java/org/camunda/spin/plugin/impl/SpinProcessEnginePlugin.java" line="41">

---

## SpinProcessEnginePlugin

The `SpinProcessEnginePlugin` class extends the `SpinConfiguration` class and overrides its `preInit` and `postInit` methods. These methods are used to initialize and configure the plugin before and after the process engine configuration respectively. The `preInit` method loads data formats using the classloader that loaded the plugin and the `postInit` method registers function mappers, script resolvers, serializers, value types, and fallback serializers.

```java
public class SpinProcessEnginePlugin extends SpinConfiguration {

  @Override
  public void preInit(ProcessEngineConfigurationImpl processEngineConfiguration) {
    // use classloader which loaded the plugin
    ClassLoader classloader = ClassLoaderUtil.getClassloader(SpinProcessEnginePlugin.class);

    // use Spin plugin configuration properties
    Map<String, Object> configurationOptions = new HashMap<>();
    configurationOptions.put(XXE_PROPERTY, isEnableXxeProcessing());
    configurationOptions.put(SP_PROPERTY, isEnableSecureXmlProcessing());

    DataFormats.loadDataFormats(classloader, configurationOptions);
  }

  @Override
  public void postInit(ProcessEngineConfigurationImpl processEngineConfiguration) {
    registerFunctionMapper(processEngineConfiguration);
    registerScriptResolver(processEngineConfiguration);
    registerSerializers(processEngineConfiguration);
    registerValueTypes(processEngineConfiguration);
```

---

</SwmSnippet>

<SwmSnippet path="/engine-plugins/spin-plugin/src/main/java/org/camunda/spin/plugin/impl/SpinFunctions.java" line="31">

---

## SpinFunctions

The `SpinFunctions` class defines constants for the Spin functions. These constants are used to register the Spin functions in the `SpinProcessEnginePlugin` class.

```java
public class SpinFunctions {
  public static final String S = "S";
  public static final String XML = "XML";
  public static final String JSON = "JSON";
}
```

---

</SwmSnippet>

<SwmSnippet path="/engine-plugins/spin-plugin/src/main/java/org/camunda/spin/plugin/impl/SpinConfiguration.java" line="24">

---

## SpinConfiguration

The `SpinConfiguration` class is a Java Bean that holds the Spin configuration properties. It has methods to enable or disable XXE processing and secure XML processing.

```java
public class SpinConfiguration extends AbstractProcessEnginePlugin {

  protected static final String XXE_PROPERTY = "xxe-processing";
  protected static final String SP_PROPERTY = "secure-processing";

  protected boolean enableXxeProcessing = false;
  protected boolean enableSecureXmlProcessing = true;

  public boolean isEnableXxeProcessing() {
    return enableXxeProcessing;
  }

  public void setEnableXxeProcessing(boolean enableXxeProcessing) {
    this.enableXxeProcessing = enableXxeProcessing;
  }

  public boolean isEnableSecureXmlProcessing() {
    return enableSecureXmlProcessing;
  }

  public void setEnableSecureXmlProcessing(boolean enableSecureXmlProcessing) {
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
