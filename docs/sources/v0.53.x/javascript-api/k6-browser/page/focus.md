---
title: 'focus(selector[, options])'
description: 'Browser module: page.focus(selector[, options]) method'
---

# focus(selector[, options])

{{< admonition type="warning" >}}

Use locator-based [`locator.focus([options])`](https://grafana.com/docs/k6/<K6_VERSION>/javascript-api/k6-browser/locator/focus/) instead.

{{< /admonition >}}

This method fetches an element with `selector` and focuses it.

<TableWithNestedRows>

| Parameter       | Type    | Default | Description                                                                                                                                                                                                                                                                                                         |
| --------------- | ------- | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| selector        | string  | `''`    | A selector to search for an element. If there are multiple elements satisfying the selector, the first will be used.                                                                                                                                                                                                |
| options         | object  | `null`  |                                                                                                                                                                                                                                                                                                                     |
| options.strict  | boolean | `false` | When `true`, the call requires selector to resolve to a single element. If given selector resolves to more than one element, the call throws an exception.                                                                                                                                                          |
| options.timeout | number  | `30000` | Maximum time in milliseconds. Pass `0` to disable the timeout. Default is overridden by the `setDefaultTimeout` option on [BrowserContext](https://grafana.com/docs/k6/<K6_VERSION>/javascript-api/k6-browser/browsercontext/) or [Page](https://grafana.com/docs/k6/<K6_VERSION>/javascript-api/k6-browser/page/). |

</TableWithNestedRows>

### Returns

| Type            | Description                                          |
| --------------- | ---------------------------------------------------- |
| `Promise<void>` | A Promise that fulfills when the element is focused. |

### Example

{{< code >}}

```javascript
import { browser } from 'k6/browser';

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
  const page = await browser.newPage();

  await page.goto('https://test.k6.io/browser.php');
  await page.focus('#text1');
}
```

{{< /code >}}
