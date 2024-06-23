---
title: Introduction to Cockpit Client Styles
---
Cockpit Client Styles in the Citi-camunda project refer to the CSS and LESS stylesheets that are used to style the Camunda Cockpit, a web-based interface for monitoring and managing workflows. These styles are organized into different files and directories based on their purpose. For instance, the `styles-components.less` file imports styles from various other files and applies some general styles. The `styles.less` file, on the other hand, imports styles from the `styles-components.less` file and other widget-specific styles. There are also directories for styles specific to directives and pages. Each of these files contributes to the overall look and feel of the Camunda Cockpit.

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/styles/styles-components.less" line="1">

---

# Organizing Styles

This file imports various style files related to different components of the application. For example, styles for pages, directives, and scripts are imported from their respective directories.

```less
// use `reference` to avoid duplicate bootstrap styles
// as they are already available in other compiled CSS
@import (reference) '~camunda-commons-ui/resources/less/shared/bootstrap.less';
@import './_app-variables.less';
@import '~camunda-commons-ui/resources/less/shared/_mixins';

/* ---------------------------------------------------------------- */

.monospaced {
  font-family: @font-family-monospace;
}

@import 'pages/repository';
@import '~ui/common/styles/pages/dashboard.less';
@import './../scripts/pages/dashboard';
@import './../scripts/components/callActivityOverlays/styles';
@import '~ui/cockpit/client/scripts/pages/processes';
@import 'pages/process-instance';
@import 'pages/batch';
@import '~ui/cockpit/client/scripts/pages/tasks';
@import 'directives/process-diagram';
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/styles/styles.less" line="1">

---

# Main Style File

This is the main style file that imports various other style files including the application variables, common styles, and widget styles. It also imports styles for directives and other components of the application.

```less
@import './_app-variables.less';
@import '~ui/common/styles/cam-webapps-common.less';
@import "~ui/common/styles/app-splash";

/* ---------------------------------------------------------------- */

@import '~camunda-commons-ui/lib/widgets/variable/cam-widget-variable';
@import '~camunda-commons-ui/lib/widgets/variables-table/cam-widget-variables-table';
@import '~camunda-commons-ui/lib/widgets/annotation/cam-annotation-edit';
@import '~camunda-commons-ui/lib/widgets/bpmn-viewer/cam-widget-bpmn-viewer';
@import '~camunda-commons-ui/lib/widgets/cmmn-viewer/cam-widget-cmmn-viewer';
@import '~ui/common/styles/directives/notifications-panel';
@import '~ui/common/styles/directives/cam-breadcrumbs-panel';
@import '~ui/common/styles/directives/pagination';
@import '~ui/common/styles/directives/cam-in-place-text-field';
@import 'directives/diagram-statistics-loader';
@import 'directives/cam-cockpit-resource-content';
@import 'directives/sortable-table-head';
@import 'directives/change-version';
@import 'directives/textarea';
@import '~camunda-commons-ui/lib/widgets/inline-field/cam-widget-inline-field';
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/styles/directives/process-diagram.less" line="1">

---

# Directive Styles

Each directive has its own style file. For example, 'process-diagram.less' contains styles specific to the process diagram directive.

```less
[process-diagram] {
  overflow: hidden;
  height: 100%;
  position: relative;

  /* disable text selection */
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/styles/pages/repository.less" line="1">

---

# Page Styles

Each page has its own style file. For example, 'repository.less' contains styles specific to the repository page.

```less
@import '~ui/common/styles/_three-cols-layout.less';

.three-cols-layout-base();
.three-cols-layout-handheld();
.three-cols-layout-colors(@column-left-bg, @column-center-bg, @column-right-bg);
.three-cols-layout-header();

// S
@media (min-width: @screen-sm-min) and (max-width: @screen-sm-max) {
  .three-cols-layout(200px, 200px * 1.618);
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/styles/ctn.less" line="1">

---

# Custom Styles

This file contains custom styles used across the application. It defines styles for various elements like main container, view, header, content container, sidebar, toolbar, etc.

```less
@ctn-sidebar-width: 280px;
@ctn-toolbar-width: 56px;
@ctn-content-bottom-height: 350px;
@ctn-resize-handle-width: 5px;

.ctn-main {
  position: absolute;
  top: @header-height + @ce-banner-height;
  bottom: @footer-height;
  left: 0;
  right: 0;
  overflow: hidden;
  background-color: @custom-gray-lighter;
}

.ctn-view {
  overflow: auto;
  max-height: ~"calc(100vh - (@{header-height} + @{footer-height}))";
}

.ctn-wrapper {
```

---

</SwmSnippet>

<SwmSnippet path="/webapps/frontend/ui/cockpit/client/styles/filters.less" line="1">

---

# Filter Styles

This file contains styles for filters used in the application. It defines styles for filter elements like alert, search, removable input, etc.

```less
.filters {
  &.tab-content {
    padding: 10px;
  }

  ul {
    margin-bottom: 0;
  }

  h5 {
    margin: 0 0 5px 0;
    font-weight: 700;
  }

  .footer {
    border-top: solid 1px @filters-color;
    padding-top: 8px;
  }

  .dropdown-menu {
    min-width: 50px;
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
