---
title: 'getAttribute(name, [options])'
description: 'Browser module: locator.getAttribute method'
---

# getAttribute(name, [options])

Returns the element attribute value for the given attribute name.

<TableWithNestedRows>

| Parameter       | Type   | Default | Description                                                                                                                                                                                                                                                                                                         |
| --------------- | ------ | ------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| name            | string | `''`    | Attribute name to get the value for.                                                                                                                                                                                                                                                                                |
| options         | object | `null`  |                                                                                                                                                                                                                                                                                                                     |
| options.timeout | number | `30000` | Maximum time in milliseconds. Pass `0` to disable the timeout. Default is overridden by the `setDefaultTimeout` option on [BrowserContext](https://grafana.com/docs/k6/<K6_VERSION>/javascript-api/k6-browser/browsercontext/) or [Page](https://grafana.com/docs/k6/<K6_VERSION>/javascript-api/k6-browser/page/). |

</TableWithNestedRows>

### Returns

| Type            | Description |
| --------------- | ----------- | --------------------------------------------------------------------------------------------------------- |
| `Promise<string | null>`      | A Promise that fulfills with the string value of the attribute or `null` if the attribute is not present. |

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
  const textbox = page.locator('#text1');
  const attribute = await textbox.getAttribute('onfocus');
  console.log(attribute);
}
```

{{< /code >}}
