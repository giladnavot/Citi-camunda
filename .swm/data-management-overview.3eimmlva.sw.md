---
title: Data Management Overview
---
Data Management in Citi-camunda refers to the handling and organization of data in a structured way. It involves the use of classes and methods to create, read, update, and delete data. This is achieved through various classes and methods in the 'variable' directory, such as 'ClientValues.java', 'XmlValue.java', 'JsonValue.java', and others. These classes provide the functionality to manage different types of data values within the application.

## Value Mappers

Value mappers are used to convert different data types. For example, `IntegerValueMapper` is used to handle integer values, `BooleanValueMapper` for boolean values, and so on. Each mapper is responsible for a specific data type.

## Data Formats

Data formats manage the format of the data. For instance, `JacksonJsonDataFormat` is used for handling JSON data, `DomXmlDataFormat` for XML data, and so on. Each data format class is responsible for a specific data format.

&nbsp;

*This is an auto-generated document by Swimm AI 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBQ2l0aS1jYW11bmRhJTNBJTNBZ2lsYWRuYXZvdA==" repo-name="Citi-camunda" doc-type="overview"><sup>Powered by [Swimm](/)</sup></SwmMeta>
