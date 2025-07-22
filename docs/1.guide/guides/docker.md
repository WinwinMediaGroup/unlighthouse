---
title: "Docker Support"
description: "Run Unlighthouse in Docker containers for consistent CI/CD environments with proper Chromium configuration."
navigation:
  title: "Docker"
---

## Introduction

Unlighthouse supports Docker environments for consistent CI/CD deployments. Docker requires special Puppeteer configuration due to sandboxing restrictions.

::warning
Docker support is community-maintained and experimental. Use the CI integration for best results.
::

## Unlighthouse Config

It's recommended you only use the `@unlighthouse/ci` with Docker. Hosting the client does not have known support.

You will need to remove the Chrome sandbox in a Docker environment, this will require using an `unlighthouse.config.ts` file.

```ts
import { defineUnlighthouseConfig } from 'unlighthouse/config'

export default defineUnlighthouseConfig({
  puppeteerOptions: {
    headless: true,
    args: [
      '--no-sandbox',
      '--disable-setuid-sandbox',
      '--disable-gpu',
      '--ignore-certificate-errors',
    ],
  },
})
```

If you're using the `unlighthouse` binary instead of the CI integration, then you will need to tell Unlighthouse not to use the server and close when
the reports are finished.

```ts
export default defineUnlighthouseConfig({
  server: {
    open: false,
  },
  hooks: {
    'worker-finished': async () => {
      process.exit(0)
    },
  },
})
```

## Docker File

Please see the following community repos:
- [indykoning—Unlighthouse Docker](https://github.com/indykoning/unlighthouse-docker)
