---
title: Basic Concepts of Incident Handling
---
An Incident in the context of the Citi-camunda repository refers to an event that disrupts normal workflow execution. Incidents are typically created when an error occurs during the execution of a process instance. They provide detailed information about the error, such as the error message and the stack trace, which can be used for troubleshooting and error handling.

# Incident Creation

This is where an incident is created when an exception is thrown during the execution of a process instance. The `handleIncident` method takes in the process instance and the exception, and creates a new incident with the relevant information.

# Incident Resolution

Once the error has been fixed, the incident can be resolved using the `resolveIncident` method. This method takes in the process instance and the incident, and resolves the incident.

# Incident Functionality

This section will cover the main functions related to the Incident functionality in the Citi-camunda project.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/incident/IncidentHandler.java" line="1">

---

## IncidentHandler

The `IncidentHandler` class is responsible for handling incidents in the system. It provides methods for creating, deleting, and resolving incidents.

```java
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
package org.camunda.bpm.engine.impl.incident;

import org.camunda.bpm.engine.runtime.Incident;

/**
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/management/IncidentStatistics.java" line="1">

---

## IncidentStatistics

The `IncidentStatistics` class provides statistical data about incidents. It includes methods for retrieving the number of incidents, their types, and their states.

```java
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
package org.camunda.bpm.engine.management;

/**
 * Represents a statistic which the aggregate number of incidents to
 * the corresponding incident type. 
```

---

</SwmSnippet>

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/runtime/Incident.java" line="1">

---

## Incident

The `Incident` class represents an individual incident in the system. It includes methods for retrieving and setting incident properties such as id, message, and process instance id.

```java
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
package org.camunda.bpm.engine.runtime;

import java.util.Date;

/**
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
