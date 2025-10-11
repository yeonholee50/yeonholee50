<div align="center">

# Yeon Lee
<sub>systems-minded software engineer · early in my career · learning in public</sub>

<a href="https://yeonthelee.tech"><kbd>site</kbd></a> ·
<a href="https://www.ampyfin.com"><kbd>ampyfin</kbd></a> ·
<a href="https://github.com/AmpyFin"><kbd>@AmpyFin</kbd></a> ·
<a href="mailto:yeonholee50@gmail.com"><kbd>email</kbd></a>

<br/>

<a href="#projects"><kbd>#contracts-first</kbd></a>
<a href="#how-i-work"><kbd>#deterministic-replays</kbd></a>
<a href="#projects"><kbd>#observability</kbd></a>
<a href="#projects"><kbd>#typed-config</kbd></a>
<a href="#notes"><kbd>#learn-in-public</kbd></a>

</div>

> *I'm not afraid of being left behind—I'm excited about what I can build with the emerging technologies of tomorrow.*

---

## ⌘K — Command Palette
[projects](#projects) • [how-i-work](#how-i-work) • [toolbox](#toolbox) • [say-hi](#say-hi)

---

## Projects

### AmpyFin (first OSS Python version)
The seed that became today’s modular platform.  
<kbd><a href="https://github.com/AmpyFin">org</a></kbd> · <kbd><a href="https://www.ampyfin.com">site</a></kbd>

### ampy-proto — canonical market schemas
Bars/Ticks/Fundamentals/News/FX/Corporate Actions/Universe/Signals/Orders/Fills/Positions/Metrics.  
<kbd><a href="https://github.com/AmpyFin/ampy-proto">repo</a></kbd> · <kbd><a href="https://pkg.go.dev/github.com/AmpyFin/ampy-proto">go pkg</a></kbd> · <kbd><a href="https://pypi.org/project/ampy-proto/">PyPI</a></kbd>

### ampy-bus — envelope, headers, QoS, DLQ, NATS/Kafka helpers
Deterministic messaging with trace propagation and replay controls.  
<kbd><a href="https://github.com/AmpyFin/ampy-bus">repo</a></kbd> · <kbd><a href="https://pkg.go.dev/github.com/AmpyFin/ampy-bus/cmd/ampybusctl">go pkg (CLI)</a></kbd> · <kbd><a href="https://pypi.org/project/ampy-bus/">PyPI</a></kbd>

### ampy-config — typed config & secrets façade (Go/Python)
Runtime reloads, secret indirection; no keys in code.  
<kbd><a href="https://github.com/AmpyFin/ampy-config">repo</a></kbd> · <kbd><a href="https://pkg.go.dev/github.com/AmpyFin/ampy-config/go/ampyconfig">go pkg</a></kbd> · <kbd><a href="https://pypi.org/project/ampy-config/">PyPI</a></kbd>

### ampy-observability — logs • metrics • tracing (OTLP)
Uniform JSON logs, Prometheus metrics, and tracing SDKs; docker-compose stack for local.  
<kbd><a href="https://github.com/AmpyFin/ampy-observability">repo</a></kbd> · <kbd><a href="https://pkg.go.dev/github.com/AmpyFin/ampy-observability/go/ampyobs">go pkg</a></kbd> · <kbd><a href="https://pypi.org/project/ampyobs/">PyPI</a></kbd>

### yfinance-go — concurrency-safe free-data client + CLI (`yfin pull`)
Historicals/quotes/fundamentals with session rotation & circuit breakers.  
<kbd><a href="https://github.com/AmpyFin/yfinance-go">repo</a></kbd> · <kbd><a href="https://pkg.go.dev/github.com/AmpyFin/yfinance-go">go pkg</a></kbd>

> **Note:** `tiingo-go` exists but is private (link intentionally omitted).

---

## How I work
I research the problem with stakeholders and end users, then whiteboard the one-line goal, non-goals, and the invariants that must hold.  
I pin **contracts before code** (explicit units/decimals; `event_time` / `ingest_time` / `as_of`) with concrete examples.  
I design for **boring failure** (timeouts, jittered retries, circuit breakers, DLQ, kill-switch) and ship **small, reversible changes** (shadow first, flag-gated release, scripted rollback).  
**Observability is day-0** (structured logs with trace context, labeled metrics, purposeful spans).  
Confidence is **replay-driven** (golden fixtures; deterministic replays; CI guards).  
I communicate **the why**, keep runbooks short, and write down what I learn.

---

## Toolbox
Python · Go · C/C++ · SQL · Protobuf · NATS JetStream/Kafka · OpenTelemetry/Prometheus/Grafana · Docker/Linux · PostgreSQL/DuckDB/MongoDB

---

## Notes
I build in public. If something looks off, open an issue—I’ll fix it and credit contributors.

---

## Say hi
<kbd><a href="mailto:yeonholee50@gmail.com">email</a></kbd> · <kbd><a href="https://www.linkedin.com/in/yeon-lee">linkedin</a></kbd> · <kbd><a href="https://yeonthelee.tech">site</a></kbd> · <kbd><a href="https://www.ampyfin.com">ampyfin</a></kbd>


