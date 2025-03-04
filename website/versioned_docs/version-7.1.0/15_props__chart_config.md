---
title: Chart Config
sidebar_label: Chart Config
copyright: (C) 2007-2018 GoodData Corporation
id: version-7.1.0-chart_config
original_id: chart_config
---

This article describes the options for configuring a chart.

## Structure

```javascript
{
    colors: ['rgb(195, 49, 73)', 'rgb(168, 194, 86)'], // array of strings
    xaxis: {
        visible: true, // boolean
        labelsEnabled: true, // boolean
        rotation: 'auto', // 'auto' or numeral string
        min: '10', // numeral string
        max: '20' // numeral string
    },
    yaxis: {
        visible: true, // boolean
        labelsEnabled: true, // boolean
        rotation: 'auto', // string
        min: '30', // numeral string
        max: '40' // numeral string
    },
    secondary_yaxis: {
        visible: true, // boolean
        labelsEnabled: true, // boolean
        rotation: 'auto', // string
        min: '300', // numeral string
        max: '400', // numeral string
        measures: ['measureLocalIdentifier']
    },
    legend: {
        enabled: true, // boolean
        position: 'bottom', // 'top' | 'left' | 'right' | 'bottom'
    },
    dataLabels: {
        visible: 'auto' // 'auto' | true | false
    },
    grid: {
        enabled: true // boolean
    },
    separators: {
        thousand: ',',
        decimal: '.'
    },
    stackMeasures: true, // boolean
    stackMeasuresToPercent: true, // boolean
    primaryChartType: 'column', // string
    secondaryChartType: 'area', // string
    dualAxis: false // boolean
}
```
Note: `primaryChartType`, `secondaryChartType`, `dualAxis` are only available for [Combo chart](10_vis__combo_chart_component.md)

## Configure colors

