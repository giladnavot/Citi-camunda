---
title: Getting started
---
This document will cover the following topics:

1. The purpose and main functionalities of the Citi-camunda repo.
2. Important documents to read from the repo.
3. How to run and debug the main parts of the repo.
4. How to contribute to the repo.

# Purpose and Main Functionalities of the Citi-camunda Repo

The Citi-camunda repo is an open-source platform for workflow and process automation. It provides a native BPMN 2.0 process engine that runs inside the Java Virtual Machine and can be embedded inside any Java application and any Runtime Container. It includes components for process implementation and execution, process design, process operations, and human task management. The platform is highly integrable and embeddable.

# Important Documents in the Repo

The two main documents in the repo are the `README.md` and `CONTRIBUTING.md` files. The `README.md` file provides an overview of the repo, its components, and how to get started. The `CONTRIBUTING.md` file provides guidelines on how to contribute to the project, including ways to contribute, how to build from source, create a pull request, and the review process.

# Running and Debugging the Repo

The `pom.xml` file is a Project Object Model (POM) file for Maven. It contains information about the project and configuration details used by Maven to build the project. To build the codebase from source, add the provided XML to your Maven `settings.xml`. Then, you can build the entire repository by running `mvn clean install` in the root directory. This will build all submodules and execute unit tests. You can also restrict the build to just the module you are changing by running the same command in the corresponding directory.

# Contributing to the Repo

To contribute to the repo, you can participate in the forum, file bugs or feature requests, or contribute code. When contributing code, select a ticket you'd like to implement, tell the team in the ticket comments or in the forum that you want to work on the ticket, check your code changes against the contribution checklist, and create a pull request. Before submitting your pull request for code review, please go through the contribution checklist.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="getting-started"><sup>Powered by [Swimm](/)</sup></SwmMeta>
