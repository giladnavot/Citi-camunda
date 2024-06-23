---
title: Overview of Shortcut Plugins
---
Shortcut Plugins in the Citi-camunda project refer to a set of functionalities that provide users with keyboard shortcuts to perform certain actions in the tasklist interface. These plugins are primarily implemented in JavaScript and are part of the frontend UI of the application. They are designed to enhance user experience by providing quick and easy access to common tasks.

One of the key components of the Shortcut Plugins is the 'showShortcutHelp' class. This class is responsible for displaying a help modal that provides information about the available shortcuts to the user. The modal is triggered when the user clicks on a link element with the class 'showShortcutHelp'.

The 'showHelp' function is another important part of the Shortcut Plugins. This function is responsible for opening the help modal when the user requests it. The modal is created with a child scope of the provided scope, and it uses the 'showHelpTemplate' as its template.

The Shortcut Plugins also include a configuration for the 'shortcut-help' view. This configuration includes an 'id' property to identify the view, a 'template' property to specify the HTML template to be used for the view, and a 'controller' property to specify the controller for the view.

The Shortcut Plugins are registered as a module in the AngularJS framework. This module, 'cam.tasklist.shortcuts', is exported for use in other parts of the application.

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/shortcuts/plugins/action/cam-tasklist-shortcut-help-plugin.js" line="70">

---

# Shortcut Plugin Implementation

This is an example of a Shortcut Plugin configuration. The `id` property is used to uniquely identify the plugin, the `template` property specifies the HTML template to be used, and the `controller` property specifies the controller that handles the plugin's logic.

```javascript
var Configuration = function PluginConfiguration(ViewsProvider) {
  ViewsProvider.registerDefaultView('tasklist.navbar.action', {
    id: 'shortcut-help',
    template: helpLinkTemplate,
    controller: Controller,
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/shortcuts/plugins/action/cam-tasklist-shortcut-help-plugin.html" line="1">

---

# Shortcut Plugin Usage

This is an example of how a Shortcut Plugin is used in the UI. The `showShortcutHelp` class is associated with a click event that triggers the `showHelp` function.

```html
<a href
   class="showShortcutHelp"
   ng-click="showHelp()">
  {{ 'SHORTCUT_HELP' | translate }}
</a>
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/shortcuts/plugins/action/cam-tasklist-shortcut-help-plugin.js" line="59">

---

# Shortcut Plugin Activation

This is an example of how a Shortcut Plugin is activated. The `focus` method is called on the element associated with the `showShortcutHelp` class, bringing it into focus when the `showHelp` function is triggered.

```javascript
        function() {
          document.querySelector('a.showShortcutHelp').focus();
        },
        function() {
          document.querySelector('a.showShortcutHelp').focus();
        }
```

---

</SwmSnippet>

# Shortcut Plugins Functions

This section will provide an overview of the main functions in the Shortcut Plugins.

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/shortcuts/plugins/action/cam-tasklist-shortcut-help-plugin.js" line="49">

---

## showHelp Function

The `showHelp` function is used to open a modal window that displays the available keyboard shortcuts. It uses the `$modal.open` method to create the modal instance, passing in an object that specifies the scope, window class, size, and template for the modal. The `showHelp` function is triggered when the user clicks on the element with the 'showShortcutHelp' class, as defined in the 'cam-tasklist-shortcut-help-plugin.html' file.

```javascript
    $scope.showHelp = function() {
      var modalInstance = $modal.open({
        // creates a child scope of a provided scope
        scope: $scope,
        windowClass: 'shortcut-modal',
        size: 'lg',
        template: showHelpTemplate
      });

      modalInstance.result.then(
        function() {
          document.querySelector('a.showShortcutHelp').focus();
        },
        function() {
          document.querySelector('a.showShortcutHelp').focus();
        }
      );
    };
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/shortcuts/plugins/action/cam-tasklist-shortcut-help-plugin.js" line="70">

---

## Configuration Function

The `Configuration` function is used to register a default view for the 'tasklist.navbar.action' key. It uses the `ViewsProvider.registerDefaultView` method to register the view, passing in an object that specifies the id, template, controller, and priority for the view. This function is responsible for adding the shortcut help link to the tasklist navigation bar.

```javascript
var Configuration = function PluginConfiguration(ViewsProvider) {
  ViewsProvider.registerDefaultView('tasklist.navbar.action', {
    id: 'shortcut-help',
    template: helpLinkTemplate,
    controller: Controller,
    priority: 300
  });
};
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
