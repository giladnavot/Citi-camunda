---
title: Understanding Components in Citi-camunda
---
Components in Citi-camunda are modular pieces of code that encapsulate specific functionality within the application. They are primarily used in the frontend of the application, specifically within the cockpit client. These components include dialogues for variable inspection, upload, and addition, as well as overlays for call activities. Each component is typically composed of a JavaScript file defining its behavior and an HTML file defining its structure.

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/components/variables/variable-inspect-dialog.js" line="6">

---

# Variable Components

This is an example of a component that provides a dialog for inspecting variables. It is a self-contained unit of code that can be reused wherever a variable inspection dialog is needed.

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

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/components/callActivityOverlays/callActivityOverlay.js" line="6">

---

# Call Activity Overlays Components

This is an example of a component that provides an overlay for call activities. It is a self-contained unit of code that can be reused wherever a call activity overlay is needed.

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

# Variable Endpoints

Variable Handling Endpoints

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/components/variables/variable-inspect-dialog.js" line="164">

---

## Uri.appUri(basePath)

This endpoint is used to update the value of a variable. The `basePath` is a parameter that determines the specific variable to be updated. The new value of the variable is sent in the request body.

```javascript
      $http({
        method: 'PUT',
        url: Uri.appUri(basePath),
        data: variableUpdate
      })
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/scripts/components/variables/variable-upload-dialog.js" line="100">

---

## Uri.appUri(basePath + '/data')

This endpoint is used to upload a new value for a variable. The `basePath` is a parameter that determines the specific variable to be updated. The new value is sent as form data in the request body.

```javascript
      $http
        .post(Uri.appUri(basePath + '/data'), fd, {
          transformRequest: angular.identity,
          headers: {'Content-Type': undefined},
          uploadEventHandlers: {
            progress: uploadProgress
          }
        })
        .then(uploadComplete)
        .catch(uploadFailed);
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
