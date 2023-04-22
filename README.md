# RelativeCI agent upload artifact action

GitHub action that uploads an artifact to share with [RelativeCI agent action](https://github.com/relative-ci/agent-action) when running during `workflow_run`.

The artifact will be available on the workflow page (see: actions/upload-artifact ["Where does the upload go?"](https://github.com/actions/upload-artifact#where-does-the-upload-go)) and it counts toward your GitHub storage usage.

---

To get started, follow [RelativeCI Setup guide](https://relative-ci.com/documentation/setup?utm_source=GitHub&utm_medium=agent-action).

## Example usage

```yaml
# .github/workflow/node.js.yml
name: Node.js CI

on:
  push:
    branches:
      - master
  pull_request:

jobs:
  build:
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '18.x'

      # Install dependencies
      - run: npm ci
 
      # Build bundle and output webpack stats
      - run: npm run build -- --json > webpack-stats.json
      
      # Upload relative-ci-artifact/webpack-stats.json to share with relative-ci/agent-action
      - name: Upload webpack stats artifact
        uses: relative-ci/agent-upload-artifact-action@v1
        with:
          webpackStatsFile: './webpack-stats.json
```

## Input

### `webpackStatsFile`

(default: `./webpack-stats.json`) Relative path to the generated bundle stats file

### `artifactName`

(default: `relative-ci-artifacts`) The artifact name

### `artifactWebpackStatsFile`

(default: `webpack-stats.json`) The artifact bundle stats file name

## `retentionDays`

(default: `90`) [actions/upload-artifact `retention-days` input](https://github.com/actions/upload-artifact#retention-period)
