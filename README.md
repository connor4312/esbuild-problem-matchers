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

### ESBuild via JS

For this problem matcher to be picked up, you need to specify your watch `onRebuild` property to match what this problem matcher is looking for. For example:

```
    console.log('[watch] build started')
    
    await esbuild
      .build({
        ...otherOptions,
        watch: {
          onRebuild(error, result) {
            console.log('[watch] build started')
            if (error) {
              error.errors.forEach((error) =>
                console.error(
                  `> ${error.location.file}:${error.location.line}:${error.location.column}: error: ${error.text}`
                )
              )
            } else console.log('[watch] build finished')
          },
        },
      })
      .then(() => {
        console.log('[watch] build finished')
      })
```

