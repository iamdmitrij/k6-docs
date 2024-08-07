---
title: 'allHeaders()'
description: 'Browser module: Response.allHeaders method'
---

# allHeaders()

{{< admonition type="caution" >}}

This method has a **known issue**. For details, refer to [#965](https://github.com/grafana/xk6-browser/issues/965).

{{< /admonition >}}

An object of key value pairs made up of HTTP headers associated with the response and the ones that the browser adds (such as cookies). All header names are lower-case.

### Returns

| Type                              | Description                                                              |
| --------------------------------- | ------------------------------------------------------------------------ |
| `Promise<Record<string, string>>` | A promise that resolves to an object of key value pairs for each header. |

### Example

{{< code >}}

```javascript
import { browser } from 'k6/browser';

export const options = {
  scenarios: {
    ui: {
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

  try {
    const res = await page.goto('https://test.k6.io/');

    const allHeaders = await res.allHeaders();
    console.log(`allHeaders: ${JSON.stringify(allHeaders)}`); // allHeaders: {"transfer-encoding":"chunked"...}
  } finally {
    await page.close();
  }
}
```

{{< /code >}}
