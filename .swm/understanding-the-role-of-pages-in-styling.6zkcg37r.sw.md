---
title: Understanding the Role of Pages in Styling
---
In Citi-camunda, 'Pages' refers to a directory located at 'webapps/frontend/ui/cockpit/client/styles/pages'. This directory contains style files for different pages of the application. Each file corresponds to a specific page and defines the look and feel of that page. For example, 'repository.less' contains styles for the repository page, 'process-instance.less' for the process instance page, and 'batch.less' for the batch page.

# Page Structure

This is an example of a typical page in the application. It includes a header, a main content area, and a footer. The header typically contains navigation controls, the main content area contains the bulk of the page's content, and the footer contains additional information or controls.

# Page Navigation

This is where the application's routing is defined. It determines which page is displayed based on the current URL. This allows users to navigate between pages by changing the URL.

# The 'Page' Class

The 'Page' class is a fundamental part of the application, providing the structure and functionality of a page.

<SwmSnippet path="/engine/src/main/java/org/camunda/bpm/engine/impl/Page.java" line="1">

---

## The 'Page' Class

The 'Page' class represents a page in the application. It provides methods for managing the page's properties and behavior. This includes methods for setting and getting the page's first result and max results, which are used for pagination.

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
package org.camunda.bpm.engine.impl;


/**
 * holds the parameters of a page (partial result) for a query. 
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
