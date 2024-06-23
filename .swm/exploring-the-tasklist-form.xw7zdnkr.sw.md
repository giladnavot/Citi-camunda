---
title: Exploring the Tasklist Form
---
The Tasklist Form in Citi-camunda refers to a form that is used in the tasklist section of the application. It is a key component in the task management process, allowing users to interact with tasks. The form is defined and manipulated through various functions and properties in the codebase. For instance, the 'getTasklistForm' function retrieves the current form, while the 'showForm' function displays the form to the user. The form can be of different types, such as 'generic', 'embedded', 'external', or 'camunda-forms', determined by the 'parseForm' function. The form's properties and behavior can be customized through various options and parameters.

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/form/directives/cam-tasklist-form.js" line="307">

---

## Using getTasklistForm

The `getTasklistForm` function is used to retrieve the current state of the Tasklist Form. It returns the `tasklistForm` object from the `$scope`.

```javascript
        this.getTasklistForm = function() {
          return $scope.tasklistForm;
        };
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/form/directives/cam-tasklist-form-generic.js" line="82">

---

## Using showForm

The `showForm` function is used to display the form with the given parameters. It takes in `tasklistForm` and `params` as arguments, makes a copy of the params, and extends them with additional properties before creating a new `CamForm` with these parameters.

```javascript
        function showForm(tasklistForm, params) {
          params = angular.copy(params);

          delete params.processDefinitionKey;

          angular.extend(params, {
            client: camAPI,
            formElement: formElement,
            done: done
          });

          $scope.camForm = camForm = new CamForm(params);
        }
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/form/directives/cam-tasklist-form.js" line="131">

---

## Using parseForm

The `parseForm` function is used to parse the form and set its type and key based on certain conditions. It checks if the form is already parsed, if not, it determines the form type and key based on the form's `key` and `camundaFormRef` properties and the task or process definition id in `$scope.params`.

```javascript
        function parseForm(form) {
          // Form is already parsed
          if (form.type) {
            setAsynchronousFormKey(form.key);
            return;
          }

          var key = form.key,
            camundaFormRef = form.camundaFormRef,
            applicationContextPath = form.contextPath;

          // structure may be [embedded:][app:]formKey
          // structure may be [embedded:][deployment:]formKey

          // structure may be [app:]formKey
          // structure may be [deployment:]formKey

          if (!key && !camundaFormRef) {
            form.type = 'generic';
            return;
          }
```

---

</SwmSnippet>

# Tasklist Form Functions

The Tasklist Form is a key component in the Citi-camunda repository. It is responsible for managing various tasks related to form handling in the application. This section will explain the main functions and properties of the Tasklist Form.

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/form/directives/cam-tasklist-form.js" line="36">

---

## noop Function

The `noop` function is a simple no-operation function. It doesn't perform any operation and is used as a placeholder when a function is expected but not necessary.

```javascript
}

var noop = function() {};

module.exports = function() {
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/form/directives/cam-tasklist-form.js" line="90">

---

## apply Function

The `apply` function is used to apply changes to the scope. It checks the phase of the $scope and if it's not already in the $apply or $digest phase, it triggers the $apply method to ensure that any changes to the scope are propagated properly.

```javascript
        const apply = () => {
          var phase = $scope.$root.$$phase;
          if (phase !== '$apply' && phase !== '$digest') {
            $scope.$apply();
          }
        };
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/form/directives/cam-tasklist-form.js" line="131">

---

## parseForm Function

The `parseForm` function is used to parse the form and set its type and key. It handles different form structures and sets the form type accordingly. It also sets the asynchronous form key using the `setAsynchronousFormKey` function.

```javascript
        function parseForm(form) {
          // Form is already parsed
          if (form.type) {
            setAsynchronousFormKey(form.key);
            return;
          }

          var key = form.key,
            camundaFormRef = form.camundaFormRef,
            applicationContextPath = form.contextPath;

          // structure may be [embedded:][app:]formKey
          // structure may be [embedded:][deployment:]formKey

          // structure may be [app:]formKey
          // structure may be [deployment:]formKey

          if (!key && !camundaFormRef) {
            form.type = 'generic';
            return;
          }
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/form/directives/cam-tasklist-form.js" line="303">

---

## getOptions Function

The `getOptions` function is used to get the options for the form. It returns the options from the scope or an empty object if no options are set.

```javascript
        this.getOptions = function() {
          return $scope.options || {};
        };
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/form/directives/cam-tasklist-form.js" line="307">

---

## getTasklistForm Function

The `getTasklistForm` function is used to get the tasklist form from the scope.

```javascript
        this.getTasklistForm = function() {
          return $scope.tasklistForm;
        };
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/form/directives/cam-tasklist-form-generic.js" line="82">

---

## showForm Function

The `showForm` function is used to display the form. It takes the tasklist form and parameters as arguments, extends the parameters with additional properties, and creates a new instance of CamForm.

```javascript
        function showForm(tasklistForm, params) {
          params = angular.copy(params);

          delete params.processDefinitionKey;

          angular.extend(params, {
            client: camAPI,
            formElement: formElement,
            done: done
          });

          $scope.camForm = camForm = new CamForm(params);
        }

        var done = function(err, _camForm) {
          if (err) {
            return formController.notifyFormInitializationFailed(err);
          }
          camForm = _camForm;

          var formName = _camForm.formElement.attr('name');
```

---

</SwmSnippet>

# Tasklist Form Methods

Tasklist Form Directive Methods

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/form/directives/cam-tasklist-form.js" line="235">

---

## Complete Method

The `complete` method is used to mark a task as complete. It sets the `completeInProgress` flag to true, indicating that the completion process is ongoing.

```javascript
        var complete = ($scope.complete = function() {
          $scope.completeInProgress = true;
          $scope.completionHandler(completionCallback);
        });
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/tasklist/client/scripts/form/directives/cam-tasklist-form.js" line="266">

---

## Save Method

The `save` method is used to save the current state of the form. It calls the `saveHandler` function, which should be defined elsewhere in the application.

```javascript
        $scope.save = function(evt) {
          $scope.saveHandler(evt);
        };
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
