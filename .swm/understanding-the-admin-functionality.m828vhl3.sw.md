---
title: Understanding the Admin Functionality
---
In the Citi-camunda repository, 'Admin' refers to a key part of the system that manages and controls various aspects of the application. It is responsible for system settings, user management, and other administrative tasks. The 'Admin' functionality is implemented through various scripts and modules, such as 'system.js', 'admin-setup.js', and 'admin-user-spec.js'. These scripts handle tasks like fetching system settings providers, setting up new admin users, and running tests for admin users. The 'Admin' is also a component in the application's UI, as seen in 'camunda-admin-ui.js' and 'camunda-admin-bootstrap.js'.

<SwmSnippet path="/webapps/frontend/ui/admin/tests/specs/admin-user-spec.js" line="27">

---

# Admin User Management

This code snippet is part of a test suite for the 'Admin' user functionality. It includes tests for validating the admin setup page, entering a new admin profile, and logging in as a new admin.

```javascript
describe('Admin admin-user Spec', function() {
  before(function() {
    return testHelper(setupFile.setup1);
  });

  it('should validate admin setup page', function() {
    // when
    usersPage.navigateToWebapp('Admin');

    // then
    testHelper.expectStringEqual(usersPage.adminUserSetup.boxHeader(), 'SETUP');
    expect(
      usersPage.adminUserSetup.createNewAdminButton().isEnabled()
    ).to.eventually.eql(false);
  });

  it('should enter new admin profile', function() {
    // when
    usersPage.adminUserSetup.userIdInput('Admin');
    usersPage.adminUserSetup.passwordInput('admin123');
    usersPage.adminUserSetup.passwordRepeatInput('admin123');
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/client/scripts/pages/system.js" line="54">

---

# Admin System Settings

This code snippet shows how the 'Admin' functionality is used to manage system settings. The 'component' property is set to 'admin.system', indicating that this part of the code is related to the system settings in the admin functionality.

```javascript
    $scope.systemSettingsProviders = Views.getProviders({
      component: 'admin.system'
    }).map(function(plugin) {
      if (angular.isArray(plugin.access)) {
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/plugins/adminPlugins.js" line="25">

---

# Admin Plugin Management

This code snippet shows the 'Admin' functionality being used to manage plugins. The 'admin.plugin.adminPlugins' module is being exported, indicating that this part of the code is related to the plugin management in the admin functionality.

```javascript
export default angular.module('admin.plugin.adminPlugins', [base.name]);
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
