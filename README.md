# esbuild-problem-matchers

To use this, add the `esbuild` or `esbuild-watch` problem matcher to your tasks.json, as appropriate. For example:

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "type": "npm",
      "script": "watch",
      "group": "build",
      "problemMatcher": "$esbuild-watch",
      "isBackground": true,
      "label": "npm: watch"
    },
    {
      "type": "npm",
      "script": "build",
      "group": "build",
      "problemMatcher": "$esbuild",
      "label": "npm: build"
    }
  ]
}
```

### ESBuild via CLI Setup

Nothing more is needed for this to work with the esbuild cli.

If you're using an esbuild version before 0.14.1, you should use the `$esbuild-0.13` and `$esbuild-0.13-watch` problem matches instead, as it has different output.

### ESBuild via JS

For this problem matcher to be picked up, you need to add a plugin property to emit the problems that the watcher is looking for. For example:

```js
/**
 * @type {import('esbuild').Plugin}
 */
const esbuildProblemMatcherPlugin = {
  name: 'esbuild-problem-matcher',

  setup(build) {
    build.onStart(() => {
      console.log('[watch] build started');
    });
    build.onEnd((result) => {
      result.errors.forEach(({ text, file, line, column }) => {
        console.error(`✘ [ERROR] ${text}`);
        console.error(`    ${location.file}:${location.line}:${location.column}`);
      });

      console.log('[watch] build finished');
    });
  },
};

// add the esbuildProblemMatcherPlugin to the esbuild plugins array
await esbuild.context({
  /* ... your options */
  plugins: [
    /* add to the end of plugins array */
    esbuildProblemMatcherPlugin,
  ],
});
```
