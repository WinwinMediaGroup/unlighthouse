---
title: "Device Configuration"
description: "Configure device emulation settings for mobile and desktop scanning with custom dimensions and throttling options."
navigation:
  title: "Device Configuration"
---

## Introduction

Unlighthouse uses device emulation to test how your website performs on different screen sizes and network conditions. By default, scans emulate a mobile device (375x667) without throttling.

Configuration aliases make it easy to switch between common device types and settings.

## Device Types

### Desktop Scanning

```ts
import { defineUnlighthouseConfig } from 'unlighthouse/config'

export default defineUnlighthouseConfig({
  scanner: {
    device: 'desktop',
  },
})
```

### Mobile Scanning (Default)

```ts
export default defineUnlighthouseConfig({
  scanner: {
    device: 'mobile',
  },
})
```

## Custom Dimensions

Test specific viewport sizes for responsive breakpoints:

```ts
export default defineUnlighthouseConfig({
  lighthouseOptions: {
    screenEmulation: {
      width: 1800,
      height: 1000,
    },
  },
})
```

## Network Throttling

Throttling simulates slower network and CPU conditions for more realistic performance testing:

```ts
export default defineUnlighthouseConfig({
  scanner: {
    throttle: true,
  },
})
```

::note
Throttling is automatically enabled for production sites and disabled for localhost by default.
::
