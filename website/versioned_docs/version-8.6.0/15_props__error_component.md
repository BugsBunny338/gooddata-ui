---
id: version-8.6.0-error_component
title: ErrorComponent
sidebar_label: ErrorComponent
copyright: (C) 2007-2018 GoodData Corporation
original_id: error_component
---

ErrorComponent indicator is a property that enables you to customize what content is displayed when a visual component is in its error state. You can disable the default setting of the ErrorComponent indicator by explicitly passing null instead.

The ErrorComponent indicator is supported by all visualization components.

## Example: Disabled ErrorComponent

In the following example, the KPI shows neither the loading indicator nor the error message.

```jsx
import { Kpi } from "@gooddata/sdk-ui";
import { Ldm } from "./ldm";

<Kpi
    measure={Ldm.$FranchiseFees}
    LoadingComponent={null}
    ErrorComponent={null}
/>
```

## Example: Customized ErrorComponent

In the following example, the default ErrorComponent is replaced by a custom component.

```jsx
import { Kpi } from "@gooddata/sdk-ui";
import { Ldm } from "./ldm";

const CustomError = ({
    code,
    message,
    description,
    icon
}) => (
    <p>
        <span className={icon} /> <strong>{message}</strong><br />
        {description}
    </p>
);

<Kpi
    measure={Ldm.$FranchiseFees}
    ErrorComponent={CustomError}
/>
```
