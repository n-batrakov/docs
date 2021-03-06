---
description: A CORS middleware for Marble.js
---

# middleware-cors

### Installation

```bash
$ npm i @marblejs/middleware-cors
```

Requires `@marblejs/core` to be installed.

### Importing

```typescript
import { cors$ } from '@marblejs/middleware-cors';
```

### Type declaration <a id="type-declaration"></a>

```text
cors$ :: CORSOptions -> HttpMiddlewareEffect
```

### Parameters

| parameter | definition |
| :--- | :--- |
| _options_ | &lt;optional&gt; `CORSOptions` |

_**CORSOptions**_

| _**parameter**_ | definition |
| :--- | :--- |
| origin | &lt;optional&gt; `string | string[] | RegExp` |
| methods | &lt;optional&gt; `HttpMethod[]` |
| optionsSuccessStatus | &lt;optional&gt; `HttpStatus` |
| allowHeaders | &lt;optional&gt; `string | string[]`  |
| exposeHeaders | &lt;optional&gt; `string[]` |
| withCredentials | &lt;optional&gt; `boolean` |
| maxAge | &lt;optional&gt; `number` |

This object allows you to configure CORS headers with various options. Both `methods` and `exposeHeaders` support wildcard. By default options are configured as following.

```typescript
{ 
  origin: '*',
  methods: ['HEAD', 'GET', 'POST', 'PUT', 'PATCH', 'DELETE', 'OPTIONS'],
  withCredentials: false,
  optionsSuccessStatus: HttpStatus.NO_CONTENT, // 204
}
```

Note that provided options are merged with default options so you need to overwrite each default parameter you want to customize.

### Basic usage

{% code-tabs %}
{% code-tabs-item title="app.ts" %}
```typescript
import { cors$ } from '@marblejs/middleware-cors';

export default httpListener({
  middlewares: [
    cors$({
      origin: '*',
      allowHeaders: '*',
      methods: ['GET', 'POST', 'PUT', 'PATCH', 'DELETE', 'OPTIONS'],
    })
  ],
  effects: [/* ... */],
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

For security purpose it's better to be strict as possible when configuring CORS options.

### Strict usage

{% code-tabs %}
{% code-tabs-item title="app.ts" %}
```typescript
import { cors$ } from '@marblejs/middleware-cors';

export default httpListener({
  middlewares: [
    cors$({
      origin: ['http://example1.com', 'http://example2.com'],
      allowHeaders: ['Origin', 'Authorization', 'Content-Type'],
      methods: ['GET', 'POST', 'PUT', 'PATCH', 'DELETE', 'OPTIONS'],
    })
  ],
  effects: [/* ... */],
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Headers notation is case insensitive. `content-type` will also work.

