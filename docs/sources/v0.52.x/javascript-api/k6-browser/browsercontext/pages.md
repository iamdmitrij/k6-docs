---
title: 'pages()'
description: 'Returns a list of pages inside this BrowserContext.'
---

# pages()

{{< admonition type="caution" >}}

This feature has **known issues**. For details, refer to
[#444](https://github.com/grafana/xk6-browser/issues/444).

{{< /admonition >}}

Returns all open [Page](https://grafana.com/docs/k6/<K6_VERSION>/javascript-api/k6-browser/page/)s in the `BrowserContext`.

### Returns

| Type          | Description                                                                                                        |
| ------------- | ------------------------------------------------------------------------------------------------------------------ |
| `Array<Page>` | An array of [page](https://grafana.com/docs/k6/<K6_VERSION>/javascript-api/k6-browser/page/) objects. |

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

export default function () {
  const context = await browser.newContext();
  await context.newPage();
  const pages = context.pages();
  console.log(pages.length); // 1
  await context.close();
}
```

{{< /code >}}
