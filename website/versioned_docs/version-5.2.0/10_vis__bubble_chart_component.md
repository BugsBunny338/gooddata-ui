---
title: Bubble Chart
sidebar_label: Bubble Chart
copyright: (C) 2007-2018 GoodData Corporation
id: version-5.2.0-bubble_chart_component
original_id: bubble_chart_component
---

Bubble chart shows data as bubbles using Cartesian coordinates.
Bubble charts typically have three measures, one for the X-axis, one for the Y-axis, and one that determines the size of each bubble.
The data is sliced by an attribute, with each bubble (an attribute item) noted with a different color.

![Bubble Chart Component](assets/bubble_chart.png "Bubble Chart Component")

## Structure

```jsx
import '@gooddata/react-components/styles/css/main.css';
import { BubbleChart } from '@gooddata/react-components';

<BubbleChart
    projectId={<workspace-id>}
    xAxisMeasure={<measure>}
    yAxisMeasure={<measure>}
    size={<measure>}
    viewBy={<attribute>}
    config={<chart-config>}
    sdk={<sdk>}
    …
/>
```

## Example

```jsx
import '@gooddata/react-components/styles/css/main.css';
import { BubbleChart } from '@gooddata/react-components';

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
    },
    {
        measure: {
            localIdentifier: 'averageCheckSizeByServer',
            definition: {
                measureDefinition: {
                    item: {
                        identifier: averageCheckSizeByServer
                    }
                }
            }
        }
    }
];

const viewBy = {
    visualizationAttribute: {
        displayForm: {
            identifier: locationResortIdentifier
        },
        localIdentifier: 'location_resort'
    }
};

<div style={{ height: 300 }}>
    <BubbleChart
        projectId={workspaceId}
        xAxisMeasure={measures[0]}
        yAxisMeasure={measures[1]}
        size={measures[2]}
        viewBy={viewBy}
    />
</div>
```

## Properties

| Name | Required? | Type | Description |
| :--- | :--- | :--- | :--- |
| projectId | false | string | The workspace ID |
| xAxisMeasure | false | [Measure](50_custom__execution.md#measure) | A measure definition (at least one of xAxisMeasure or yAxisMeasure must be provided for the bubble chart to render properly) |
| yAxisMeasure | false | [Measure](50_custom__execution.md#measure) | A measure definition (at least one of xAxisMeasure or yAxisMeasure must be provided for the bubble chart to render properly) |
| size | false | [Measure](50_custom__execution.md#measure) | A measure definition that determines the size of the bubbles |
| viewBy | false | [Attribute](50_custom__execution.md#attribute) | An attribute definition |
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
| pushData | false | Function | A callback after AFM is resolved |
-->
