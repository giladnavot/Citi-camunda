---
title: Introduction to Admin UI
---
The Admin UI in Citi-camunda is a user interface that allows administrators to manage the system. It provides functionalities such as user management, system settings, and plugin management. The Admin UI is built using AngularJS and it interacts with the backend through the Camunda API. It is designed to be highly customizable with the ability to add plugins for additional functionalities.

<SwmSnippet path="/webapps/frontend/ui/admin/client/scripts/pages/users.html" line="1">

---

# User Management

This file defines the HTML structure of the user management page in the Admin UI. It includes a table that lists all users and their details, and provides links for editing each user's information.

```html
<!-- # CE - camunda-bpm-webapp/ui/admin/client/scripts/pages/users.html -->
<section ng-cloak>
  <!-- <aside></aside> -->
  <div class="section-content">
    <header class="row">
      <div class="col-xs-8">
        <h3>{{ 'USERS_LIST_OF_USERS' | translate }}</h3>
      </div>
      <div class="col-xs-4 text-right">
        <a class="btn btn-default"
           href="#/user-create">
          {{ 'USERS_ADD_USER' | translate }}
          <span class="glyphicon glyphicon-plus-sign"></span>
        </a>
      </div>
    </header>

    <div cam-searchable-area
         config="searchConfig"
         on-search-change="onSearchChange(query, pages)"
         loading-state="loadingState"
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/client/scripts/pages/system.js" line="54">

---

# System Settings

This file defines the functionality for the system settings page in the Admin UI. It fetches the system settings providers and allows administrators to interact with them.

```javascript
    $scope.systemSettingsProviders = Views.getProviders({
      component: 'admin.system'
    }).map(function(plugin) {
      if (angular.isArray(plugin.access)) {
        var fn = $injector.invoke(plugin.access);

        fn(function(err, access) {
          if (err) {
            throw err;
          }

          plugin.accessible = access;
        });
      } else {
        plugin.accessible = true;
      }

      return plugin;
    });

    var selectedProviderId = $routeParams.section;
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/client/scripts/camunda-admin-ui.js" line="1">

---

# Admin UI Initialization

This file is responsible for initializing the Admin UI. It sets up the AngularJS module for the application, configures routes and providers, and initializes various services and controllers.

```javascript
/*
 * Copyright Camunda Services GmbH and/or licensed to Camunda Services GmbH
 * under one or more contributor license agreements. See the NOTICE file
 * distributed with this work for additional information regarding copyright
 * ownership. Camunda licenses this file to you under the Apache License,
 * Version 2.0; you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *     http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */

'use strict';

if (process.env.NODE_ENV === 'development') {
  require('../../../common/scripts/util/dev-setup').setupDev();
```

---

</SwmSnippet>

# Admin UI Functions

In this section, we will delve into the main functions of the Admin UI, focusing on user management, group management, tenant management, and authorization.

<SwmSnippet path="/webapps/frontend/ui/admin/client/scripts/pages/users.js" line="1">

---

## User Management

The `users.js` file contains the main functions for user management in the Admin UI. It includes functions for listing users, creating new users, and editing user details.

```javascript
/*
 * Copyright Camunda Services GmbH and/or licensed to Camunda Services GmbH
 * under one or more contributor license agreements. See the NOTICE file
 * distributed with this work for additional information regarding copyright
 * ownership. Camunda licenses this file to you under the Apache License,
 * Version 2.0; you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *     http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */

'use strict';

var template = require('./users.html?raw');
var searchConfig = require('./users-search-plugin-config.json');
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/client/scripts/pages/groups.js" line="1">

---

## Group Management

The `groups.js` file contains the main functions for group management in the Admin UI. It includes functions for listing groups, creating new groups, and editing group details.

```javascript
/*
 * Copyright Camunda Services GmbH and/or licensed to Camunda Services GmbH
 * under one or more contributor license agreements. See the NOTICE file
 * distributed with this work for additional information regarding copyright
 * ownership. Camunda licenses this file to you under the Apache License,
 * Version 2.0; you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *     http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */

'use strict';

var template = require('./groups.html?raw');
var searchConfig = require('./groups-search-plugin-config.json');
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/admin/client/scripts/pages/tenants.js" line="1">

---

## Tenant Management

The `tenants.js` file contains the main functions for tenant management in the Admin UI. It includes functions for listing tenants, creating new tenants, and editing tenant details.

```javascript
/*
 * Copyright Camunda Services GmbH and/or licensed to Camunda Services GmbH
 * under one or more contributor license agreements. See the NOTICE file
 * distributed with this work for additional information regarding copyright
 * ownership. Camunda licenses this file to you under the Apache License,
 * Version 2.0; you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *     http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */

'use strict';

var template = require('./tenants.html?raw');
var searchConfig = require('./tenants-search-plugin-config.json');
```

---

</SwmSnippet>

## Authorization

The `authorization.js` file contains the main functions for managing authorizations in the Admin UI. It includes functions for listing authorizations, creating new authorizations, and deleting authorizations.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
