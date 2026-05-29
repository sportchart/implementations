# Top Chart - Reference Implementations

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Working implementations of the [Top Chart Open Sports Data Standard](https://github.com/sportchart/standard).

## Overview

Reference implementations in multiple languages to help federations publish results using the open standard.

**Choose your language:**
- [Python](#python) - Most popular, great for data processing
- [JavaScript](#javascript) - For web applications
- [Go](#go) - High performance, concurrent operations

## Python

### Installation

```bash
pip install topchart
```

### Quick Start

```python
from topchart import TopChartPublisher, EventMetadata, Result

# Initialize publisher
publisher = TopChartPublisher(
    federation_id="cysaf",
    api_key="your-api-key"
)

# Define event
event = EventMetadata(
    event_name="CYSAF Championship 2025",
    event_date="2025-06-14",
    location="Larnaca",
    sport="sailing"
)

# Create results
results = [
    Result(
        athlete_name="Petros G.",
        club="Marina",
        class_name="ORC-A",
        position=1,
        points=9
    ),
    Result(
        athlete_name="Maria K.",
        club="Larnaca",
        class_name="ORC-A",
        position=2,
        points=7
    )
]

# Publish
publisher.publish(event, results)
```

### Features

✅ Type-safe data validation
✅ Built-in error handling
✅ Retry logic for network issues
✅ Batch operations support
✅ Full documentation

### Documentation

See `python/README.md` for full API docs.

---

## JavaScript

### Installation

```bash
npm install @topchart/sdk
```

### Quick Start

```javascript
import { TopChartPublisher, EventMetadata } from '@topchart/sdk';

const publisher = new TopChartPublisher({
  federationId: 'cysaf',
  apiKey: 'your-api-key'
});

const event = new EventMetadata({
  eventName: 'CYSAF Championship 2025',
  eventDate: '2025-06-14',
  location: 'Larnaca',
  sport: 'sailing'
});

const results = [
  {
    athleteName: 'Petros G.',
    club: 'Marina',
    className: 'ORC-A',
    position: 1,
    points: 9
  },
  {
    athleteName: 'Maria K.',
    club: 'Larnaca',
    className: 'ORC-A',
    position: 2,
    points: 7
  }
];

await publisher.publish(event, results);
```

### Features

✅ Promise-based async/await
✅ TypeScript support
✅ Browser and Node.js compatible
✅ Real-time event streaming
✅ Webhook support

### Documentation

See `javascript/README.md` for full API docs.

---

## Go

### Installation

```bash
go get github.com/sportchart/implementations/go
```

### Quick Start

```go
package main

import (
    "context"
    "log"
    
    "github.com/sportchart/implementations/go/topchart"
)

func main() {
    publisher := topchart.NewPublisher(
        "cysaf",
        "your-api-key",
    )
    
    event := &topchart.EventMetadata{
        EventName: "CYSAF Championship 2025",
        EventDate: "2025-06-14",
        Location:  "Larnaca",
        Sport:     "sailing",
    }
    
    results := []*topchart.Result{
        {
            AthleteName: "Petros G.",
            Club:        "Marina",
            ClassName:   "ORC-A",
            Position:    1,
            Points:      9,
        },
        {
            AthleteName: "Maria K.",
            Club:        "Larnaca",
            ClassName:   "ORC-A",
            Position:    2,
            Points:      7,
        },
    }
    
    ctx := context.Background()
    if err := publisher.Publish(ctx, event, results); err != nil {
        log.Fatalf("publish failed: %v", err)
    }
}
```

### Features

✅ Concurrent publishing (batches)
✅ Context-based cancellation
✅ Custom retry policies
✅ Pluggable storage backends
✅ Production-ready

### Documentation

See `go/README.md` for full API docs.

---

## Standard Compliance

All implementations strictly follow the [Top Chart Open Sports Data Standard](https://github.com/sportchart/standard):

- ✅ Event-centric data model
- ✅ Flat results table (one row = one athlete)
- ✅ JSON schema validation
- ✅ REST API compatibility
- ✅ CC0/MIT licensing

## Common Patterns

### CSV Import

```python
import csv
from topchart import TopChartPublisher

publisher = TopChartPublisher("cysaf")

with open('results.csv') as f:
    reader = csv.DictReader(f)
    results = [Result(**row) for row in reader]
    publisher.publish(event, results)
```

### Batch Processing

```python
# Process 100 events in parallel
from concurrent.futures import ThreadPoolExecutor

with ThreadPoolExecutor(max_workers=5) as executor:
    futures = [
        executor.submit(publisher.publish, event, results)
        for event, results in events
    ]
    for future in futures:
        future.result()
```

### Real-Time Streaming

```javascript
const stream = publisher.createStream({
  event: eventMetadata,
  batchSize: 10,
  flushInterval: 1000 // ms
});

// As results come in from spotters
spotterFeed.on('result', (result) => {
  stream.write(result);
});
```

## Contributing

Implementations are MIT licensed. Contributions welcome!

### Testing

Each implementation includes comprehensive tests:

```bash
# Python
pytest python/tests/

# JavaScript
npm test

# Go
go test ./...
```

### Adding a New Language

1. Create new directory: `/{language}/`
2. Follow the structure of existing implementations
3. Add comprehensive examples
4. Update this README
5. Submit pull request

## Support

- **Issues:** Report bugs in GitHub issues
- **Questions:** Ask in Discussions
- **Docs:** Full documentation in each language folder
- **Examples:** See `examples/` directory

## Contact

**Project Lead:** Aleksandr Fediaev
**GitHub:** github.com/sportchart
**Standard Spec:** github.com/sportchart/standard

---

**Use the implementation that fits your stack.** 🚀

Open sports data for everyone.
