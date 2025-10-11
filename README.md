<div align="center">

# Yeon Lee  
<sub>systems-minded software engineer • early in my career • learning out loud</sub>

<a href="https://yeonthelee.tech" title="Personal site"><kbd>yeonthelee.tech</kbd></a> ·
<a href="https://www.ampyfin.com" title="AmpyFin — projects & ideas"><kbd>ampyfin.com</kbd></a> ·
<a href="https://github.com/AmpyFin" title="GitHub org"><kbd>@AmpyFin</kbd></a> ·
<a href="mailto:yeonholee50@gmail.com" title="Email me"><kbd>email</kbd></a>

<br/><br/>

<code>#contracts-first</code> · <code>#deterministic-replays</code> · <code>#observability</code> · <code>#typed-config</code> · <code>#learn-in-public</code>

</div>

> *I'm not afraid of being left behind—I'm excited about what I can build with the emerging technologies of tomorrow. Every new framework, every breakthrough, every innovation is an opportunity to create something that didn't exist yesterday and solve problems we haven't even discovered yet.*

---

<a id="palette"></a>
## ⌘K — Command Palette (jump anywhere)
- **Proof →** [impact snapshots](#impact) • [mini-stories](#mini-stories) • [craft demo](#craft)
- **Projects →** [proto](#proto) • [bus (envelope & headers)](#envelope-headers) • [config](#config) • [observability (telemetry)](#telemetry) • [ampyfin main](#ampyfin) • [yfinance-go](#yfinance-go) • [tiingo-go](#tiingo-go)
- **Process →** [how I work](#how-i-work) • [toolbox](#toolbox) • [contact](#say-hi)

---

<a id="tags"></a>
## 🏷️ Tag Cloud (click to filter by section)
[contracts-first](#craft) ·
[deterministic-replays](#how-i-work) ·
[trace-context](#envelope-headers) ·
[domain-metrics](#telemetry) ·
[bounded-concurrency](#yfinance-go) ·
[typed-config](#config) ·
[learn-in-public](#ampyfin)

---

<a id="impact"></a>
## Proof — Impact snapshots
> Show, don’t tell.

- **Data quality** — Drift/orphan checks → **bad‑data incidents ↓ >86%**; **same‑day updates** across ~20k SKUs/week.  
  <a href="#telemetry"><sup>telemetry-backed</sup></a>
- **Latency to insight** — Tree‑based compatibility engine on AWS Neptune → **multi‑day test matrix → < 1 hour**.  
  <a href="#craft"><sup>contract-first demo</sup></a>
- **Reproducibility** — **run_id / universe_id / trace context** → ordering bugs caught **before prod** via deterministic replays.  
  <a href="#envelope-headers"><sup>envelope & headers</sup></a>

---

<a id="mini-stories"></a>
## Mini-stories — how I learn
- **Float lies hurt models.** Replaced silent float coercions with **decimal-as-string** + explicit currency; variance disappeared on replay.  
- **Don’t scale a mystery.** Added **trace IDs** + **bounded concurrency**; flamegraph exposed a costly reparse—fix beat parallelism.  
- **Explain it to future me.** Every tricky bug gets a fixture, a 1‑pager “why it failed,” and a CI check.

---

<a id="craft"></a>
## Craft demo (2 files, one promise)

**`contracts/bars.proto`**

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

**`bus/publish.go`**

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

> Contract makes units & time explicit. Envelope stamps context for replays & tracing. Same payload works in Python/C++.

---

## Projects
> Click a card to jump. Wherever possible, repos come with fixtures, examples, and CI smoke tests.

<a id="ampyfin"></a>
### AmpyFin (first OSS Python version)
The earliest open‑source Python repo that seeded today’s modular platform.  
<a href="https://github.com/AmpyFin" title="Org index (main repo inside)">org entry</a> · <a href="https://www.ampyfin.com" title="Project home">site</a> · <code>#learn-in-public</code>

<a id="proto"></a>
### ampy‑proto
**Canonical schemas** for markets (bars/ticks/fundamentals/news/fx/corporate_actions/universe/signals/orders/fills/positions/metrics).  
[`pip install ampy-proto`](https://pypi.org/project/ampy-proto/) · <a href="https://github.com/AmpyFin/ampy-proto" title="Schemas repo">repo</a> · <code>#contracts-first</code>

<a id="envelope-headers"></a>
### ampy‑bus
**Deterministic messaging** — envelope, headers, QoS tiers, DLQ routing, NATS/Kafka helpers, trace propagation.  
<a href="https://github.com/AmpyFin/ampy-bus" title="Messaging helpers">repo</a> · <code>#trace-context</code> <code>#replays</code>

<a id="config"></a>
### ampy‑config
**Typed config & secrets facade** (Go/Python), runtime reloads, secret indirection.  
<a href="https://github.com/AmpyFin/ampy-config" title="Config facade">repo</a> · <code>#typed-config</code>

<a id="telemetry"></a>
### ampy‑observability
**Logs + metrics + tracing** with OTLP exporters; docker‑compose observability stack.  
<a href="https://github.com/AmpyFin/ampy-observability" title="Observability SDKs">repo</a> · <code>#domain-metrics</code> <code>#p95/p99</code>

<a id="yfinance-go"></a>
### yfinance‑go
Production‑minded free‑data client (historicals/quotes/fundamentals), bounded concurrency, session rotation, circuit breakers; library + CLI (`yfin pull`).  
<a href="https://github.com/AmpyFin/yfinance-go" title="Yahoo Finance Go client">repo</a> · <code>#bounded-concurrency</code>


---

<a id="how-i-work"></a>
## How I work

I start at the **whiteboard**: clarify the problem in one sentence, list non-goals, and write the invariants that must always hold.

Then I **research the domain** and past incidents: what broke before, where the data lies, which constraints (time semantics, currencies, ordering) are non-negotiable.

I **pin interfaces and contracts** before code—schemas with explicit units/decimals and `event_time`/`ingest_time`/`as_of`. I add three examples (happy, weird-but-valid, invalid) so expectations are concrete.

I **design for boring failure**: timeouts, retries with jitter, circuit breakers, idempotency keys, and a DLQ with structured reasons. There’s always a kill-switch.

**Observability is day 0**: JSON logs carry `trace_id`, `run_id`, and `universe_id`; metrics expose rates/latencies/backlogs; spans outline fetch → normalize → publish. One dashboard, few alerts, tied to user pain.

I **ship in small, reversible changes**: wire telemetry, validate, shadow-publish, then flag-gate the real path. Rollback is scripted and tested.

Confidence is **replay-driven**: golden fixtures (half-days, tz shifts, splits) and deterministic replays (same input + config ⇒ same bytes). CI fails on nondeterministic diffs or schema drift.

I **communicate the why**: each PR links the one-pager, states risk/mitigations, and shows how to reproduce locally.

After release, I **operate and learn**: runbooks with first actions, and when something bites, I add a fixture, a guardrail, and a short note so the next change is easier.


---

<a id="toolbox"></a>
## Toolbox
Go • Python • C/C++ • SQL · Protobuf · NATS JetStream/Kafka · OpenTelemetry/Prometheus/Grafana · Docker/Linux · PostgreSQL/DuckDB/MongoDB

---

<a id="say-hi"></a>
## Say hi
<a href="mailto:yeonholee50@gmail.com"><kbd>email</kbd></a> · <a href="https://www.linkedin.com/in/yeon-lee"><kbd>LinkedIn</kbd></a> · <a href="https://yeonthelee.tech"><kbd>site</kbd></a> · <a href="https://www.ampyfin.com"><kbd>AmpyFin</kbd></a>


