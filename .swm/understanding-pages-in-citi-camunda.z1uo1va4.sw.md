---
title: Understanding Pages in Citi-camunda
---
In Citi-camunda, 'Pages' refers to a directory in the codebase that contains scripts for different pages of the application. These scripts define the data and functionality for each page. For instance, the 'processInstance.js' and 'processDefinition.js' files contain a 'pageData' property, which is used to store and manage data specific to the process instance and process definition pages respectively.

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/pages/dashboard.js" line="6">

---

# Dashboard Page

This is the JavaScript file for the Dashboard page. It contains the logic for displaying and interacting with the dashboard view in the application.

```javascript
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
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/pages/tasks.js" line="6">

---

# Tasks Page

This is the JavaScript file for the Tasks page. It contains the logic for displaying and interacting with the tasks view in the application.

```javascript
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
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/pages/processDefinition.js" line="6">

---

# Process Definitions Page

This is the JavaScript file for the Process Definitions page. It contains the logic for displaying and interacting with the process definitions view in the application.

```javascript
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
```

---

</SwmSnippet>

# Functions of Pages

The functions of Pages are primarily involved in managing the user interface's breadcrumbs and page data.

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/pages/processDefinition.js" line="427">

---

## page.breadcrumbsClear

The `page.breadcrumbsClear` function is used to clear the breadcrumbs in the user interface.

```javascript
        page.breadcrumbsClear();

        page.breadcrumbsAdd({
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/pages/processDefinition.js" line="434">

---

## page.breadcrumbsAdd

The `page.breadcrumbsAdd` function is used to add new breadcrumbs to the user interface.

```javascript
        if (parent) {
          page.breadcrumbsAdd({
            type: 'processDefinition',
            label: parent.name || parent.id.slice(0, 8) + '…',
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/pages/processInstance.js" line="718">

---

## pageData

The `pageData` property is used to store and manage data related to the current page.

```javascript
      processData: processData,
      filter: $scope.filter,
      pageData: pageData
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
