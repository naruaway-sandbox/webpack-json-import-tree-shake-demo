# webpack-json-import-tree-shake-demo

**The PR to fix this issue is https://github.com/webpack/webpack/pull/17637**

When using `webpack@5.88.2` with the default configuration, unused JSON imports are not tree-shaked properly for non trivial cases.
See [src/index.js](src/index.js) and the imported files in this repo to see the reproduction case.

## How to reproduce the issue

```
npm ci
npm run build
```

The following is the description of the bug:
- Actual behavior: `dist/main.js` includes the huge JSON payload in the form of `JSON.parse(...)` although this is unused.
- Expected behavior: We should not see the JSON payload embedded.