To configure colors, use the following options:
* [Color array (the `colors` property)](#color-array)
* [Custom color palette (the `colorPalette` property)](#custom-color-palette)
* [Color mapping (the `colorMapping` property)](#color-mapping)

If you have more than one option configured for a visualization, the following rules apply:
* The `colors` property overrides a custom color palette uploaded through the API.
* The `colorPalette` property overrides the `colors` property and the custom color palette uploaded through the API.
* The `colorMapping` property overrides the `colorPalette` property, the `colors` property, and the custom color palette uploaded through the API.

### Color array

The following are examples of a color array:

```javascript
['rgb(195, 49, 73)', 'rgb(168, 194, 86)']

```

```javascript
['#fa0510', '#AA2030']

```

If there are fewer colors than data points, then the colors are repeated. For example, here is how colors will be used for two colors and three data points:

```javascript
['rgb(195, 49, 73)', 'rgb(168, 194, 86)', 'rgb(195, 49, 73)']
```

To change colors in a chart, provide a `config` for each component where you want to change colors, or create a wrapped components with a `config` baked in.

**NOTE:** Heatmaps use only the first color from the provided colors as the base color, and generate the other colors themselves.

```javascript
import { Visualization } from '@gooddata/react-components';

// Example of embedding a visualization with custom colors and palette options
<Visualization
    projectId=<workspace-id>
    identifier=<visualization-id>
    config={{
        colors: ['rgb(195, 49, 73)', 'rgb(168, 194, 86)']
    }}
/>
```

Within one visualization:
* The `colors` property overrides a custom color palette uploaded through the API.
* The `colors` property can be overriden by the [`colorPalette` property](#custom-color-palette) or the [`colorMapping` property](#color-mapping).

### Custom color palette

If you [uploaded a custom color palette](https://help.gooddata.com/pages/viewpage.action?pageId=86794489) to your workspace, the visualizations created based on the [Visualization component](10_vis__insight_view.md) use this palette instead of the default colors.

To override the uploaded custom color palette for a specific visualization, define the `colorPalette` property for this visualization.

```javascript
import { Visualization } from '@gooddata/react-components';

// Example of embedding a visualization with a custom palette
<Visualization
   projectId=<workspace-id>
   identifier=<visualization-id>
   config={{
       colorPalette: [{
            guid: '01',
            fill: {
                r: 195,
                g: 49,
                b: 73
            }
        }, {
            guid: '02',
            fill: {
                r: 168,
                g: 194,
                b: 86
            }
        }, {
            guid: '03',
            fill: {
                r: 243,
                g: 217,
                b: 177
            }
        }]
    }}
/>
```

Within one visualization:
* The `colorPalette` property overrides the custom color palette uploaded through the API and the `colors` property.
* The `colorPalette` property can be overriden by the `colorMapping` property.

### Color mapping

Color mapping allows you to assign colors to individual measures or attribute elements. To set up color mapping, set the `colorMapping` property.

The `colorMapping` property contains an array of objects. Each object is represented by a pair of a mapping predicate and a color (color GUID or color value).

* A **mapping predicate** is a function that takes a result header as the first argument and returns a Boolean value indicating whether the color will be assigned to a particular measure or attribute element.
 For more information on how to create predicates, see [Create Predicates](30_tips__create_predicates.md).
* A **color** is an object that contains two keys, `type` and `value`.
    * To assign a color from a color palette (either the custom color palette uploaded through the API or the palette defined by the `colorPalette` property), set `type` to `guid`, and set `value` to the GUID of the color from the palette.
    * To assign a custom color, set `type` to `rgb`, and set `value` to an object containing the keys `r`, `g`, and `b` with numerical values.

The following example shows how to assign the color with GUID `02` to the measure with the local identifier `m1_localIdentifier`, and the black color to the measure with the local identifier `m2_localIdentifier`:

```javascript
import { Visualization } from '@gooddata/react-components';

// Example of embedding a visualization with custom color mapping
<Visualization
    projectId=<workspace-id>
    identifier=<visualization-id>
    config={{
        colorMapping: [{
            predicate: (headerItem) => {
                return headerItem.measureHeaderItem && (headerItem.measureHeaderItem.localIdentifier === 'm1_localIdentifier')
            },
            color: {
                type: 'guid',
                value: '02'
            }
        }, {
            predicate: (headerItem) => {
                return headerItem.measureHeaderItem && (headerItem.measureHeaderItem.localIdentifier === 'm2_localIdentifier')
            },
            color: {
                type: 'rgb',
                value: {
                    r: 0,
                    g: 0,
                    b: 0
                }
            }
        }]
    }}
/>
```
Within one visualization, the `colorMapping` property overrides the `colorPalette` property (while still can use its colors), the `colors` property, and the custom color palette uploaded through the API.

## Change legend visibility and position

* To hide the legend, set the `config.legend.enabled` property to `false`.
* To change the legend position, adjust the `config.legend.position` property \(`'left'`/`'right'`/`'top'`/`'bottom'`\).

```javascript
import { Visualization } from '@gooddata/react-components';

// Example of embedding a visualization with a custom legend position
<Visualization
    projectId=<workspace-id>
    identifier=<visualization-id>
    config={{
        legend: {
            enabled: true,
            position: 'bottom' // 'left', 'right', 'top'
        }
    }}
/>
```

## Change a separator in the number format

* To change the thousands separator, adjust the `config.separators.thousand` property.
* To change the decimal separator, adjust the `config.separators.decimal` property.

```javascript
import { Visualization } from '@gooddata/react-components';

// Example of embedding a visualization with a custom separator in the number format
<Visualization
    projectId=<workspace-id>
    identifier=<visualization-id>
    config={{
        separators: {
            thousand: ',',
            decimal: '.'
        }
    }}
/>
```

## Configure axes

* To change axis visibility, set the `config.xaxis.visible` property.
* To hide axis labels, set the `config.xaxis.labelsEnabled` property to `false`.

    **NOTE:** When `config.xaxis.visible` is set to `false`, axis labels are hidden automatically regardless of what `config.xaxis.labelsEnabled` is set to.
* To rotate axis labels, set `config.xaxis.rotation` to a desired value.
* To set the axis scale, set `config.xaxis.min` and `config.xaxis.max`.
* To show measures on a secondary axis, set `config.secondary_xaxis.measures`. If `config.secondary_xaxis.measures` is not configured, all measures are displayed on the main axis by default.

> For the properties of the Y axis, replace `xaxis` with `yaxis`.

```javascript
import { Visualization } from '@gooddata/react-components';

// Example of embedding a visualization with settings for the x-axis
<Visualization
    projectId=<workspace-id>
    identifier=<visualization-id>
    config={{
        xaxis: {
            visible: false,
            labelsEnabled: false,
            rotation: '-90',
            min: '150',
            max: '440'
        },
        secondary_xaxis: {
            visible: true,
            labelsEnabled: true,
            rotation: '-90',
            min: '1500',
            max: '4400',
            measures: ['measureLocalIdentifier1', 'measureLocalIdentifier2']
        }
    }}
/>
```

## Configure canvases

To configure data labels, set the `config.dataLabels` property.

```javascript
import { Visualization } from '@gooddata/react-components';

// Example of embedding a visualization with settings for the canvas
<Visualization
    projectId=<workspace-id>
    identifier=<visualization-id>
    config={{
        dataLabels: true,
        grid: {
            enabled: false
        }
    }}
/>
```

## Configure stacking

* You can configure stacking for the following types of charts:
    * [Area charts](10_vis__area_chart_component.md)
    * [Bar charts](10_vis__bar_chart_component.md)
    * [Column charts](10_vis__column_chart_component.md)
    * [Combo charts](10_vis__combo_chart_component.md)

         **NOTE:** In combo charts using column or area charts, stacking is applied only to the measures shown on the left axis.
    * Charts with the [secondary axis](#configure-axes)
* To display the total contribution of each measure, enable `config.stackMeasures`.
    * For area charts, `config.stackMeasures` is enabled by default.
    * For bar charts, column charts, and charts with the secondary axis, `config.stackMeasures` is ignored when the chart has only one measure.
* To display the percentage contribution of each measure, enable `config.stackMeasuresToPercent`.
    * If both `config.stackMeasuresToPercent` and `config.stackMeasures` are present, `config.stackMeasuresToPercent` overwrites `config.stackMeasures`.
    * For charts with the secondary axis, `config.stackMeasuresToPercent` is applied only to the left axis.

```javascript
import { Visualization } from '@gooddata/react-components';

// Example of embedding a visualization with stacking
<Visualization
    projectId=<workspace-id>
    identifier=<visualization-id>
    config={{
        stackMeasures: false,
        stackMeasuresToPercent: true
    }}
/>
```

## Customize tooltips and fonts

To customize tooltips and fonts, [implement a custom visualization](data_layer.md).
