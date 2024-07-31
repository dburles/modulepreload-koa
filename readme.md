# modulepreload-koa

Koa middleware for generating [modulepreload](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/rel/modulepreload) link relations for a [Link](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Link) entity-header based on the requested JavaScript modules import graph. This will prevent request waterfalls for nested module imports. Supports import maps.

## Install

```sh
npm i modulepreload-koa
```

## Usage example

```js
import Koa from "koa";
import serve from "koa-static";
import createModulePreloadMiddleware from "modulepreload-koa/createModulePreloadMiddleware.mjs";

const app = new Koa();

const APP_ROOT = "app";

app.use(createModulePreloadMiddleware(APP_ROOT));
app.use(serve(APP_ROOT));

app.listen(3000);
```

## API

### `createModulePreloadMiddleware(path[, options])`

- `path` {string} Path to the application root directory, eg "app".
- `options` {Object}
  - `extensions` {Array&lt;string&gt;} The file extensions to consider for module scripts. Defaults to: `["mjs", "js"]`.
  - `importMap` {string} Import map string.
  - `cache` {Object} A custom (map-like) cache.
