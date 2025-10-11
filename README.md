> I’m early in my career, but I build like an operator: typed contracts, deterministic replays, and telemetry that explains **what happened and why** — then I write down the path so the next person ships faster. I like working with people who share the goal but **think differently**; that’s where innovation happens.

**Motto**  
*I'm not afraid of being left behind—I'm excited about what I can build with the emerging technologies of tomorrow. Every new framework, every breakthrough, every innovation is an opportunity to create something that didn't exist yesterday and solve problems we haven't even discovered yet.*

**Site:** https://yeonthelee.tech • **Org:** https://github.com/AmpyFin • **Email:** yeonholee50@gmail.com

---

## Proof, not promises

### Impact snapshots
- **Data quality** — Rebuilt vendor‑data flow with drift/orphan detection → **bad‑data incidents ↓ >86%**; same‑day updates across ~20k SKUs/week.
- **Latency to insight** — Turned a multi‑day compatibility test‑matrix into **< 1 hour** via a tree‑based engine on AWS Neptune.
- **Reproducibility** — Codified **run_id / universe_id** and typed configs → deterministic replays caught ordering bugs **before** prod.
- **On‑call sanity** — Introduced circuit breakers, backoff, and DLQs with domain metrics → p95 stabilized while throughput rose.

> I’m happiest when a teammate says, “debugging this is boring now.”

---

## Mini‑stories (how I learn)

**1) “Float lies hurt models.”**  
I once traced a drifting signal to a float conversion hiding inside a provider. I replaced it with **decimal‑as‑string** fields and explicit currencies across the contract. We reran the same data through a replay and the variance disappeared. Lesson: **pin the contract first**; code follows.

**2) “Don’t scale a mystery.”**  
An ingestion path hit rate limits under burst. Before parallelizing, I added **trace IDs** and a **bounded‑concurrency gate** with cancellation. The flamegraph pointed at an unnecessary JSON reparse. Fixing that bought more headroom than extra goroutines.

**3) “Explain it to future me.”**  
Every tricky bug gets a golden sample in a `fixtures/` folder, a one‑page “why it failed,” and a CI check. When it fails again in six months, I’ll thank past me.

---

## A small craft demo

Two files, one promise: **determinism**.

**`contracts/bars.proto` (excerpt)**

```proto
message Bar {
  string ticker        = 1;   // "AAPL"
  string currency      = 2;   // "USD"
  int64  event_time_ns = 3;   // exchange event time
  string open          = 4;   // decimal as string
  string high          = 5;
  string low           = 6;
  string close         = 7;
  string volume        = 8;   // bigint as string
}
```

**`bus/publish.go` (essentials)**

```go
b := &barsv1.Bar{Ticker: "AAPL", Currency: "USD",
  EventTimeNs: time.Now().UnixNano(),
  Open: "233.12", High: "235.00", Low: "232.80", Close: "234.90", Volume: "1865321",
}
payload, _ := proto.Marshal(b)

env := ampybus.EnvelopeFor("bars.v1", payload,
  ampybus.WithRunID("run_2025_10_11"),
  ampybus.WithUniverseID("us_equities"),
  ampybus.WithTraceContextFrom(ctx),
)

_ = js.Publish("bars.v1", env.Bytes())
```

- Contract makes conversions explicit.  
- Envelope stamps context for replays & tracing.  
- Same payload works in Python/C++ because contracts are the source of truth.

---

## What I’m building (and why)

- **ampy‑proto** — canonical schemas for markets (bars/ticks/fundamentals/news/fx/corporate_actions/universe/signals/orders/fills/positions/metrics).  
  `pip install ampy-proto` • https://github.com/AmpyFin/ampy-proto

- **ampy‑bus** — deterministic messaging: envelope, headers, QoS tiers, DLQ, NATS/Kafka helpers, trace propagation.  
  https://github.com/AmpyFin/ampy-bus

- **ampy‑config** — typed config & secrets facade (Go + Python), runtime reloads, secret indirection.  
  https://github.com/AmpyFin/ampy-config

- **ampy‑observability** — JSON logs + Prometheus metrics + OTLP tracing, plus a docker‑compose stack for local runs.  
  https://github.com/AmpyFin/ampy-observability

- **AmpyFin (first OSS Python version)** — the earliest open‑source Python repo that seeded today’s modular platform (historicals/ingestion experiments, typed contracts).  
  https://github.com/AmpyFin

- **yfinance‑go** — production‑minded free‑data client (historicals/quotes/fundamentals), bounded concurrency, session rotation, circuit breakers; library + CLI (`yfin pull`).  
  https://github.com/AmpyFin/yfinance-go

- **tiingo‑go** — normalized fundamentals & prices (Go) with safe decimals and time semantics. *(private — link intentionally omitted)*

> Tools matter, but I’m not selling a platform. I’m selling the ability to take a messy, real‑world requirement and turn it into something robust, observable, and easy to change.

---

## How I work

1. **Pin the interface** (fields, units, time semantics).  
2. **Make failure boring** (timeouts, retries, backoff, idempotency, DLQ).  
3. **Instrument day 0** (structured logs, labeled metrics, purposeful spans).  
4. **Reproduce before clever** (golden samples, seedable randomness, deterministic replays).  
5. **Automate the path** (scripts/CI; “happy path” is the default).  
6. **Write it down** (a future teammate will thank me — usually me).

---

## Tech I actually use

**Go • Python • C/C++ • SQL** · **Protobuf** · **NATS JetStream/Kafka** · **OpenTelemetry/Prometheus/Grafana** · **Docker/Linux** · **PostgreSQL/DuckDB/MongoDB**

---

## Open to mentorship & feedback

I learn fast from people who’ve been there. If you see a sharper way to build or reason about any of this, I’m all ears. I’ll try it, measure it, and write up what I learned.

**Say hi:** yeonholee50@gmail.com · https://www.linkedin.com/in/yeon-lee · https://yeonthelee.tech
