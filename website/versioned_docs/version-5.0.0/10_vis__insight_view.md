---
title: Visualization
sidebar_label: Visualization
copyright: (C) 2007-2018 GoodData Corporation
id: version-5.0.0-visualization_component
original_id: visualization_component
---

Visualization is a generic component that renders a chart according to the provided URI or identifier. It can render a table or any type of chart.

## Structure

```javascript
import '@gooddata/react-components/styles/css/main.css';
import { Visualization } from '@gooddata/react-components';
 
<div style={{ height: 400, width: 600 }}>
    <Visualization
        projectId="<workspace-id>"
        identifier="<visualization-identifier>"
        config={<chart-config>}
    />
</div>
```

```javascript
import '@gooddata/react-components/styles/css/main.css';
import { Visualization } from '@gooddata/react-components';

<div style={{ height: 400, width: 600 }}>
    <Visualization
        projectId="<workspace-id>"
        uri="<visualization-uri>"
        config={<chart-config>}
    />
</div>
```

## Example

<!-- This example uses data from the GoodSales // TODO REMOVE! demo workspace. For testing purposes, you can use this snippet as is. -->

```javascript
import '@gooddata/react-components/styles/css/main.css';
import { Visualization } from '@gooddata/react-components';
 
<div style={{ height: 400, width: 600 }}>
    <Visualization
        identifier="aoJqpe5Ib4mO"
        projectId="la84vcyhrq8jwbu4wpipw66q2sqeb923"
        config={{
            colors: ['rgb(195, 49, 73)', 'rgb(168, 194, 86)'],
            legend: {
                enabled: true,
                position: 'bottom'
            }
        }}
    />
</div>
```

## Properties

| Name | Required? | Type | Description |
| :--- | :--- | :--- | :--- |
| projectId | true | string | The workspace ID |
| uri | false | string | The URI of the visualization to be rendered. Can be omitted if the visualization identifier is present. |
| identifier | false | string | The identifier of the visualization to be rendered. Can be omitted if the visualization URI is present. |
| locale | false | string | The localization of the visualization. Defaults to `en-US`. For other languages, see the [full list of available localizations](https://github.com/gooddata/gooddata-react-components/tree/master/src/translations). |
| config  | false | ChartConfig | The chart configuration |
| filters | false | FilterItem\[\] | The list of filters to be applied to the visualization |
| drillableItems | false | DrillableItem\[\] | The drilling configuration. See [DrillableItems](15_props__drillable_item.md).|
| onFiredDrillEvent | false | [onFiredDrillEvent()](15_props__on_drill.md) | The drilling event catcher. Called when drilling happens. |
| uriResolver | false | function | A custom method for querying URIs for identifiers. Defaults to the standard Gooddata SDK. `getObjectUri()`. |
| onError | false | function | A custom error handler. Called with the argument containing the state and original error message, for example: `{ status:ErrorStates.BAD_REQUEST,error: {...} }`. See the [full list of error states](https://github.com/gooddata/gooddata-react-components/blob/master/src/constants/errorStates.ts). Defaults to `console.error`. |
| onLoadingChanged | false | function | A custom loading handler. Called when a visualization changes to/from the loading state. Called with the argument denoting a valid state, for example: `{ isLoading:false}`. |
| onLegendReady | false | [onLegendReady()](15_props__on_legend_ready.md) | The legend ready callback. Called when the visualization series are ready to render. Can be used for rendering a custom legend. |
