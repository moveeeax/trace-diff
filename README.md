# trace-diff

> "It got slower" becomes "the checkout DB span grew by 380 ms".

**Status:** 🚧 In development

## Overview

Compare two OpenTelemetry traces of the same operation and show where the time moved, turning "it got slower" into a named span.

## Features

- Aligns two traces of the same operation by span name and position in the tree, not by span ID
- Reports per-span deltas in self time and wall time, sorted by how much of the regression each one explains
- Detects spans that appeared, disappeared, or changed in count — the N+1 that showed up between releases
- Separates a span that got slower from a span that is simply called more often
- Compares aggregates of many traces per side, so a single unlucky request does not become the verdict
- Reads OTLP JSON or protobuf exports, or pulls traces by ID from a collector endpoint

## Stack

Go + go.opentelemetry.io/proto/otlp for the trace types, go.opentelemetry.io/collector/pdata for reading exports, cobra for the CLI.

## Usage

```bash
trace-diff --baseline traces/v1.42.json --candidate traces/v1.43.json --min-delta 25ms --format table
```

## License

MIT

---

Archived on 2026-11-05. The idea moved to [otel-trace-replay](https://github.com/moveeeax/otel-trace-replay/issues/2).
