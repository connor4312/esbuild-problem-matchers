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
