---
category: Components
group: Navigation
title: Breadcrumb
cover: https://mdn.alipayobjects.com/huamei_7uahnr/afts/img/A*I5a2Tpqs3y0AAAAAAAAAAAAADrJ8AQ/original
coverDark: https://mdn.alipayobjects.com/huamei_7uahnr/afts/img/A*Tr90QKrE_LcAAAAAAAAAAAAADrJ8AQ/original
demo:
  cols: 2
---

A breadcrumb displays the current location within a hierarchy. It allows going back to states higher up in the hierarchy.

## When To Use

- When the system has more than two layers in a hierarchy.
- When you need to inform the user of where they are.
- When the user may need to navigate back to a higher level.

```jsx
// works when >=5.3.0, recommended ✅
return <Breadcrumb items={[{ title: 'sample' }]} />;

// works when <5.3.0, deprecated when >=5.3.0 🙅🏻‍♀️
return (
  <Breadcrumb>
    <Breadcrumb.Item>sample</Breadcrumb.Item>
  </Breadcrumb>
);

// or

return <Breadcrumb routes={[{ breadcrumbName: 'sample' }]} />;
```

## Examples

<!-- prettier-ignore -->
<code src="./demo/basic.tsx">Basic Usage</code>
<code src="./demo/withIcon.tsx">With an Icon</code>
<code src="./demo/react-router.tsx" iframe="200">react-router V6</code>
<code src="./demo/separator.tsx">Configuring the Separator</code>
<code src="./demo/overlay.tsx">Bread crumbs with drop down menu</code>
<code src="./demo/separator-component.tsx">Configuring the Separator Independently</code>
<code src="./demo/debug-routes.tsx">Debug Routes</code>

## API

### Breadcrumb

| Property | Description | Type | Default | Version |
| --- | --- | --- | --- | --- |
| itemRender | Custom item renderer | (route, params, routes, paths) => ReactNode | - |  |
| params | Routing parameters | object | - |  |
| items | The routing stack information of router | [items\[\]](#ItemType) | - | 5.3.0 |
| separator | Custom separator | ReactNode | `/` |  |

### ItemType

> type ItemType = [RouteItemType](#RouteItemType) | [SeparatorType](#SeparatorType)

### RouteItemType

| Property | Description | Type | Default | Version |
| --- | --- | --- | --- | --- |
| className | The additional css class | string | - |  |
| dropdownProps | The dropdown props | [Dropdown](/components/dropdown) | - |  |
| href | Target of hyperlink. Can not work with `path` | string | - |  |
| path | Connected path. Each path will connect with prev one. Can not work with `href` | string | - |  |
| menu | The menu props | [MenuProps](/components/menu/#api) | - | 4.24.0 |
| onClick | Set the handler to handle click event | (e:MouseEvent) => void | - |  |
| title | item name | ReactNode | - |  |

### SeparatorType

```ts
const item = {
  type: 'separator', // Must have
  separator: '/',
};
```

| Property  | Description       | Type        | Default | Version |
| --------- | ----------------- | ----------- | ------- | ------- |
| type      | Mark as separator | `separator` |         | 5.3.0   |
| separator | Custom separator  | ReactNode   | `/`     | 5.3.0   |

### Use with browserHistory

The link of Breadcrumb item targets `#` by default, you can use `itemRender` to make a `browserHistory` Link.

```jsx
import { Link } from 'react-router';

const items = [
  {
    path: 'index',
    title: 'home',
  },
  {
    path: 'first',
    title: 'first',
    children: [
      {
        path: '/general',
        title: 'General',
      },
      {
        path: '/layout',
        title: 'Layout',
      },
      {
        path: '/navigation',
        title: 'Navigation',
      },
    ],
  },
  {
    path: 'second',
    title: 'second',
  },
];
function itemRender(route, params, items, paths) {
  const last = items.indexOf(item) === items.length - 1;
  return last ? <span>{item.title}</span> : <Link to={paths.join('/')}>{item.title}</Link>;
}

return <Breadcrumb itemRender={itemRender} items={items} />;
```

## Design Token

<ComponentTokenTable component="Breadcrumb"></ComponentTokenTable>
