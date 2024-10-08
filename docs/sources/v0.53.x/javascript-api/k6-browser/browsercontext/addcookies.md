---
title: 'addCookies()'
description: 'Clears context cookies.'
---

# addCookies()

Adds a list of [cookies](https://grafana.com/docs/k6/<K6_VERSION>/javascript-api/k6-browser/browsercontext/cookie) into the [browser context](https://grafana.com/docs/k6/<K6_VERSION>/javascript-api/k6-browser/browsercontext/). All pages within this [browser context](https://grafana.com/docs/k6/<K6_VERSION>/javascript-api/k6-browser/browsercontext/) will have these [cookies](https://grafana.com/docs/k6/<K6_VERSION>/javascript-api/k6-browser/browsercontext/cookie) set.

{{< admonition type="note" >}}

If a [cookie](https://grafana.com/docs/k6/<K6_VERSION>/javascript-api/k6-browser/browsercontext/cookie)'s `url` property is not provided, both `domain` and `path` properties must be specified.

{{< /admonition >}}

### Returns

| Type            | Description                                                                                                                                                                                                                                                        |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `Promise<void>` | A Promise that fulfills when the [cookies](https://grafana.com/docs/k6/<K6_VERSION>/javascript-api/k6-browser/browsercontext/cookie) have been added to the [browser context](https://grafana.com/docs/k6/<K6_VERSION>/javascript-api/k6-browser/browsercontext/). |

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
  const context = await browser.newContext();
  const page = await context.newPage();

  try {
    const unixTimeSinceEpoch = Math.round(new Date() / 1000);
    const day = 60 * 60 * 24;
    const dayAfter = unixTimeSinceEpoch + day;
    const dayBefore = unixTimeSinceEpoch - day;

    await context.addCookies([
      // this cookie expires at the end of the session
      {
        name: 'testcookie',
        value: '1',
        sameSite: 'Strict',
        domain: 'httpbin.org',
        path: '/',
        httpOnly: true,
        secure: true,
      },
      // this cookie expires in a day
      {
        name: 'testcookie2',
        value: '2',
        sameSite: 'Lax',
        domain: 'httpbin.org',
        path: '/',
        expires: dayAfter,
      },
      // this cookie expires in the past, so it will be removed.
      {
        name: 'testcookie3',
        value: '3',
        sameSite: 'Lax',
        domain: 'httpbin.org',
        path: '/',
        expires: dayBefore,
      },
    ]);

    const response = await page.goto('https://httpbin.org/cookies', {
      waitUntil: 'networkidle',
    });
    console.log(response.json());
    // prints:
    // {"cookies":{"testcookie":"1","testcookie2":"2"}}
  } finally {
    await page.close();
  }
}
```

{{< /code >}}
