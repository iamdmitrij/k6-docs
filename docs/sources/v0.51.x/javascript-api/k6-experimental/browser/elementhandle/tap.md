---
title: 'tap(options)'
description: 'Browser module: elementhandle.tap(options) method'
---

# tap(options)

Taps the element.

<TableWithNestedRows>

| Parameter           | Type     | Default | Description                                                                                                                                                                                                                                                                                                                                   |
| ------------------- | -------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| options             | object   | `null`  |                                                                                                                                                                                                                                                                                                                                               |
| options.force       | boolean  | `false` | Setting this to `true` will bypass the actionability checks (`visible`, `stable`, `enabled`).                                                                                                                                                                                                                                                 |
| options.modifiers   | string[] | `null`  | `Alt`, `Control`, `Meta` or `Shift` modifiers keys pressed during the action. If not specified, currently pressed modifiers are used.                                                                                                                                                                                                         |
| options.noWaitAfter | boolean  | `false` | If set to `true` and a navigation occurs from performing this action, it will not wait for it to complete.                                                                                                                                                                                                                                    |
| options.position    | object   | `null`  | A point to use relative to the top left corner of the element. If not supplied, a visible point of the element is used.                                                                                                                                                                                                                       |
| options.position.x  | number   | `0`     | The x coordinate.                                                                                                                                                                                                                                                                                                                             |
| options.position.y  | number   | `0`     | The y coordinate.                                                                                                                                                                                                                                                                                                                             |
| options.strict      | boolean  | `false` | When `true`, the call requires selector to resolve to a single element. If given selector resolves to more than one element, the call throws an exception.                                                                                                                                                                                    |
| options.timeout     | number   | `30000` | Maximum time in milliseconds. Pass `0` to disable the timeout. Default is overridden by the `setDefaultTimeout` option on [BrowserContext](https://grafana.com/docs/k6/<K6_VERSION>/javascript-api/k6-experimental/browser/browsercontext/) or [Page](https://grafana.com/docs/k6/<K6_VERSION>/javascript-api/k6-experimental/browser/page/). |
| options.trial       | boolean  | `false` | Setting this to `true` will perform the actionability checks without performing the action.                                                                                                                                                                                                                                                   |

</TableWithNestedRows>

### Returns

| Type            | Description                                              |
| --------------- | -------------------------------------------------------- |
| `Promise<void>` | A Promise that fulfills when the tap action is finished. |

### Example

{{< code >}}

```javascript
import { browser } from 'k6/experimental/browser';

export const options = {
  scenarios: {
    browser: {
      executor: 'shared-iterations',
      options: {
        browser: {
          type: 'chromium',
        },
      },
    },
  },
};

export default async function () {
  const page = browser.newPage({
    hasTouch: true,
  });

  await page.goto('https://test.k6.io/browser.php');
  const el = page.$('#numbers-options');
  await el.tap();
}
```

{{< /code >}}