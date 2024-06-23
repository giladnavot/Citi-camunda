---
title: Understanding Cockpit Client Scripts
---
Cockpit Client Scripts in the Citi-camunda repository refer to the JavaScript files that are responsible for the client-side functionality of the Camunda Cockpit. These scripts handle tasks such as setting up the development environment, importing necessary libraries and modules, initializing the AngularJS application, and defining various AngularJS components such as services, directives, and controllers. They also include scripts for handling specific features like navigation, variable manipulation, and process diagram visualization. The scripts are organized into different directories based on their functionality, such as services, directives, and components.

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/camunda-cockpit-ui.js" line="1">

---

# Cockpit Client Scripts Structure

This is the main script file for the Cockpit UI. It sets up the development environment, requires necessary dependencies, initializes the AngularJS application for the Cockpit, and exports functions for initializing plugins and exposing packages.

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

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/navigation/main.js" line="1">

---

# Navigation Scripts

This script is responsible for managing navigation in the Cockpit. It defines a navigation module and a controller for handling header views.

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

var angular = require('camunda-commons-ui/vendor/angular'),
  camHeaderViewsCtrl = require('./controllers/cam-header-views-ctrl');
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/directives/main.js" line="1">

---

# Directives Scripts

This script is responsible for managing directives in the Cockpit. It defines a directives module and registers various directives for handling different UI components and functionalities.

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

var angular = require('camunda-commons-ui/vendor/angular'),
  breadcrumbs = require('./../../../../common/scripts/directives/breadcrumbs'),
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/services/main.js" line="1">

---

# Services Scripts

This script is responsible for managing services in the Cockpit. It defines a services module and registers various services for handling different functionalities.

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

var angular = require('camunda-commons-ui/vendor/angular'),
  transform = require('./transform'),
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
