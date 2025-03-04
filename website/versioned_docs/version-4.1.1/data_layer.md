---
title: DataLayer
sidebar_label: DataLayer
copyright: (C) 2007-2018 GoodData Corporation
id: version-4.1.1-data_layer
original_id: data_layer
---

This is the 3.0.0 version! In sync with the live doc.

DataLayer is mostly intended for addressing advanced use cases \(for example, writing advanced custom components\).

For the majority of use casesinvolving custom visualizations, we recommend that you try using the [Execute component](50_custom__component.md) first. If it does not meet your requirements, you can always go back to using DataLayer.

DataLayer obtains data from your workspace either using AFM+ResultSpec or Visualization URI. You can use that data, for example, to create a visualization that is not a part of the GoodData UI SDK.

![Data layer](assets/data_layer_diagram.png)

## How to Use DataLayer

In the following code sample, replace the parameter placeholders with your values, and then execute the code.

The parameter placeholders are:

* &lt; measure-identifier &gt;
* &lt; workspace-id &gt;

For more information about what AFM and resultSpec are, see [AFM](afm) and [Result Specification \(resultSpec\)](50_custom__result.md).

Though you can use either object URIs or object identifiers, we recommend that you use the **object identifiers**, which are consistent across your domain regardless of the GoodData workspace they live in. That is, an object used in any workspace within your domainwould have the_same_object identifier in_any_of those workspaces\). To get a list ofcatalog items and date datasets from a GoodData workspace in form of a JavaScript object, use [gdc-catalog-export](02_start__catalog_export.md).

```javascript
/*
Importing GoodData DataLayer dependencies
and GoodData Java Script SDK
(https://github.com/gooddata/gooddata-js)
*/
import { DataTable, ExecuteAfmAdapter } from '@gooddata/data-layer';
import * as sdk from 'gooddata';
 
/*
Defining AFMs and (optionally) resultSpec
*/
const afm = {
    measures: [
        {
            localIdentifier: 'measure1', // An identifier which will be referenced in the execution results
            definition: {
                measure: {
                    item: {
                        identifier: '<measure-identifier>'
                    }
                }
            }
        }
    ]
};

const resultSpec = {};

/*
Initializing the Adapter object
The Adapter converts the AFMs for the backend to process.
*/
const adapter = new ExecuteAfmAdapter(sdk, '<workspace-id>');
 
/*
Initializing the Data Table object
The Data Table processes the AFMs and resultSpec and returns raw data from the backend.
*/
const dataTable = new DataTable(adapter);
 
/*
Adding callbacks that will be called once the data is ready or if the execution fails.
*/
dataTable.onData((data) => console.log(data));
dataTable.onError((err) => console.error(err));
 
/*
Executing the defined AFMs and resultSpec
*/
dataTable.getData(afm, resultSpec);
```
