# SportChart - Reference Implementations

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Working implementations of the [TopChart Open Sports Data Standard](https://github.com/sportchart/standard).

Choose your language: **Python** | **JavaScript** | **Go**

---

## Python

### Install

```bash
pip install sportchart
```

### Quick Start

```python
from sportchart import Publisher, Event, Result

pub = Publisher(federation_id="cysaf")

event = Event(
    name="CYSAF Championship 2025",
    date="2025-06-14",
    location="Larnaca",
    sport="sailing"
)

results = [
    Result(athlete="Petros G.", club="Marina", position=1, points=9),
    Result(athlete="Maria K.", club="Larnaca", position=2, points=7)
]

pub.publish(event, results)
```

**Features:** Type-safe, validation, error handling, batch operations.

See `python/README.md` for full API docs.

---

## JavaScript

### Install

```bash
npm install @sportchart/sdk
```

### Quick Start

```javascript
import { Publisher } from '@sportchart/sdk';

const pub = new Publisher({ federationId: 'cysaf' });

const event = {
  name: 'CYSAF Championship 2025',
  date: '2025-06-14',
  location: 'Larnaca',
  sport: 'sailing'
};

const results = [
  { athlete: 'Petros G.', club: 'Marina', position: 1, points: 9 },
  { athlete: 'Maria K.', club: 'Larnaca', position: 2, points: 7 }
];

await pub.publish(event, results);
```

**Features:** Async/await, TypeScript support, browser & Node.js, real-time.

See `javascript/README.md` for full API docs.

---

## Go

### Install

```bash
go get github.com/sportchart/implementations/go
```

### Quick Start

```go
package main

import "github.com/sportchart/implementations/go/sportchart"

func main() {
    pub := sportchart.NewPublisher("cysaf", apiKey)
    
    event := &sportchart.Event{
        Name:     "CYSAF Championship 2025",
        Date:     "2025-06-14",
        Location: "Larnaca",
        Sport:    "sailing",
    }
    
    results := []*sportchart.Result{
        {Athlete: "Petros G.", Club: "Marina", Position: 1, Points: 9},
        {Athlete: "Maria K.", Club: "Larnaca", Position: 2, Points: 7},
    }
    
    pub.Publish(ctx, event, results)
}
```

**Features:** Concurrent, context-based, high performance, production-ready.

See `go/README.md` for full API docs.

---

## Standard Compliance

All implementations strictly follow [TopChart Open Standard](https://github.com/sportchart/standard):

- ✅ Event-centric data model
- ✅ Flat results table
- ✅ JSON schema validation
- ✅ REST API compatible
- ✅ CC0/MIT licensing

---

## Common Patterns

**CSV Import:**
```python
results = [Result(**row) for row in csv.DictReader(f)]
pub.publish(event, results)
```

**Batch Processing:**
```python
executor = ThreadPoolExecutor(max_workers=5)
futures = [executor.submit(pub.publish, event, results) for ...]
```

**Real-Time Streaming:**
```javascript
const stream = pub.createStream({ batchSize: 10 });
spotterFeed.on('result', r => stream.write(r));
```

---

## Testing

```bash
# Python
pytest tests/

# JavaScript
npm test

# Go
go test ./...
```

---

## Support

- **Issues:** GitHub issues
- **Questions:** GitHub Discussions
- **Docs:** Each language folder
- **Examples:** /examples

---

## Contact

Aleksandr Fediaev
linkedin.com/in/artiman

---

**Pick your language. Start publishing.** 🚀
