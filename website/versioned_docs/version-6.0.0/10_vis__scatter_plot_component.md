---
title: Scatter Plot
sidebar_label: Scatter Plot
copyright: (C) 2007-2018 GoodData Corporation
id: version-6.0.0-scatter_plot_component
original_id: scatter_plot_component
---

Scatter plot shows data as points using Cartesian coordinates. Scatter plots typically have a minimum of two measures, one for the X-axis and the other for the Y-axis, and one attribute, which determines the meaning of each data point.
Scatter plots are useful for analyzing trends between two measures or for tracking the magnitude of two measures from the same chart.

![Scatter Plot Component](assets/scatter_plot.png "Scatter Plot Component")

## Structure

```jsx
import '@gooddata/react-components/styles/css/main.css';
import { ScatterPlot } from '@gooddata/react-components';

<ScatterPlot
    projectId={<workspace-id>}
    xAxisMeasure={<measure>}
    yAxisMeasure={<measure>}
    attribute={<attribute>}
    config={<chart-config>}
    sdk={<sdk>}
    …
/>
```

## Example

```jsx
import '@gooddata/react-components/styles/css/main.css';
import { ScatterPlot } from '@gooddata/react-components';

const measures = [
    {
        measure: {
            localIdentifier: 'franchiseFeesIdentifier',
            definition: {
                measureDefinition: {
                    item: {
                        identifier: franchiseFeesIdentifier
                    }
                }
            },
            format: '#,##0'
        }
    },
    {
        measure: {
            localIdentifier: 'franchisedSalesIdentifier',
            definition: {
                measureDefinition: {
                    item: {
                        identifier: franchisedSalesIdentifier
                    }
                }
            },
            format: '#,##0'
        }
    }
];

const attribute = {
    visualizationAttribute: {
        displayForm: {
            identifier: monthDateIdentifier
        },
        localIdentifier: 'month'
    }
};

<div style={{ height: 300 }}>
    <ScatterPlot
        projectId={workspaceId}
        xAxisMeasure={measures[0]}
        yAxisMeasure={measures[1]}
        attribute={attribute}
    />
</div>
```

## Properties

| Name | Required? | Type | Description |
| :--- | :--- | :--- | :--- |
| projectId | true | string | The workspace ID |
| xAxisMeasure | false | [Measure](50_custom__execution.md#measure) | A measure definition (at least one of xAxisMeasure or yAxisMeasure must be provided for the scatter plot to render properly) |
| yAxisMeasure | false | [Measure](50_custom__execution.md#measure) | A measure definition (at least one of xAxisMeasure or yAxisMeasure must be provided for the scatter plot to render properly) |
| attribute | false | [Attribute](50_custom__execution.md#attribute) | An attribute definition |
| filters | false | [Filter[]](30_tips__filter_visual_components.md) | An array of filter definitions |
| sortBy | false | [SortItem[]](50_custom__result.md#sorting) | An array of sort definitions |
| config | false | [ChartConfig](15_props__chart_config.md) | The chart configuration object |
| locale | false | string | The localization of the chart. Defaults to `en-US`. For other languages, see the [full list of available localizations](https://github.com/gooddata/gooddata-react-components/tree/master/src/translations). |
| drillableItems | false | [DrillableItem[]](15_props__drillable_item.md) | An array of points and attribute values to be drillable. |
| sdk | false | SDK | A configuration object where you can define a custom domain and other API options |
| ErrorComponent | false | Component | A component to be rendered if this component is in error state |
| LoadingComponent | false | Component | A component to be rendered if this component is in loading state |
| onError | false | Function | A callback when component updates its error state |
| onLoadingChanged | false | Function | A callback when component updates its loading state |

<!-- These internals are intentionally undocumented
| afterRender | false | Function | A callback after component is rendered |
| dataSource | false | DataSource class | A class that is used to resolve AFM |
| environment | false | string | An Internal property that changes behaviour in Analytical Designer and KPI Dashboards |
| height | false | number | Height of the component in pixels |
| onFiredDrillEvent | false | Function | A callback after drill event was emitted |
| onLoadingFinish | false | Function | A callback when component ends loading |
| pushData | false | Function | A callback after AFM is resolved |
| visualizationProperties | false | {} | The chart configuration object |
-->

The following example shows the supported `config` structure with sample values. To see descriptions of individual options, see [ChartConfig section](15_props__chart_config.md).
```javascript
{
    colors: ['rgb(195, 49, 73)', 'rgb(168, 194, 86)'],
    xaxis: {
        visible: true,
        labelsEnabled: true,
        rotation: 'auto',
        min: '20',
        max: '30'
    },
    yaxis: {
        visible: true,
        labelsEnabled: true,
        rotation: 'auto',
        min: '40',
        max: '50'
    },
    dataLabels: {
        visible: 'auto'
    },
    grid: {
        enabled: true
    }
    separators: {
        thousand: ',',
        decimal: '.'
    }
}
```
