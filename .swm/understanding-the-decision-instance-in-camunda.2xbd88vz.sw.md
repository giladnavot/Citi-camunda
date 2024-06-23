---
title: Understanding the Decision Instance in Camunda
---
A Decision Instance in the Citi-camunda project refers to a specific execution of a decision definition. It is the result of evaluating a decision, such as a business rule, within the Camunda BPMN process engine. The decision instance contains the input and output variables used and produced during the evaluation.

The decision instance is represented in the frontend of the application, specifically within the Cockpit plugin. The files in the 'decisionInstance' directory handle the display of the decision instance's details, including input and output variables.

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/decisionList/app/views/decisionInstance/outputTable.js" line="6">

---

# Decision Instance Execution

This file is part of the decision instance execution process. It handles the output table of the decision instance, which shows the results of the decision.

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

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/decisionList/app/views/decisionInstance/realInput.js" line="6">

---

# Decision Instance Inputs

This file handles the real inputs of the decision instance. These inputs are used in the decision-making process.

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

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/decisionList/app/views/decisionInstance/highlightRules.js" line="6">

---

# Decision Instance Rules

This file highlights the rules of the decision instance. These rules are used in the decision-making process.

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

# Decision Instance Functions

This section will delve into the functions of the Decision Instance, focusing on how it handles input and output variables.

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/decisionList/app/views/decisionInstance/inputTable.js" line="35">

---

## Input Variable Handling

The input variable handling function maps the inputs of the decision instance into a format that can be used in the application. It checks the type of each variable and formats it accordingly. For instance, if the variable type is 'Date', it converts the value into a Date object.

```javascript
          $scope.loadingState =
            $scope.decisionInstance.inputs.length > 0 ? 'LOADED' : 'EMPTY';
          $scope.variables = $scope.decisionInstance.inputs.map(function(
            variable
          ) {
            const variableValue =
              variable.type === 'Date'
                ? new Date(variable.value)
                : variable.value;

            return {
              variable: {
                type: variable.type,
                value: variableValue,
                name: variable.clauseName || variable.clauseId,
                valueInfo: variable.valueInfo
              }
            };
          });
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/plugins/decisionList/app/views/decisionInstance/outputTable.js" line="35">

---

## Output Variable Handling

The output variable handling function maps the outputs of the decision instance in a similar way to the input handling function. It also checks the type of each variable and formats it accordingly. The output variables are then used in other parts of the application.

```javascript
          $scope.variables = $scope.decisionInstance.outputs.map(function(
            variable
          ) {
            const variableValue =
              variable.type === 'Date'
                ? new Date(variable.value)
                : variable.value;
            return {
              variable: {
                type: variable.type,
                value: variableValue,
                name:
                  variable.clauseName ||
                  variable.clauseId ||
                  variable.variableName,
                valueInfo: variable.valueInfo
              }
            };
          });
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
